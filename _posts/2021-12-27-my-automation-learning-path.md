---
layout: post
title: My 2021 Learning Path to Network Automation
description: 
image: /post-images/net-automation-books.jpg
comments: True
tags: automation learning
---

![net-automation-books](/post-images/net-automation-books.jpg)

Like many of my fellow network engineers, automation was top of the list of topics to learn for this year. A goal that I had continued to put off in previous years. But for me, this time was going to be different because I realized that I needed to put into practice what I was learning, otherwise it was going to get lost. My problem all along was that I didn't know where to start. I'd participated in a handful of DevNet labs at CiscoLive and other local events that would mostly target greenfield deployments. I'd read documentation on different product APIs. I'd watch YouTube videos and read networktocode blogs. And yet, I wasn't any closer to solving any of the problems at work that could benefit from an automated approach.

So I started using GitHub. Every configuration change I was designing, planning, and implementing would go into .md or .txt files (and .ios if you are familiar with the Cisco IOS extension on VS Code). I knew git is the most popular Version Control tool, and I knew engineers across the industry were using it to share code and integrating them into configuration pipelines. And I needed to learn how to use it even if the content of my repositories wasn't real code. This practice made me very comfortable with git push/pull, commits, and branches.

Then, I found a book that provided me with the blueprint I so much needed to get started with code, John Capobianco's [Automate Your Network](https://smile.amazon.com/Automate-Your-Network-Introducing-Enterprise-ebook/dp/B07PKDNL78).

I read John's book in 3 days! 

I didn't stop to test the code, I didn't install any libraries, I just read. I know network platforms and commands, I wanted to know how to use code to access data and make changes. I found his book to be really good at setting out a good automation strategy for the enterprise team and then hands-on code with very good explanations of what they did from there on.

![camping-movie](/post-images/campsite-movie.jpg)
*While the gang was enjoying Jurassic World I was head down reading John's book*


## The Book
The book showcases Ansible and how to use it to manage and operate Cisco IOS and NXOS devices.

I learned the folder structure I needed for my code. I learned that there were certain "modules" included on Ansible by default, such as what I needed, NXOS. I learned the file structure for an inventory file - which lists the target devices you want to apply config changes to. I learned how to group single device configs vs. group device configs. I learned how to format a playbook! what are tasks! 

This book had a solution to the problem I had, how to get started!

## Hands-on

When I got back to the office I started to test some of the code from the book. After researching that Ansible offered modules for all the solutions I supported (NXOS, ACI, MSO, NSX-T) I decided to get my hands dirty.

1. I created a Github repo for every product I supported.
   * The goal was to publish the folder structure from John's book across all of the repos. It turned out that they don't all require things like group_vars, especially when working against orchestrator products like MSO. But this was part of the learning experience.
2. I installed Ansible.
   * Downloaded ansible-galaxy collections for the products that required it (e.g. MSO, NSX-T).
3. I started a playbook to display ANY data from the products.
   * Login to the environment.
   * Get list of networks. All, any, or just one. 
4. I presented my little demo to my team.

## Getting the team involved

I implemented a NetDevOps Dojo at work. Every Monday 12-2pm we have a learning session. Attendance is not mandatory, and all questions are welcomed. Everything and anything network automation related is in scope. I designed the session to have the team share code they've been working on, have presenters from other teams that are using automation/orchestration, do code reviews, build code together, if anyone is not sure how to use a piece of code to implement a network change we build and write the implementation plan or variables files together.

There's a Teams channel to share information, training, and resources. If I finish writing a neat piece of code, I share it, others see it and try it out, and we can review it at the next dojo as a team.

Our leadership team is very encouraging when it comes to automation so their support is greatly appreciated when it's time to schedule training and have engineers attend courses, like Kirk Byers's Netmiko or Nornir ones.

The practice of meeting periodically and offering this hands-on experience has been very well received - so much so that the team has voted to keep it going into the next year.


## Starting small and growing up

Although I admire the Cisco DevNet program, I often find their resources for DC infra to be too basic, targetting simple greenfield deployments. Take ACI as an example, API interactions for Fabric components are almost non-existent (if you feel differently, share the resource on the comment section) and it's probably one of the components I intereact with the most as I grow the network.

So my first ACI project was to build an Interface Profile followed by how to add the it to a Switch Profile. I started with a simple small config change, create an interface profile - no configs, no interfaces, no policy. Then I built those functionalities in. But starting with the simplest config was essential to gaining momentum and building the rest. It provided me with the opportunity to get to understand how the Ansible modules were written and how they interacted with the ACI controllers.

And now if a customer needs to deploy a new server to the data center, our engineers can run a playbook that configures the fabric with the new physical requirements. 4 interfaces, 10G, in a port-channel for switches 1 and 2? We got chu.

Since this effort started, we've automated new Switch deployments, new network builds, new infra adds to exisiting networks, backups, etc.

We are able to build automated plays for known customers. If a Storage engineer were to deploy the same XIO hardware every 6 months, we'd know what the requirements are and could deploy the connectivity profile in a matter a seconds.

## What's next

The dream is a fully automated pipeline, the CI/CD dream pipe if you will. If that same Storage Eng has hardware in place they can submit a request that triggers the new config to be generated, tests against some lab infra, and pushes to non-prod and prod without the intervention of a Network Engineer.

So we gotta develop good guidelines for customers, test cases to try candidate configs against, and have reliable lab infrastructure to try the changes on first.

We will continue to study and learn how to improve our code and test cases.

The goal is to have repeatable tasks fully automated so we can focus on design and R&D to enable our customers with the best products we can offer. 

## Conclusion

I understand that not every enterprise offers their employees with the tools and the strategic freedom to get up and running with network automation. I'm very lucky in that regard. My advice if that is not the case is to get the buy from your manager, emphasize the cost benefit of automation in hours saved, the potential to reduce errors, increase network uptime, and enable your customers to have working solutions faster. Perhaps request a small set of resources to demonstrate a Proof of Concept.

Personally, I'm very happy with the growth I've made this year in the network automation space. I didn't know how to get started, then found a useful resource, identified a small project, shared my progress, built it up, and got others to join in on the fun.

I have yet so much to learn but getting started was the hardest part, the future doesn't seem too scary.

## Continuing Education

Other resources I used this summer to build my automation knowledge: 

1. Edelman, Lowe & Oswalt - [Network Programmability and Automation](https://smile.amazon.com/Network-Programmability-Automation-Next-Generation-Engineer/dp/1491931256)
   1. Excellent resource, well rounded. Teaches the basics of Python, Ansible, Github and other tools relevant to net automation.
2. Geerling - [Ansible for DevOps](https://smile.amazon.com/Ansible-DevOps-Server-configuration-management-ebook/dp/B08FBLVVFG)
   1. This is a great book to learn the ins and outs of Ansible. The author is really good at explaining what each line of Ansible does.

If you're a woman, John's announced he's giving his book away until the end of 2022 for free, just email him. See his [Tweet](https://twitter.com/John_Capobianco/status/1473782314526195718) for the announcement. Recently he mentioned already given out 1000+ copies of his book in just the first weekend.


