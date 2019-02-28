---
layout: post
title: Rails-like 'flash' in Spring, part 2
tags: []
typo_id: 317
---

<style type="text/css">
@import url(/stylesheets/textmate/brilliance_black.css);
</style>

(Continued from [part 1]({{ site.baseurl }}{% post_url 2007-12-13-rails-like-flash-in-spring-part-1 %}))

Next you need a component which runs at the conclusion of every request. This component is responsible for decrementing the message counters in the flash object:

```java
package info.evansweb.spring.examples.flash;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.web.servlet.handler.HandlerInterceptorAdapter;

/**
 * Copyright 2007 Jon Evans, jon@springyweb.com
 *
 *  Licensed under the Apache License, Version 2.0 (the "License");
 *  you may not use this file except in compliance with the License.
 *  You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 *  Unless required by applicable law or agreed to in writing, software
 *  distributed under the License is distributed on an "AS IS" BASIS,
 *  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 *  See the License for the specific language governing permissions and
 *  limitations under the License.
 * 
 * @author Jon Evans, jon@springyweb.com
 *
 */
public class FlashDecrementer extends HandlerInterceptorAdapter {

  private Flash flash;

  public void setFlash(Flash flash) {
    this.flash = flash;
  }

  public void decr() {
    if (flash!=null) {
      flash.decr();
    }
  }

  public void afterCompletion(HttpServletRequest request,
      HttpServletResponse response, Object handler, Exception exception)
      throws Exception {
    decr();
  }
}
```

It gets wired into the Spring framework in your applicationContext.xml:

```xml
  <bean id="flash" class="info.evansweb.spring.examples.flash.Flash"
    scope="session">
    <!-- Google for aop:scoped-proxy if you don't understand why this is here  -->
    <aop:scoped-proxy />
  </bean>

  <bean id="flashDecrementer"
    class="info.evansweb.spring.examples.flash.FlashDecrementer">
    <property name="flash" ref="flash" />
  </bean>
```

and in the servlet xml file:

```xml
  <bean id="handlerMapping"
    class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping">
    <property name="interceptors">
      <list>
        <!-- This line makes sure the flash gets decremented
          after every request -->
        <ref bean="flashDecrementer" />
      </list>
    </property>
  </bean>

  <bean
    class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/jsp/" />
    <property name="suffix" value=".jsp" />
    <property name="viewClass"
      value="org.springframework.web.servlet.view.JstlView" />
    <property name="attributes">
      <map>
        <!-- This is the line that makes the flash object available in
          every view -->
        <entry key="flash" value-ref="flash" />
      </map>
    </property>
  </bean>
```

Now, it's really easy to add a message to the flash from your controller. First you make sure the flash object is available:

```java
  @Autowired
  private Flash flash;
```

Then in a controller method you just add your message:

```java
  @RequestMapping("/login.do")
  public ModelAndView login() {
    // Do your login stuff here...
    flash.setNotice("Welcome back!");

    ModelAndView mav = new ModelAndView("redirect:/home.do");
    return mav;
  }
```

And in your views you just include a simple flash.jsp file containing something like this:

```xml
<c:if test="${flash.error != null}"></c:if>
  <div class="error" id="error">${flash.error}</div>
</c:if>
<c:if test="${flash.notice != null}">
  <div class="notice" id="notice">${flash.notice}</div>
</c:if>
```

I've built an example web application and packaged it up. Once unzipped you can run it straight away with "mvn jetty:run" if you have maven2 installed. Here's the zipfile (only 13k!):
<a href="{{ site.baseurl }}/files/spring-flash-example.zip" title="spring-flash-example.zip">spring-flash-example.zip</a>

Finally a shameless plug. I quit my full-time job at the end of November 2007 in order to become a freelance developer. I'm starting a new software development business with my good friends Surjan Basan and Simon Hutchinson. Please feel free to get in touch if you need any Java, Ruby on Rails or .Net expertise.

If you want to make any comments, please return to [the original blog post]({{ site.baseurl }}{% post_url 2007-12-13-rails-like-flash-in-spring %}).