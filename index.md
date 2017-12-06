[Check out the App](https://manoa-rides.meteorapp.com)

[Check out our GitHub](https://github.com/manoa-rides)

# Table of contents

* [Overview of Manoa Rides](#about-manoa-rides)
* [User Guide](#user-guide)
* [Developer Guide](#user-guide)
 * [Installation](#installation)
  * [Branches](#branches)
  * [Meteor Website](#meteor-website)
 * [Application design](#application-design)
   * [Directory structure](#directory-structure)
   * [Import conventions](#import-conventions)
   * [Naming conventions](#naming-conventions)
   * [Data model](#data-model)
   * [CSS](#css)
   * [Routing](#routing)
   * [Authentication](#authentication)
   * [Authorization](#authorization)
   * [Configuration](#configuration)
   * [Redeploy Meteor](#redeploy-meteor)
   * [Quality Assurance](#quality-assurance)
     * [ESLint](#eslint)
* [Development history](#development-history)
  * [Initial Mockup Pages](#initial-mockup-pages)
  * [Milestone 1: Mockup development](#milestone-1-mockup-development)
  * [Milestone 2](#milestone-2)
* [Community Feedback](#community-feedback)


# About Manoa Rides 

## What's Manoa Carpool all about?
### Carpooling solves two problems

Commuting is expensive and parking is rare. With Manoa Carpool everybody wins.

### Get there quicker with the carpool lane

With fewer cars clogging the roads and the HOV lane, we all get there faster.

### Make connections

Make friends while you travel.


## Enter Manoa Carpool
### Connect with Drivers and Riders

After creating a Manoa Carpool profile, search for Riders or Drivers in your vicinity commuting to the University of Hawaii

### Filter to find the perfect riding companion

Search the Manoa Carpool directory and filter individuals by interests, driving skill, distance, and classes.

### Make connections

Make friends while you travel.

![](images/profile-mockup.png)

![](images/filterpage.png)

![](images/schedule-mockup.png)


# Installation

First, [install Meteor](https://www.meteor.com/install).

Second, [download a copy of Manoa-Rides](https://github.com/manoa-rides/manoa-rides/archive/master.zip), or clone it using git.
  
Third, cd into the app/ directory and install libraries with:

```
$ meteor npm install
```

Fourth, run the system with:

```
$ meteor npm run start
```

If all goes well, the application will appear at [http://localhost:3000](http://localhost:3000). If you have an account on the UH test CAS server, you can login.  

# User Guide


### Branches

When creating a new branch for the project use issue-XX naming conventions. This way branches can be directly tied to the issue they correspond to. 

```
$ git checkout -b issue-XX
```

Make sure that master always has working code. 

To change branches:

```
$ git checkout [issue-XX or master]
```

Make sure to:

```
$ git pull
```

frequently from the master branch. This assures that you will have the most recent working code from other people. 


### Meteor Website

To use and make a meteor app website, first create an account on the [Galaxy website](https://galaxy.meteor.com/) After creating an account it will be costly to push any website onto galaxy so it's best to work with an organization that has limited slots but will be able to push your website for free. 

For more instructions, please at [E54: Test deploy to Galaxy](http://courses.ics.hawaii.edu/ics314s17/morea/deployment/experience-test-deployment.html)

# Development History

The development process for Manoa-Rides

## Milestone 1: Mockup development

This milestone started on November 14, 2017 and ended on November 22, 2017.

For milestone 1 the goal was to get mockups off all the page we wanted, and get an idea of what the completed application would look like.  

Mockups for the following four pages were implemented during M1:

<img width="200px" src="images/schedule-mockup.png"/>
<img width="200px" src="images/profile-mockup.png"/>
<img width="200px" src="images/directory.png"/>
<img width="200px" src="images/filterpage.png"/>

Milestone 1 was implemented as [Manoa-Rides GitHub Milestone M1](https://github.com/manoa-rides/manoa-rides/milestones):

![](images/m1-milestone.png)


Milestone 1 consisted of nine issues, and progress was managed via the [Manoa-Rides GitHub Project M1](https://github.com/manoa-rides/manoa-rides/projects/1):

![](images/m1-project.png)

Each issue was implemented in its own branch, and merged into master when completed:

![](images/m1-branch-graph.png)

Milestone 2 will focus on the back-end design to facilitate meaningful interaction between drivers and riders of Manoa. Integration of Google Calendars into our own application as well as long term scheduling between users is our main focus for features in Milestone 2. Milestone 2 can be found via [Manoa-Rides Github Project M2](https://github.com/manoa-rides/manoa-rides/projects/2)


## Initial User Study

