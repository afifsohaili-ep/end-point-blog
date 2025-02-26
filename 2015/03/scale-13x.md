---
author: Jacob Minshall
title: SCaLE 13x
github_issue_number: 1096
tags:
- chef
- conference
- containers
- open-source
date: 2015-03-04
---

<img alt="SCaLE Penguin" src="/blog/2015/03/scale-13x/image-0.png" title=""/>

I recently went to the [Southern California Linux Expo](http://www.socallinuxexpo.org) (SCaLE). It takes place in Los Angeles at the Hilton, and is four days of talks, classes, and more, all focusing around Linux. SCaLE is the largest volunteer run open source conference. The volunteers put a lot of work into the conference, from the nearly flawless wireless network to the AV team making it as easy as plugging in a computer to start a presentation.

One large focus of the conference was the growing [DevOps](https://en.wikipedia.org/wiki/DevOps) community in the Linux world. The more DevOps related talks drew the biggest crowds, and there was even a DevOps focused room on Friday. There are a wide range of DevOps related topics but the two that seemed to draw the largest crowds were configuration management and containerization. I decided to attend a full day talk on [Chef](https://www.chef.io/) (a configuration management solution) and [Docker](https://www.docker.com/) (the new rage in containerization).

The Thursday [Chef talk](http://www.socallinuxexpo.org/scale/13x/presentations/introduction-chef-testing-your-automation-code) was so full that they decided to do an extra session on Sunday. The talk was more of an interactive tutorial than a lecture, so everyone was provided with an [AWS](https://aws.amazon.com/) instance to use as their Chef playground. The talk started with the basics of creating a file, installing a package, and running a service. It was all very interactive; there would be a couple of slides explaining a feature and then there was time provided to try it out. During the talk there was a comment from someone about a possible bug in Chef, concerning the suid bit being reset after a change of owner or group to a file.  The presenter, who works for the company that creates Chef, wasn’t sure what would happen and said, “Try it out.” I did try it out, and there was a bug in Chef. The presenter suggested I file an issue on github, so I [did](https://github.com/chef/chef/issues/2951) and I even wrote a patch and made a [pull request](https://github.com/chef/chef/pull/2967) later on that weekend.

Containers were the other hot topic that weekend, with the half day class on Friday, and a few other talks throughout the weekend. The [Docker Talk](https://www.socallinuxexpo.org/scale/13x/presentations/introduction-docker-and-containers) was also set up in a learn by doing style. We learned the basics of downloading and running Docker images from the [Docker Hub](https://hub.docker.com/) through the command line. We added our own tweaks to the tops of those images and created new images of our own. The speaker, Jerome Petazzoni, usually gives a two or three day class on the subject, so he picked the parts he thought most interesting to share with us. I really enjoyed making a Docker File which describes the creation of a new machine from a base image. I also thought one of the use cases described for Docker to be very interesting, creating a development environment for employees at a company. There is usually some time wasted moving things from machine to machine, whether upgrading a personal machine or transferring a project from one employee to another, especially when they are using different operating systems. Docker can help to create a unified state for all development machines in a company to the point where setting a new employee up with a workspace can be accomplished in a matter of minutes. This also helps to bring the development environment closer to the production environment.

One sentiment I heard reiterated in multiple DevOps talks was the treatment of servers as Pets vs. Cattle. Previously servers were treated as pets. We gave servers names, we knew what they liked and didn’t like, when they got sick we’d nurse them back to health. This kind of treatment for servers is time consuming and not manageable at the scale that many companies face. The new trend is to treat servers like cattle. Each server is given a number, they do their job, and if they get sick they are “put down”. Tools like Docker and Chef make this possible, servers can be set up so quickly that there’s no reason to nurse them back to health anymore. This is great for large companies that need to manage thousands of servers, but it can save time for smaller companies as well.
