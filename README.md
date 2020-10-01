# 1. Demo Application

This is sample application for develop using [TERASOLUNA Server Framework for Java (5.x)](http://terasoluna.org).<br>
**Currently, this application is under developing !!!**

This application is developed based [TERASOLUNA Server Framework for Java (5.x) Development Guideline](http://terasolunaorg.github.io/guideline/).<br>
But it being customized by my opinion in the partially (this means is not 100% compliance by guideline).

[![Java CI with Maven](https://github.com/kazuki43zoo/demo-application/workflows/Java%20CI%20with%20Maven/badge.svg)](https://github.com/kazuki43zoo/demo-application/actions?query=workflow%3A%22Java+CI+with+Maven%22)


# 2. Application Structure

Structure of this application is following.<br><br>
![alt text](./images/application-structure.png "Application Structure")

| Layer | Component/Library | Main responsibilities |
| :-----: | --------- | --------------------- |
| Client Layer         | [jQuery 3.5.1](http://jquery.com/) | Provide the useful javascript operations. |
|                      | [AngularJS 1.2.32](https://code.angularjs.org/1.2.32/docs/guide) | Provide the JavaScript MVW Framework. |
|                      | [Bootstrap 3.4.1](https://getbootstrap.com/docs/3.4/) | Provide the useful & stylish css configurations, and provide the useful client components(alert, message dialog, etc..). |
| Server Side Platform | Java SE 8 Java Virtual Machine | Provide the execution environment for Java application. | 
|                      | Java EE 7 Servlet Container | Provide the servlet engine that supports servlet 3.1 specification. | 
|                      | [Spring Framework 5.2.3.RELEASE](http://projects.spring.io/spring-framework/) | Provide mechanism of CDI(Context and Dependency Inject). In this application, use the transaction management and AOP mechanism.|
| Application Layer    | [Spring Security 5.2.1.RELEASE](http://projects.spring.io/spring-security/) | Provide mechanism of security on web application. |
|                      | [Spring MVC 5.2.3.RELEASE](http://projects.spring.io/spring-framework/) | Provide mechanism of Java MVC Framework for web application. |
|                      | [Bean Validation 2.0(JSR-380)](https://beanvalidation.org/2.0/) | Provide mechanism of validation for request data. In this application, use [Hibernate Validator 6.0.18.Final](http://hibernate.org/validator/) as implementation provider.|
|                      | Controller | Handle a request & delegate a business procedure to the services.  |
|                      | DTO | Hold transfer data(form data or resource data) of application layer(web layer). |
|                      | JSP | Generate presentation component(HTML) by accessing to DTO and Domain Object via `Model` object or `RedirectAttributes` provided by Spring MVC.  |
| Domain Layer         | Domain Object | Hold domain data & implements core business logic. |
|                      | Repository | Define & provide CRUD operations(interfaces) to the Domain objects. |
|                      | Service | Implements & provide business procedure(Part of the business logic) and provide transaction boundary. |
| Infrastructure Layer | [MyBatis 3.5.3](http://mybatis.github.io/mybatis-3/) | Provide mechanism of database access. In this application, use the Mapper interface as Repository interface. SQL is implements in Mapper MXL. |
| Libraries            | [TERASOLUNA Server Framework for Java (5.x) Common Library 5.6.0.RELEASE](https://github.com/terasolunaorg/terasoluna-gfw) | Provide useful functionalities(Transaction Token Check, Codelist, Pagination, MessageManagement, ExceptionHandling, etc..) on develop enterprise application. And provide dependency on useful OSS libraries([Dozer](https://github.com/DozerMapper/dozer), [Joda-Time](http://www.joda.org/joda-time/), [Apache-Commons families](http://commons.apache.org/), etc..). |

## 2.1. Dependency libraries for application-specific
The following libraries is dependency for application-specific without relate on TERASOLUNA Server Framewrok for Java (5.x).

| Library(Group Id:Artifact Id) | Version | Description |
| ----- | :-----:| --------------------- |
| [com.h2database:h2](http://www.h2database.com/) | 1.4.200 \* | Depends on to access H2 database. |
| [org.projectlombok:lombok](http://projectlombok.org/) | 1.18.10 \* | Depends on for automatically generate a methods(getter/setter/etc ...) of JavaBean. By the this library use, we can develop smoothly and effectively.<br>**If you are use IDE as Eclispe or STS(Spring Tool Suite) or IDEA or NetBeans, please  install lombok.jar to the IED. In detail of how to install, please see [here](http://jnb.ociweb.com/jnb/jnbJan2010.html#installation).** (If IDEA , please install lombok plugin) |
| [org.springframework.hateoas:spring-hateoas](https://github.com/spring-projects/spring-hateoas) | 1.0.3.RELEASE \* | Depends on to support HATEOAS as REST API. |
| [io.github.bonigarcia:webdrivermanager](http://www.h2database.com/) | 4.0.0 | Depends on download an execution file of selenium `WebDrivier`. (test scope) |

\* The version is managed by Spring Boot Dependency via TERASOLUNA Server Framewrok for Java (5.x) parent project.

## 2.2. Version up of dependency libraries for application-specific  
The following libraries are version up from version that TERASOLUNA Server Framework for Java (5.x) depend on. Reason of version up is to try the latest version.

| Library | In this application | TERASOLUNA Server Framework<br>for Java (5.x) |
| ----- | :-----: | :-----: |

## 2.3. Java package Structure

![alt text](./images/java-package-structure.png "Java package Structure")

Description coming soon...

## 2.4. Resources package Structure

![alt text](./images/resources-package-structure.png "Resources package Structure")

Description coming soon...

## 2.5. Web application(war) Structure

![alt text](./images/web-application-structure.png "Web application(war) Structure")

Description coming soon...

# 3. Application Functionalities

Functionalities of this application are follows.<br>

| No | Functionality name | Description |
| :-----: | ----- | ----- |
| 1 | Welcome page | Coming soon... |
| 2 | Authentication | Coming soon... |
| 3 | Authorization | Coming soon... |
| 4 | Security Countermeasure | Coming soon... |
| 5 | Session Management | Coming soon... |
| 6 | Accounts Management | Coming soon... |
| 7 | My Profile Management | Coming soon... |
| 8 | Password Management | Coming soon... |
| 9 | Time Card | Coming soon... |
| 10 | Others... | Coming soon... |


# 4. Authentication
This section describe about authentication in this application.<br>
In this application, authentication(login and logout) processing are implements using Spring Security and Spring MVC.<br>

  > ![alt text](./images/info.png "Note")<br>
  > **Responsibility of each other are following.** 
  >
  > * **Spring Security has responsible for the authentication processing.**
  > * **Spring MVC has responsible for input values validation and the screen control.**

## 4.1. View the login form

Display processing flow of login form are following.

[alt text](./images/flow-view-login-form.png "Flow of view the login form page")

### Access the protected page when not authenticate

If access the protected page when not authenticate, spring-security redirect to the uri(page) that is defined in `login-page` attribute of `sec:form-login` element.

`src/main/resources/META-INF/spring/spring-security.xml`

```xml
<sec:http auto-config="true" use-expressions="true">
    <!-- omit -->
    <sec:form-login login-processing-url="/auth/authenticate" login-page="/auth/login?encourage"
        username-parameter="accountId" password-parameter="password"
        authentication-details-source-ref="customAuthenticationDetailsSource"
        authentication-failure-handler-ref="authenticationFailureHandler" />
    <!-- omit -->
</sec:http>
```

### Encourage the login

Request of `GET /auth/login?encourage` and `GET /auth/login` are handled `LoginController`.
In the `LoginController`, set the message and view the login form page.

`src/main/java/com/github/kazuki43zoo/app/auth/LoginController.java`

```java
@RequestMapping("auth/login")
@Controller
public class LoginController {
    // omit

    @TransactionTokenCheck(type = TransactionTokenType.BEGIN)
    @RequestMapping(method = RequestMethod.GET)
    public String showLoginForm() {
        return "auth/loginForm";
    }

    @RequestMapping(method = RequestMethod.GET, params = "encourage")
    public String encourageLogin(RedirectAttributes redirectAttributes) {
        redirectAttributes.addFlashAttribute(Message.AUTH_ENCOURAGE_LOGIN.buildResultMessages());
        return "redirect:/auth/login";
    }

    // omit
}
```

  > ![alt text](./images/info.png "Note")<br>
  > **When view the login form page, global transaction for transaction token check is begun.**


Generate screen data(response data) by the `auth/loginForm` view(JSP). 

`src/main/webapp/WEB-INF/views/auth/loginForm.jsp`

```jsp
<c:if test="${!param.including}">
    <t:messagesPanel messagesAttributeName="SPRING_SECURITY_LAST_EXCEPTION" messagesType="danger" />
    <t:messagesPanel />
    <spring:hasBindErrors name="loginForm">
        <spring:nestedPath path="loginForm">
            <div class="alert alert-danger">
                <form:errors path="*" />
            </div>
        </spring:nestedPath>
    </spring:hasBindErrors>
</c:if>
<form:form action="${contextPath}/auth/login" class="navbar-form" method="post" modelAttribute="loginForm">
    <div class="form-group">
        <form:input type="text" path="accountId" class="form-control" placeholder="Account ID" />
    </div>
    <div class="form-group">
        <form:password path="password" class="form-control" placeholder="Password" />
    </div>
    <button class="btn">
        <span class="glyphicon glyphicon-log-in"></span>
    </button>
</form:form>
```

  > ![alt text](./images/info.png "Note")<br>
  > **`loginForm.jsp` is included from the `src/main/webapp/WEB-INF/views/common/layout/topNavbar.jsp`.**
  > **Hence, in this JSP, use the `including` parameter to judge the included / not included.**
  > **When are included from `topNavbar.jsp`, error message does not displayed in this page.** 


### Actual screen(response) are following.

![alt text](./images/screenshot-view-login-form.png "login form")


## 4.2. Login(Authenticate)

Login processing flow are following.

![alt text](./images/flow-authentication.png "Flow of login")

### Submit login request

In this application, parameter name of username and password has change the default settings of Spring Security.

`src/main/webapp/WEB-INF/views/auth/loginForm.jsp`

```jsp
<form:form action="${contextPath}/auth/login" class="navbar-form" method="post" modelAttribute="loginForm">
    <div class="form-group">
        <form:input type="text" path="accountId" class="form-control" placeholder="Account ID" />
    </div>
    <div class="form-group">
        <form:password path="password" class="form-control" placeholder="Password" />
    </div>
    <button class="btn">
        <span class="glyphicon glyphicon-log-in"></span>
    </button>
</form:form>
```

### Receive the login request by the Spring MVC

In this application, `LoginController` receive the login request, and execute validation of login form data. If not exists violation, `LoginContoller` forward to the authentication processing of Spring Security.

  > ![alt text](./images/tip.png "Tip")<br>
  > **If not exists requirement as input value validation or re-display, Spring MVC is not required.**

`src/main/java/com/github/kazuki43zoo/app/auth/LoginController.java`

```java
@RequestMapping("auth/login")
@Controller
public class LoginController {
    // omit

    @TransactionTokenCheck
    @RequestMapping(method = RequestMethod.POST)
    public String login(@Validated LoginForm form, BindingResult bindingResult) {

        if (bindingResult.hasErrors()) {
            return showLoginForm();
        }

        return "forward:/auth/authenticate";
    }

    // omit
}
```

  > ![alt text](./images/info.png "Note")<br>
  > **In the login processing , execute global transaction token check. Global transaction are begin when view the welcom page or the login page.**

`src/main/java/com/github/kazuki43zoo/app/auth/LoginForm.java`

```java
@AllArgsConstructor
@NoArgsConstructor
@Data
public class LoginForm implements Serializable {
    private static final long serialVersionUID = 1L;
    @NotNull
    private String accountId;
    @NotNull
    private String password;
}
```

  > ![alt text](./images/point.png "Point")<br>
  > For forward to the authentication processing of Spring Security, as the settings of `SpringSecurityFilterChain`, need add `<dispatcher>FORWARD</dispatcher>` .

`src/main/webapp/WEB-INF/web.xml`

```xml
<filter>
    <filter-name>SpringSecurityFilterChain</filter-name>
    <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
    <init-param>
        <param-name>targetBeanName</param-name>
        <param-value>springSecurityFilterChain</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>SpringSecurityFilterChain</filter-name>
    <url-pattern>/auth/authenticate</url-pattern>
    <dispatcher>FORWARD</dispatcher>
</filter-mapping>
<filter-mapping>
    <filter-name>SpringSecurityFilterChain</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

```

### Receive the login(authentication) request by the Spring Security

Spring Security execute the authentication processing when was accessed to the url that is defined in `login-processing-url` attribute of `sec:form-login` element.
In this application, `login-processing-url` & `username-parameter` & `password-parameter` attribute of `sec:form-login` element has change the default settings of Spring Security.<br>

  > ![alt text](./images/important.png "Important")<br>
  > **Reason of changing default settings is to hide the fact that are using the Spring Security as security countermeasure. If occur the security vulnerability in the Spring Security, be able to reduce the risk of attack to this application.**

`src/main/resources/META-INF/spring/spring-security.xml`

```xml
<sec:http auto-config="true" use-expressions="true">
    <!-- omit -->
    <sec:form-login login-processing-url="/auth/authenticate" login-page="/auth/login?encourage"
        username-parameter="accountId" password-parameter="password"
        authentication-details-source-ref="customAuthenticationDetailsSource"
        authentication-failure-handler-ref="authenticationFailureHandler" />
    <!-- omit -->
</sec:http>
```

### Execute authentication processing

In this application, authentication realize using the `DaoAuthenticationProvider` of Spring Security.<br>
`DaoAuthenticationProvider` has authenticate by using the user information that are loaded from the data store.<br>
In `DaoAuthenticationProvider`, be able to check for the status of loaded user. Actually checking contents are following.

  > ![alt text](./images/info.png "Note")<br>
  > **User information are loaded as instance of the `CustomUserDetails` (extended class in this application). In this application, load the user information via the `CustomUserDetailService` (extended class in this application).**


| No | Checking content | Specification in this application |
| :-----: | ----- | ----- |
| 1 | Specified user exists ? | Fetches the record that matches specified account id from the account table. If not exists matched record, occur the authentication error. |
| 2 | Specified user is not lock ? | Fetches the password failure count of fetched account. If it is over the max count of password failure count, occur the authentication error. |
| 3 | Specified user is enable ? | Fetches the enable flag of fetched account. If it is false(disabled), occur the authentication error. |
| 4 | Specified user is not expired ? | In this application, not support this checking. This means that check result is OK at always. |
| 5 | Specified user's password is not expired ? | Fetches the last modified date time of password. If it not modified during the password valid days period, encourage the password changing. |
| 6 | Matches the specified password ? | Fetches the password. If it not matches the specified password, occur the authentication error as bad credential.  |

`src/main/resources/META-INF/spring/spring-security.xml`

```xml
<sec:authentication-manager>
    <sec:authentication-provider user-service-ref="customUserDetailsService">
        <sec:password-encoder ref="passwordEncoder" />
    </sec:authentication-provider>
</sec:authentication-manager>
```

  > ![alt text](./images/info.png "Note")<br>
  > **`customUserDetailsService` are scan by component-scan.**
  > **`passwordEncoder` are defined in `src/main/resources/META-INF/spring/applicationContext.xml`. In this application, use the `BCryptPasswordEncoder`.**

### Execute authentication success processing

description coming soon...

## 4.3. Handle login error

![alt text](./images/flow-handle-authentication-error.png "Flow of handle the authentication error")

description coming soon...

## 4.4. Handle validation error

![alt text](./images/flow-handle-authentication-validation-error.png "Flow of handle the validation error on login")

description coming soon...

## 4.5. Logout

![alt text](./images/flow-logout.png "Flow of logout")

description coming soon...

## 4.6. Logout by session timeout
Coming soon...

# 5. Authorization
This section describe about authorization in this application.<br>
In this application, authorization(access control of protected page) processing are implements using Spring Security.<br>

Coming soon...

# 6. Other Security Countermeasure
This section describe about other security countermeasure in this application.<br>

## 6.1. Session Fixation Attacks Protection
Coming soon...

`src/main/resources/META-INF/spring/spring-security.xml`

```xml
<sec:http auto-config="true" use-expressions="true">
    <!-- omit -->
    <sec:session-management invalid-session-url="/error/invalidSession"
        session-fixation-protection="migrateSession"  />
    <!-- omit -->
</sec:http>
```

## 6.2. CSRF Attacks Protection
Coming soon...

`src/main/resources/META-INF/spring/spring-security.xml`

```xml
<sec:http auto-config="true" use-expressions="true">
    <!-- omit -->
    <sec:csrf request-matcher-ref="csrfRequestMatcher" />
    <!-- omit -->
</sec:http>
```
```xml
<bean id="csrfRequestMatcher" class="org.springframework.security.web.util.matcher.AndRequestMatcher">
    <constructor-arg>
        <list>
            <bean class="org.springframework.security.web.csrf.CsrfFilter$DefaultRequiresCsrfMatcher"/>
            <bean class="org.springframework.security.web.util.matcher.NegatedRequestMatcher">
                <constructor-arg ref="csrfExclusionPathMatcher" />
            </bean>
        </list>
    </constructor-arg>
</bean>
<bean id="csrfExclusionPathMatcher" class="org.springframework.security.web.util.matcher.OrRequestMatcher">
    <constructor-arg>
        <list>
            <bean class="org.springframework.security.web.util.matcher.AntPathRequestMatcher">
                <constructor-arg index="0" value="/vendor/h2/**" />
            </bean>
        </list>
    </constructor-arg>
</bean>
```

## 6.3. XSS attacks Protection
Coming soon...

`src/main/resources/META-INF/spring/spring-security.xml`

```xml
<sec:http auto-config="true" use-expressions="true">
    <!-- omit -->
    <sec:headers>
        <!-- omit -->
        <sec:content-type-options />
        <sec:xss-protection/>
    </sec:headers>
    <!-- omit -->
</sec:http>
```

## 6.4. Clickjacking Attacks Protection
Coming soon...

`src/main/resources/META-INF/spring/spring-security.xml`

```xml
<sec:http auto-config="true" use-expressions="true">
    <!-- omit -->
    <sec:headers>
        <!-- omit -->
        <sec:frame-options policy="SAMEORIGIN" />
        <!-- omit -->
    </sec:headers>
    <!-- omit -->
</sec:http>
```

## 6.5. Directory Traversal Attacks Protection
Coming soon...


## 6.6. Protected resource not cache

`src/main/resources/META-INF/spring/spring-security.xml`

```xml
<sec:http auto-config="true" use-expressions="true">
    <!-- omit -->
    <sec:headers>
        <sec:cache-control />
        <!-- omit -->
    </sec:headers>
    <!-- omit -->
</sec:http>
```

## 6.7. HTTP Strict Transport Security (HSTS)
Coming soon...

`src/main/resources/META-INF/spring/spring-security.xml`

```xml
<sec:http auto-config="true" use-expressions="true">
    <!-- omit -->
    <sec:headers>
        <!-- omit -->
        <sec:hsts />
        <!-- omit -->
    </sec:headers>
    <!-- omit -->
</sec:http>
```


# 7. Session Management
This section describe about session management in this application.<br>

## 7.1. Detect Session timeout
Coming soon...

