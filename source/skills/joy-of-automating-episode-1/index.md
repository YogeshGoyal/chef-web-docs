---
title: 'Episode 1: Scripts to Recipes with Tomcat on CentOS 7'
description: 'Converting the application installation and configuration instructions into tested recipes. In this episode we initially install Tomcat onto CentOS 7.'
order: 1
keywords: training, videos, screencasts
category: 'joy-of-automating'
layout: skills-topic
sections: []
icon: video.png
---

<iframe width="877" height="493" src="https://www.youtube.com/embed/FOYc_SGWE-0?list=PL11cZfNdwNyORJfIYA8t07PRMchyDXIjq" frameborder="0" allowfullscreen></iframe>
<p/>

## Activity

In this episode we focus on taking the manual installation instructions found in [this tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-8-on-centos-7) and create a recipe that does the work for us.

* [How to Install Apache Tomcat 8 on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-8-on-centos-7)

## Resources

* [chef (executable)](https://docs.chef.io/ctl_chef.html): [generate cookbook](https://docs.chef.io/ctl_chef.html#chef-generate-cookbook) and [generate template](https://docs.chef.io/ctl_chef.html#chef-generate-template)
* [kitchen (executable)](https://docs.chef.io/ctl_kitchen.html): [destroy](https://docs.chef.io/ctl_kitchen.html#kitchen-destroy); [create](https://docs.chef.io/ctl_kitchen.html#kitchen-create); and [verify](https://docs.chef.io/ctl_kitchen.html#kitchen-verify)
* [Test Kitchen Configuration File](https://docs.chef.io/config_yml_kitchen.html)
* [Vagrant](https://docs.chef.io/plugin_kitchen_vagrant.html) and [Virtual Box](https://www.vagrantup.com/docs/virtualbox/)
* [Atom commands](http://flight-manual.atom.io/): [Fuzzy Find](http://flight-manual.atom.io/getting-started/sections/atom-basics/) and [Toggle Tree View](http://flight-manual.atom.io/getting-started/sections/atom-basics/)
* [Linux commands](http://www.mediacollege.com/linux/command/linux-command.html): [rm](http://www.mediacollege.com/cgi-bin/man/page.cgi?topic=rm); [cd](http://www.rapidtables.com/code/linux/cd.htm); [tree](http://www.computerhope.com/unix/tree.htm); [useradd](http://www.mediacollege.com/cgi-bin/man/page.cgi?topic=useradd); [chgrp](http://www.mediacollege.com/cgi-bin/man/page.cgi?topic=chgrp); [chmod](http://www.mediacollege.com/cgi-bin/man/page.cgi?topic=chmod)
* [Chef Resources](https://docs.chef.io/resources.html): [package](https://docs.chef.io/resource_package.html); [execute](https://docs.chef.io/resource_execute.html); [user](https://docs.chef.io/resource_user.html); [group](https://docs.chef.io/resource_group.html); [remote_file](https://docs.chef.io/resource_remote_file.html); [directory](https://docs.chef.io/resource_directory.html); [template](https://docs.chef.io/resource_template.html); and [service](https://docs.chef.io/resource_service.html)
* [ServerSpec](http://serverspec.org/): [command](http://serverspec.org/resource_types.html#command); [user](http://serverspec.org/resource_types.html#user); [group](http://serverspec.org/resource_types.html#group); and [file](http://serverspec.org/resource_types.html#file)
* [Unix Permissions Calculator](http://permissions-calculator.org/)
* Ruby: [Array](http://www.rubydoc.info/stdlib/core/2.1.6/Array); [The each method or Enumerator](http://www.rubydoc.info/stdlib/core/2.1.6/Enumerator); and [String Interpolation](https://en.wikibooks.org/wiki/Ruby_Programming/Syntax/Literals#Interpolation)

## Further activities

When you are done with the initial implementation we encourage you to challenge yourself by:

### Refactoring to attributes

It is common to want to make certain values configurable within a cookbook. To do that we often refactor hard-coded values into attributes. While we do not have requirements driving us to change the code this is a good time to practice this technique.

In the episode we extracted the version number into a [node attribute](https://docs.chef.io/attributes.html#attribute-files). Find other values within the recipe that you may want to define as node attributes.

### Desired state

When we use Test Kitchen to converge our test instance we are continually left with a few resources that are constantly taking action. This is inefficient if the system is already in the desired state. It is also noisy as they are constantly being reported in the output.

One way we can counter these 'wasteful' resources is through [resource guards](https://docs.chef.io/resources.html#guards). These guards allow you to define additional tests that are executed before the a resource takes action. Find a resource within the recipe that could implement a guard statement to stop it from executing. Then define that guard with the correct command to execute.

Another way is through [resource notifications](https://docs.chef.io/resources.html#notifications). When a resource defines a notification it will contact that resource when it takes action. This allows you to step up an "If This Then That" (IFTTT) chain of events. Find two resources within the recipe that appear dependent on one another. If one resource takes action then this other resource should take action. Then define a notification in the first resource to contact the second resource.