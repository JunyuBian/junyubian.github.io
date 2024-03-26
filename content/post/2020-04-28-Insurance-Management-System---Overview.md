---
layout: post
title: Insurance Management System - Overview
subtitle: Insurance Management System 
description: In this series of blogs, we will talk about how to build a Insurance Management web application together with database system.
excerpt: In this series of blogs, we will talk about how to build a Insurance Management web application together with database system.
date: 2020-04-28
author: Junyu
tags:
    - projects
    - web
    - tom-show
URL: "/2020/04/28/Insurance-Management-System---Overview/"
categories: [ Proj ]
---

In this series of blogs, we will talk about how to build a Insurance Management web application together with database system.

# Background

Tom's dad works in an insurance company. His work is to drop down who bought what kind of insurance, on which day does the customer receives an invoice, and on which day does the customer makes a payment. 

Oneday, Tom's dad talks to Tom: "Oh Tom, you see see you, one day day, only eat, do nothing, build a management system for me." Tom becomes not happy.

# Rlational Model

Tom's dad talks to Tom about what information is needed. After discussion, Tom draws the following relational model:![Relational Model](https://raw.githubusercontent.com/JYBian/BlogPic/master/截屏2020-04-09下午8.28.00.png)

# Summary of development environment

Tom thinks it over and over, finally decides to apply the following development environment: 

1. Programming language: Python3.5

2. Framework: Django2.1.1

3. Database: SQLite

4. Code editor: Pycharm

# Application Features

To build the application, Tom mainly used the ORM model characteristic provided by Django. With ORM, so that he can treat each table as a CLASS in python and each time he insert data into that table, he simply instantiate an object, together with Object-Oriented Programming, he can make queries, add items, change information and delete object in a convenient way.

The features of the application are but not restricted to:

## Normal Users

For users who are new to the application, he/she can register themselves in the REGISTER page. As shown below, the REGISTER page can be access by clicking the REGISTER button on the right of system bar.

![Registration Page](https://github.com/JYBian/BlogPic/raw/master/%E6%88%AA%E5%B1%8F2020-04-28%E4%B8%8B%E5%8D%888.08.13.png)

If information is filled not properly, application will generate warnings to helper users. When information filled in the correct way, user will be directed to the login page with notice of successful account creation.

![Login Page](https://github.com/JYBian/BlogPic/raw/master/%E6%88%AA%E5%B1%8F2020-04-28%E4%B8%8B%E5%8D%888.08.13.png)

After logging in, application will go to welcome page, where the username of user is confirmed again to make sure the user is about to purchase insurance. As long as the user has been logged in, the username and email will always be displayed on each page.

![Welcome Page](https://github.com/JYBian/BlogPic/raw/master/%E6%88%AA%E5%B1%8F2020-04-28%E4%B8%8B%E5%8D%888.19.43.png)

After confirmation, the user will be guided to the insurance purchase page, the first insurance is Home insurance, after which user is required to enter the information about home under insurance. When Home insurance purchase is finished, user is going to the Auto insurance purchase page, after which the information about vehicle under insurance needs to be provided, and finally the driver information is also needed. Notice the side bar, there are more detailed instruction about how to buy different kinds of insurance.

![Purchase Page](https://github.com/JYBian/BlogPic/raw/master/%E6%88%AA%E5%B1%8F2020-04-28%E4%B8%8B%E5%8D%889.23.05.png)

If the user want to check detailed information about the insurances purchased, he/she can click on the PROFILE button. In the PROFILE window, user can update email address if needed. And for each insurance listed, to check the detail information, just click on the insurance number will work.

![Profile Page](https://github.com/JYBian/BlogPic/raw/master/%E6%88%AA%E5%B1%8F2020-04-28%E4%B8%8B%E5%8D%889.29.35.png)

When finish browsing, user can click on LOGOUT to logout the account.

![Logout Page](https://github.com/JYBian/BlogPic/raw/master/%E6%88%AA%E5%B1%8F2020-04-28%E4%B8%8B%E5%8D%889.32.17.png)

## Super User

For users with administration power, they can go to 127.0.0.1:8000/admin/ to access the administrative page.

![Login Page for Admin](https://github.com/JYBian/BlogPic/raw/master/%E6%88%AA%E5%B1%8F2020-04-28%E4%B8%8B%E5%8D%889.44.37.png)

After logging in, Tom can manage all stored data, including add invoice and payment information for different users. (Notice that users pay their bill in other sites, this site is just designed for users to choose insurance and look for records.)

![Adding Invocie Page](https://github.com/JYBian/BlogPic/raw/master/%E6%88%AA%E5%B1%8F2020-04-28%E4%B8%8B%E5%8D%889.47.26.png)

# Project Outcome

In this project, Tom designed and built a web-based database application. There are three fields Tom have outcomes:

1. web development
2. database development
3. connection between web development and database development

For the web development, Tom chose to use python as programming language and django as web framework. This combination guaranteed us a good view of Object Oriented Programming experience. All the users and each recorded were created as an object from CLASS Tom defined.

Django is a MVT like frame, therefore, during web development, it is important to get clear of which page Tom are working on, which html Tom want to return and which template is required by django.

For database, Tom used the simple but powerful SQLite to perform its duty. Together with Pycharm, Tom can clearly see the structure of our project and database, in addition to manage through admin page, Tom can also open the SQLite database with Navicat or other database management software to easily manage our SQL.

The connection between database and web application is established by the ORM character of django, Tom can use OOP procedure to create and manage different records. But Tom also need to be clear about the foreign key relationship between different tables, each time Tom create or delete a record, Tom need to guarantee its foreign key (if any) is assigned. This gives us a good taste of how database is used in reality.

Tom is happy now.