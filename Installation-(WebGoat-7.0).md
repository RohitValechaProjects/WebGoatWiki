The WebGoat Readme (link to readme) has the most extensive and up to date installation instructions.

## Configure new WebGoat users in your installation
 WebGoat uses spring-security.xml to configure users.

```
<!-- Authentication Manager -->
<authentication-manager alias="authenticationManager">
  <authentication-provider>
    <user-service>
      <user name="guest" password="guest" authorities="ROLE_WEBGOAT_USER" />
      <user name="webgoat" password="webgoat" authorities="ROLE_WEBGOAT_ADMIN" />
      <user name="server" password="server" authorities="ROLE_SERVER_ADMIN" />
    </user-service>
  </authentication-provider>
</authentication-manager>  
```

## Adding Users

Usually WebGoat only requires logging in with the user:guest and password:guest. But maybe in laboratory you have made a setup with one server and a lot of clients. In this case you might want to have a user for every client, you will have to alter /WEB-INF/spring-security.xml to add additional users. We recommend not to use real passwords as the passwords are stored in plain text in this file!    

## Adding a new User

Adding a user is straight forward. You can use the guest entry as an example. The added users should have the same role as the guest user. The new user/password will not show on the login page. Add lines like this to the /WEB-INF/spring-security.xml file:

```
<user name="guest2" password="guest2" authorities="ROLE_WEBGOAT_USER" />
...
```
