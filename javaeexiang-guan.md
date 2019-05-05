## 1.Shiro

i.概述

shiro是apache的一个开源框架，是一个权限管理的框架，实现用户认证、用户授权。

spring中有spring security \(原名Acegi\)，是一个权限框架，它和spring依赖过于紧密，没有shiro使用简单。

shiro不依赖于spring，shiro不仅可以实现 web应用的权限管理，还可以实现c/s系统，分布式系统权限管理，shiro属于轻量框架，越来越多企业项目开始使用shiro。使用shiro实现系统的权限管理，有效提高开发效率，从而降低开发成本。

ii.Shiro结构

![](https://img-blog.csdn.net/20181011165546162?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM0MzQxMTYy/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 "在这里插入图片描述")

subject：主体，可以是用户也可以是程序，主体要访问系统，系统需要对主体进行认证、授权。

securityManager：安全管理器，主体进行认证和授权都是通过securityManager进行。

authenticator：认证器，主体进行认证最终通过authenticator进行的。

authorizer：授权器，主体进行授权最终通过authorizer进行的。

sessionManager：web应用中一般是用web容器对session进行管理，shiro也提供一套session管理的方式。

SessionDao： 通过SessionDao管理session数据，针对个性化的session数据存储需要使用sessionDao。

cache Manager：缓存管理器，主要对session和授权数据进行缓存，比如将授权数据通过cacheManager进行缓存管理，和ehcache整合对缓存数据进行管理。

realm：域，领域，相当于数据源，通过realm存取认证、授权相关数据。

iii.认证的流程

  


![](https://img-blog.csdn.net/20181011170602710?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzM0MzQxMTYy/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 "在这里插入图片描述")

1、通过ini配置文件创建securityManager

2、调用subject.login方法主体提交认证，提交的token

3、securityManager进行认证，securityManager最终由ModularRealmAuthenticator进行认证。

4、ModularRealmAuthenticator调用IniRealm\(给realm传入token\) 去ini配置文件中查询用户信息。

5、IniRealm根据输入的token（UsernamePasswordToken）从 shiro.ini查询用户信息，根据账号查询用户信息（账号和密码）。

如果查询到用户信息，就给ModularRealmAuthenticator返回用户信息（账号和密码）。

如果查询不到，就给ModularRealmAuthenticator返回null。

6、ModularRealmAuthenticator接收IniRealm返回Authentication认证信息。









