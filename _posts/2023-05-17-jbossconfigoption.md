---
layout: post
title: Jboss EAP Configuration options 
categories: [Blog]
tags: [web, dev, jboss, config, cli]
date:   2023-05-17

---
In my last project I was able to dive in Jboss EAP 7.4. 
And I was really impressed by the possibilities about configurating the server. 
generally you have several options to configure a jboss applicationserver.

* WEB UI : Management Console (available ``host:9990/console/index.html``)
* Jboss CLI (available  ``BOSS_HOME/bin/jboss-cli.sh``)
* JBoss CLI Gui (available ``BOSS_HOME/bin/jboss-cli.sh --gui``)

The CLI itself can even contain conditional statements and execute another script files. so it is really powerful! Embrace it! it will pay out. 
For example the command "take-snapshot" it persists the runtime config of the server as xml. Many times I had to find out, where the difference is. This helped me a lot. 

Anything to disagree or argue with me? just twitter me @BiegelAndre #ConfigJBoss

## Sources:
* https://www.mastertheboss.com/jbossas/jboss-script/use-conditional-statements-in-wildfly-cli/
* https://access.redhat.com/documentation/de-de/jboss_enterprise_application_platform/6.2/html/administration_and_configuration_guide/use_the_management_cli_in_batch_mode1
* https://developer.jboss.org/docs/DOC-16728
* https://access.redhat.com/documentation/de-de/jboss_enterprise_application_platform/6.2/html/administration_and_configuration_guide/save_a_configuration_snapshot_using_the_management_cli

