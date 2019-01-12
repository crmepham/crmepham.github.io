---
classes: wide
tags: [java, swagger, spring, authentication]
---
This post will explain how to configure Spring Boot 2 to access Swagger 2 using HTTP Basic authorization.
<h2>Requirements</h2>
Spring Boot 2.0.4.RELEASE
Swagger 2.9.2
<h2>Create the REST controller</h2>

```java
import com.server.common.model.Menu;
import com.server.dataservice.service.MenuService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController("menus")
public class MenuController
{
    @Autowired
    private MenuService menuService;

    @GetMapping("/get-all")
    public ResponseEntity&lt;List&lt;Menu&gt;&gt; getMenus() {
        return new ResponseEntity&lt;&gt;(menuService.getAll(), HttpStatus.OK);
    }
}
```

<h2>Create the configuration class</h2>

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.web.AuthenticationEntryPoint;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter
{
    @Autowired
    private AuthenticationEntryPoint authEntryPoint;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable().authorizeRequests()
                .anyRequest().authenticated()
                .and().httpBasic()
                .authenticationEntryPoint(authEntryPoint);
    }

    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication().withUser("john123").password("{noop}password").roles("USER");
    }

}
```

You could replace the simple in-memory authentication with anything else.

Now, start your Spring Boot 2 application and navigate to http://localhost:9030/swagger-ui.html. The port may differ.

You should be presented with a login dialog. Enter the username and password from the configuration file to gain access to the Swagger UI. Or alternatively use Postman.

<img class="aligncenter size-full wp-image-1062" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/08/Screen-Shot-2018-08-31-at-20.44.45.png" alt="" width="3214" height="1662" />

Notice the Authorization header! The value starts with "Basic " followed by <em>username:password</em> Base64 encoded.
