---
ID: 922
post_title: Migrate SugarCRM data to SalesForce
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/guide/migrate-sugarcrm-data-to-salesforce/
published: true
post_date: 2017-06-04 12:29:08
---
The following post will describe how to migrate all Accounts, Contacts, Tasks and Notes from SugarCRM to SalesForce whilst maintaining their relationships with one another. More specifically; preparing the .csv import files for importing into the <a href="https://appexchange.salesforce.com/listingDetail?listingId=a0N300000016ZoVEAU">Jitterbit </a>data loader.
<h3>Step 1. Create a custom field against the Account object</h3>
Name the custom field 'sugarId'. This field is very important and will be used to hold a text value which is the SugarCRM ID for the Account, and will allow the Account to retain its relationship with Contacts, Notes and Tasks.
<h3>Step 2. Export all Accounts from SugarCRM</h3>
The following SQL script will pull the Accounts data from the SugarCRM database, and will also perform any data manipulation/transformation that may be required to match up data with relevant Account custom fields that may exist.

At this point, it is worth mentioning that the most important part of the migration process is making sure that the data is correctly formatted and relevant. This is a good opportunity to also disregard any unnecessary or old data that doesn't need to be migrated.
<pre class="EnlighterJSRAW" data-enlighter-language="sql">select

'SugarId__c', 'Name', 'Website', 'Type', 'Description', 'Phone', 'Incumbent__c', 'Lead_Status__c', 'Courier__c', 'Interested_In__c', 'Campaign__c', 'E_commerce_Platforms__c'

union all

select
a.id SugarId__c,
ifnull(a.name, '') Name,
ifnull(a.website, '') Website,
ifnull(a.account_type, '') Type,
ifnull(replace(a.description,'"',''''), '') Description,
ifnull(a.phone_office, '') Phone,
ifnull(ac.incumbent_c, '') Incumbunt__c,
ifnull(ac.lead_status_c, '') Lead_Status__c,

ifnull(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(ac.courier2_c,
'^',''),
',',';'), 
'ups', 'UPS'),
'tnt', 'TNT'),
'dhl', 'DHL'),
'apc', 'APC'),
'usps', 'USPS'),
'yodel', 'Yodel'),
'ukmail', 'UK Mail'),
'geopost', 'GeoPost (DPD)'),
'hermes', 'Hermes'),
'metapack', 'MetaPack'),   
'parcel_force', 'Parcel Force'),  
'interlink_express', 'Interlink Express'),
'royal_mail', 'Royal Mail'), '') Courier__c,

ifnull(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(ac.interested_in_c,
'^',''),
',',';'),
'linnworks','Linnworks'),
'ebay','Ebay'),
'amazon','Amazon'),
'openerp','Open ERP'),
'sap','SAP'), 
'sage','Sage'), '') Interested_In__c,

ifnull(ac.campaign_c, '') Campaign__c,

ifnull(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(
replace(ac.cart2_c,
'^',''),
',',';'),
'woocommerce','WooCommerce'),
'ebay','EBay'),
'actinic','Actinic'),
'visualsoft','Visual Soft'),
'erol','EROL'),
'retail_store','Retail Store'),
'inhouse_development','Inhouse Development'),
'shopify','Shopify'),
'magento','Magento'), '') E_commerce_Platforms__c

from accounts a
left join accounts_cstm ac on ac.id_c = a.id
where a.deleted = false

into outfile '/var/lib/mysql-files/Accounts.csv'
fields terminated by ','
optionally enclosed by '"'
escaped by ''
lines terminated by '\n';</pre>
<h3>Step 3. Import the Accounts.csv file into SalesForce using the Jitterbit data loader.</h3>
<h3>Step 4. Export the Accounts 'id' and 'sugarId_c' values from SalesForce using the Jitterbit data loader.</h3>
We now have the SalesForce and SugarCRM ID's for each Accounts.
<h3>Step 5. Import the Accounts IDs into the SugarCRM database</h3>
Create a temporary table in the SugarCRM database.
<pre class="EnlighterJSRAW" data-enlighter-language="sql">create table accounts_mapping (
  sugarId varchar(255),
  salesForceId varchar(255)
);</pre>
Import the .csv file containing the Accounts ID mappings.
<pre class="EnlighterJSRAW" data-enlighter-language="sql">LOAD DATA LOCAL INFILE '/var/lib/mysql-files/Accounts_id_mapping.csv' 
INTO TABLE accounts_mapping 
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"' 
LINES TERMINATED BY "\n" (salesForceId,sugarId);</pre>
Note that you may need to enable to LOAD DATA. This can be done using the command line flag "<code class="EnlighterJSRAW" data-enlighter-language="sql">--local-infile"</code>. Also, you may need to remove a carriage return that may have been added to the SugarCRM ID values. You can do this with the following query: <code class="EnlighterJSRAW" data-enlighter-language="sql">update accounts_mapping set sugarId = replace(sugarId, '\r','');</code>
<h3>Step 6. Export SugarCRM Tasks using a join on the temporary table to retain the relationship with the Account</h3>
<pre class="EnlighterJSRAW" data-enlighter-language="sql">select 'Status', 'Description', 'Priority', 'Subject', 'WHATID'

union all

select 
'Completed' Status,
ifnull(t.description,'') Description,
t.priority Priority,
ifnull(t.name,' ') Subject,
am.salesForceId WHATID
from tasks t
join accounts_mapping am on t.parent_id = am.sugarId
where deleted = false

into outfile '/var/lib/mysql-files/Tasks.csv'
fields terminated by ','
OPTIONALLY enclosed by '"'
lines terminated by '\n';</pre>
<h3>Step 7. Import the Tasks into SalesForce using the Jitterbit data loader.</h3>
<h3>Step 8. Export SugarCRM Notes using a join on the temporary table to retain the relationship with the Account</h3>
<pre class="EnlighterJSRAW" data-enlighter-language="null">select

'Body', 'isPrivate', 'OwnerId', 'ParentId', 'Title'

union all

select
ifnull(replace(n.description,'"',''''), 'n/a') Body,
0 isPrivate,
'0050Y000001SnN2QAK' OwnerId,
am.salesForceId WHATID,
ifnull(n.name, 'n/a') Title
from notes n
join accounts_mapping am on n.parent_id = am.sugarId
where n.deleted = false

into outfile '/var/lib/mysql-files/Notes.csv'
fields terminated by ','
optionally enclosed by '"'
escaped by ''
lines terminated by '\n';</pre>
Note that in the example above I have hard coded the SalesForce User ID. But you could also map users in a similar way to how we have already mapped the Account IDs. So you can retain the correct user/author for the Notes.
<h3>Step 9. Import the Notes into SalesForce using the Jitterbit data loader.</h3>
The SugarCRM Note object refers to the SalesForce Notes &amp; Attachments object in SalesForce (not the ContentNote object) which is not displayed on the Accounts page by default if you are using the new "Lightning Experience" theme. You can add the "Notes &amp; Attachments" section to the Accounts page from the Setup &gt; Page Layout settings.
<h3>Step 10. Export SugarCRM Contacts using a join on the temporary table to retain the relationship with the Account</h3>
<pre class="EnlighterJSRAW" data-enlighter-language="sql">select

'Title', 'Department', 'Email', 'MobilePhone', 'Phone', 'Salutation', 'FirstName', 'LastName', 'MailingStreet', 'MailingCity','MailingState','MailingPostalCode','MailingCountry', 'AccountId'

union all

select
ifnull(c.title, 'n/a') Title,
ifnull(c.department, 'n/a') Department,
ifnull(e.email_address, '') Email,
ifnull(c.phone_mobile, 'n/a') MobilePhone,
ifnull(c.phone_work, 'n/a') Phone,
ifnull(c.salutation, 'n/a') Salutation,
ifnull(c.first_name, 'n/a') FirstName,
ifnull(c.last_name, 'n/a') LastName,
ifnull(c.primary_address_street, 'n/a') MailingStreet,
ifnull(c.primary_address_city, 'n/a') MailingCity,
ifnull(c.primary_address_state, 'n/a') MailingState,
ifnull(c.primary_address_postalcode, 'n/a') MailingPostalCode,
ifnull(c.primary_address_country, 'n/a') MailingCountry,
ifnull(am.salesForceId, '') AccountId
from contacts c
left join email_addr_bean_rel er on er.bean_id = c.id
left join email_addresses e on e.id = er.email_address_id
left join accounts_contacts ac on ac.contact_id = c.id and ac.deleted = false
left join accounts a on ac.account_id = a.id and a.deleted = false
left join accounts_mapping am on a.id = am.sugarId
where c.deleted = false

into outfile '/var/lib/mysql-files/Contacts.csv'
fields terminated by ','
optionally enclosed by '"'
lines terminated by '\r\n';</pre>
<h3>Step 11. Import the Contacts into SalesForce using the Jitterbit data loader</h3>