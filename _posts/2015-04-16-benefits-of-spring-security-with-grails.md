---
layout: post
title: "Benefits Of Using Spring Security With Grails"
excerpt: "There are some obvious benefits to writing custom code vs using a plugin. When using a plugin you get a lot of things
off the shelf rather than writing it your self. But using something as mature as Spring Security has its unique advantages."
tags: [spring security, grails, plugins]
comments: true
---

There are some obvious benefits to writing custom code vs using a plugin. When using a plugin you get a lot of things
off the shelf rather than writing it your self. But there is always that risk of adding more bloat to your code base than
is needed, debugging and finally bug fixes. Using something as mature as Spring Security has its unique advantages and in
my experience a very extensible family of plugins that have got the most love from the Grails community. 

## 1. Basic Authentication and User Management
If you are involved with writing multiple apps you would appreciate how easy it is these days to get an app running with
basic user management and authentication across various platforms and Grails is no different. You could setup Spring
Security Core and Spring Security UI in around 30 minutes.

- Certificate X509 authentication
- Rember-Me Cookie configurations
- Ajax authentication
- Password Hashing
- Salted Password

All out of the box!

## 2. Multiple ways to protect an endpoint
	
###	Request mappings
You can [configure request mappings](http://grails-plugins.github.io/grails-spring-security-core/guide/requestMappings.html)
to secure URLs

	grails.plugin.springsecurity.controllerAnnotations.staticRules = [
		'/':               ['permitAll'],
		'/index':          ['permitAll'],
		'/index.gsp':      ['permitAll'],
		'/assets/**':      ['permitAll'],
		'/**/js/**':       ['permitAll'],
		'/**/css/**':      ['permitAll'],
		'/**/images/**':   ['permitAll'],
		'/**/favicon.ico': ['permitAll']
	]

### Annotate an endpoint directly
Simply adding annotation to a controller action like

	@Secured(['ROLE_ADMIN'])
	def index() {
		render 'you have ROLE_ADMIN'
	}

to protect one of the endpoints or if you wanted to restrict the entire controller, simply add the annotation to the class

	@Secured(['ROLE_ADMIN'])
	class SecureController

## 3. Utility code that just shouldn't be written
[SpringSecurityService](http://grails-plugins.github.io/grails-spring-security-core/guide/helperClasses.html#springSecurityService)
and [SpringSecurityUtils](http://grails-plugins.github.io/grails-spring-security-core/guide/helperClasses.html#springSecurityUtils) 
let you do things like:

- Get basic details of the current user (because you don't want to load the entire user object every time
you want to deal with the current user).
- Load current user
- Check if the user has a particular role or does not have a particular role

## 4. Switch or operate as a different user
It can be configured to allow admins to switch user accounts while they are on the app. This is specially helpful while debugging and
seeing exactly what the other user is seeing without asking their password.

## 5. Allows you to have a notion of Group
This makes it easier to give a [group of users a set of authorities](http://grails-plugins.github.io/grails-spring-security-core/guide/domainClasses.html#authorityGroupClass).

## 6. Close to 15 plugins make it easier to extend your authentication needs
<ul class="star">
<li><a href="http://grails.org/plugin/spring-security-acl" class="pageLink">Spring Security ACL</a> which adds support for object-level and method-level authorization using ACLs (access control list)</li>
<li><a href="http://grails.org/plugin/spring-security-appinfo" class="pageLink">Spring Security AppInfo</a> which provides a basic UI to view the security configuration</li>
<li><a href="http://grails.org/plugin/spring-security-cas" class="pageLink">Spring Security CAS</a> which adds support for single sign-on using Jasig CAS</li>
<li><a href="http://grails.org/plugin/spring-security-openid" class="pageLink">Spring Security OpenID</a> which adds support for OpenID authentication</li>
<li><a href="http://grails.org/plugin/spring-security-facebook" class="pageLink">Spring Security Facebook</a> which adds support for Facebook authentication</li>
<li><a href="http://grails.org/plugin/spring-security-kerberos" class="pageLink">Spring Security Kerberos</a> which adds support for single sign-on using Kerberos</li>
<li><a href="http://grails.org/plugin/spring-security-ldap" class="pageLink">Spring Security LDAP</a> which adds support for LDAP and ActiveDirectory authentication</li>
<li><a href="http://grails.org/plugin/spring-security-mock" class="pageLink">Spring Security Mock</a> which adds support for fake/mock authentication during developement</li>
<li><a href="http://grails.org/plugin/spring-security-oauth2-provider" class="pageLink">Spring Security OAuth2 Provider</a> which allows your application to be an OAuth2 Provider</li>
<li><a href="http://grails.org/plugin/spring-security-radius" class="pageLink">Spring Security RADIUS</a> which adds support for RADIUS authentication</li>
<li><a href="http://grails.org/plugin/spring-security-rest" class="pageLink">Spring Security REST</a> which uses a token-based workflow to implement authentication for REST APIs</li>
<li><a href="http://grails.org/plugin/spring-security-shibboleth-native-sp" class="pageLink">Spring Security Shibboleth Native SP</a> which adds support for container provided Shibboleth authentication.</li>
<li><a href="http://grails.org/plugin/spring-security-shiro" class="pageLink">Spring Security Shiro</a> which adds support for using Shiro ACLs and permissions.</li>
<li><a href="http://grails.org/plugin/spring-security-twitter" class="pageLink">Spring Security Twitter</a> which adds support for Twitter authentication</li>
<li><a href="http://grails.org/plugin/spring-security-ui" class="pageLink">Spring Security UI</a> which provides CRUD screens and other user management workflows.</li>
</ul>
