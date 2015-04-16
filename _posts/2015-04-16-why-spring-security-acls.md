---
layout: post
title: "Why Spring Security ACLs?"
excerpt: "[Spring Security ACL](http://grails.org/plugin/spring-security-acl) makes it much easier to implement object level permissions
and maintaining access control lists in your Grails app."
tags: [spring security acls, grails, plugins]
comments: true
---

I had recently written about the [benefits of using spring-security-core](http://vishesh.space/benefits-of-spring-security-with-grails/)
the other plugins that extend its capability are what make it truly valuable. One such use case is managing user permissions.

[Spring Security ACL](http://grails.org/plugin/spring-security-acl) makes it much easier to implement object level permissions
and maintaining access control lists in your Grails app.

## Flat domain structure
It has a very [flat domain structure](https://github.com/grails-plugins/grails-spring-security-acl/tree/master/grails-app/domain/grails/plugin/springsecurity/acl) 
making it an ideal starting place for both SQL and NoSQL databases.

## Bulletproof your business logic with DRY access control
There are some neat annotations available that will do the pre and post access checks on your service methods:

	<ul class="star">
	<li><a href="http://docs.spring.io/spring-security/site/docs/3.2.x/apidocs/org/springframework/security/access/prepost/PreAuthorize.html" target="blank">@PreAuthorize</a></li>
	<li><a href="http://docs.spring.io/spring-security/site/docs/3.2.x/apidocs/org/springframework/security/access/prepost/PreFilter.html" target="blank">@PreFilter</a></li>
	<li><a href="http://docs.spring.io/spring-security/site/docs/3.2.x/apidocs/org/springframework/security/access/prepost/PostAuthorize.html" target="blank">@PostAuthorize</a></li>
	<li><a href="http://docs.spring.io/spring-security/site/docs/3.2.x/apidocs/org/springframework/security/access/prepost/PostFilter.html" target="blank">@PostFilter</a></li>
	</ul>

	@PreAuthorize("hasRole('ROLE_USER')")
	@PostFilter("hasPermission(filterObject, read) or " +
				"hasPermission(filterObject, admin)")
	List getAllReports(params = [:]) {
		Report.list(params)
	}

The above service method call has two checks, the first checks if the user has the mentioned role and filters out
any list items that the user might not have access to. This becomes very handy when you have query that produces limited results
and you don't want to rely on joins or you are on a NoSQL based system. (I have not tested this on NoSQL yet).

## Generic permissions that are easily extensible
It provides the basic READ, WRITE, CREATE, DELETE and ADMINISTRATION permissions by default but can be easily extended
to add more [custom permissions](http://grails-plugins.github.io/grails-spring-security-acl/docs/manual/guide/usage.html#customPermissions)

## Utility classes and integration with Spring Security Core
This too has a couple of utility classes that makes managing the permissions much easier like [AclUtilService](https://github.com/grails-plugins/grails-spring-security-acl/blob/master/grails-app/services/grails/plugin/springsecurity/acl/AclUtilService.groovy)
and [AclService](https://github.com/grails-plugins/grails-spring-security-acl/blob/master/grails-app/services/grails/plugin/springsecurity/acl/AclService.groovy)

The biggest advantage by far is its integration with the rest of the spring security ecosystem.
