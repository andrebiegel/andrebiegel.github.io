---
layout: post
title: Building Reverse Proxies / Gateways
categories: [Projects]
tags: [infrastructure, configuration , httpd , modules, mod_substitute , mod_proxy_html, mod_proxy]
date:   2019-10-02
github_url: https://github.com/andrebiegel/apache-reverse-proxies

---

This Project examines the possibilities to create a reverse proxy with Apache HTTPD. It clearly shows which modules need to used.

Furthermore it shows how to tackle commons issues with referencing resources (absolute urls etc)

* App 1 shows how links should be done
* App 2 shows problems with having absolute path definitions like /images/image.jpg
* App 3 shows problems with having absolute url definitions like http://app3/images/image.jpg
* App 4 shows problems with having absolute path definitions in css  (inline  & external )
* App 5  shows how web compomnents can be handled in this usecase. furthermore it tries to show a solution to provide configuration in frontend development




You can find the source code for the Projekt at GitHub:
[andrebiegel](https://github.com/andrebiegel) / [apache-reverse-proxies](https://github.com/andrebiegel/apache-reverse-proxies)


