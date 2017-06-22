---
layout: default
title: Infrastructure from Code
date: 2017-05-09 22:25:00
---


# [Infrastructure from Code](https://www.pluralsight.com/courses/infrastructure-code-big-picture)

## Prerequisites/Overview

## The Pipeline

- The workflow of moving a project through stages of work.
<br>- The Saving to Business and Customers
<br>- Change and release management&nbsp;
<br>- Improved security
<br>- Reduced recovery at time&nbsp;

### The Configuration

- Read by an automation process
<br>- Contains configuration properties
<br>- Imperative - How to do
<br>- Declarative - What you want

### The Components of Pipeline (Stages)

1. ### [Source](#Stage-1:-Source)

2. ### [Build](#Stage-2:-Build)

3. ### [Test](#Stage-3:-Test)

4. ### [Release](#Stage-4:-Release)

### Push/Pull Target Delivery

- #### Push

&nbsp; - Best for testing
<br>&nbsp; - Great production solution&nbsp;

- #### Pull

&nbsp; - Great production solution

### Continuous Configuration Automation (CCA) Tools

- Referred to as the DevOps Toolchain
<br>- Tools that automate and orchestrate
<br>- May be specific to a platform
<br>- Need to meet your security and compliance needs
<br>- Needs to scale

### A New View of "Failure"

- Due to inconsistence procedures, lack of automation, lack of change control - IT Ops managers are slow to make change because of failure.
<br>- Infrastructure from Code provides a reliable, repeatable process that can learn
<br>- Rush to failure!

## Stage 1: Source

- ### Defining What is "Source"

&nbsp; - Not just code - the supported files needed for applications and infrastructure
<br>&nbsp; - Source Control - Storing code and documentation charges&nbsp;
<br>&nbsp; - Examples: GitHub, Apache Subversion, GitLab, Microsoft Visual Studio Team Foundation Server

- ### Version Control

&nbsp; - Much better than just a file share
<br>&nbsp; - Tracks changes, conflict resolution and maintains a history of changes from beginning to production
<br>&nbsp; - Identifies "Who" made a change and "When"
<br>&nbsp; - Supports multiple team members and can identify and resolve conflicts

- ### Code Review

&nbsp; - Prior to Check-in or commit
<br>&nbsp; - Checks code for best practices
<br>&nbsp; - Can be manual, but automated is best
<br>&nbsp; - Assures that code is maintainable
<br>&nbsp; - Can be done during test phase - also known as listing

## Stage 2: Build

## Stage 3: Test

## Stage 4: Release