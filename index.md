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

Loren ipsums 

# Developer guide 

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

## Directory structure

The top-level directory structure contains:

```
app/        # holds the Meteor application sources
config/     # holds configuration files, such as settings.development.json
.gitignore  # don't commit IntelliJ project files, node_modules, and settings.production.json
```

This structure separates configuration files (such as the settings files) in the config/ directory from the actual Meteor application in the app/ directory.

The app/ directory has this top-level structure:

```
client/
  lib/           
  head.html      # the <head>
  main.js        # import all the client-side html and js files (important if creating or deleting any directories)

imports/
  api/           # Define collection processing code (client + server side)
    base/        # BaseCollection is an abstract superclass of all RadGrad data model entities.
    interest/    # Represents a specific interest, such as "Software Engineering".
    profile/     # Profiles provide portfolio data for a user.
    user_accepted_listings/
  startup/       # Define code to run when system starts up (client-only, server-only)
    client/      # Contains the router and user account-configuration.js page to link other pages
    server/      # Initializes the database and publish the interest and profiles.
  ui/
    components/  # templates that appear inside a page template.
    layouts/     # Layouts contain common elements to all pages (i.e. menubar and footer)
    pages/       # Pages are navigated to by FlowRouter routes.
    stylesheets/ # CSS customizations, if any.

node_modules/    # managed by Meteor

private/
  database/      # holds the JSON file used to initialize the database on startup.

public/          
  images/        # holds static images for the website
  
server/
   main.js       # import all the server-side js files.
```

### Import conventions

This system adheres to the Meteor 1.4 guideline of putting all application code in the imports/ directory, and using client/main.js and server/main.js to import the code appropriate for the client and server in an appropriate order.

This system accomplishes client and server-side importing in a different manner than most Meteor sample applications. In this system, every imports/ subdirectory containing any JavaScript or HTML files has a top-level index.js file that is responsible for importing all files in its associated directory.   

Then, client/main.js and server/main.js are responsible for importing all the directories containing code they need. For example, here is the contents of client/main.js:

```
import '/imports/startup/client';
import '/imports/ui/components/form-controls';
import '/imports/ui/components/directory';
import '/imports/ui/components/user';
import '/imports/ui/components/landing';
import '/imports/ui/layouts/directory';
import '/imports/ui/layouts/landing';
import '/imports/ui/layouts/shared';
import '/imports/ui/layouts/user';
import '/imports/ui/pages/directory';
import '/imports/ui/pages/filter';
import '/imports/ui/pages/landing';
import '/imports/ui/pages/listing';
import '/imports/ui/pages/mylistings';
import '/imports/ui/pages/user';
import '/imports/ui/pages/edit';
import '/imports/ui/stylesheets/style.css';
import '/imports/api/base';
import '/imports/api/profile';
import '/imports/api/interest';
import '/imports/api/user_accepted_listings';
```

Apart from the last line that imports style.css directly, the other lines all invoke the index.js file in the specified directory.

We use this approach to make it simpler to understand what code is loaded and in what order, and to simplify debugging when some code or templates do not appear to be loaded.  In our approach, there are only two places to look for top-level imports: the main.js files in client/ and server/, and the index.js files in import subdirectories. In those subdirectories, they usually will contain any html, CSS and JavaScript files that the subdirectories will use. 

Note that this two-level import structure ensures that all code and templates are loaded, but does not ensure that the symbols needed in each file are accessible.  So, for example, a symbol bound to a collection still needs to be imported into any file that references it. 
 
### Naming conventions

This system adopts the following naming conventions:

  * Files and directories are named in all lowercase, with words separated by hyphens. Example: accounts-config.js
  * "Global" JavaScript variables (such as collections) are capitalized. Example: Profiles.
  * Other JavaScript variables are camel-case. Example: collectionList.
  * Templates representing pages are capitalized, with words separated by underscores. Example: Directory_Page. The files for this template are lower case, with hyphens rather than underscore. Example: directory-page.html, directory-page.js.
  * Routes to pages are named the same as their corresponding page. Example: Directory_Page.

### Data model

The BowFolios data model is implemented by two Javascript classes: [ProfileCollection](https://github.com/manoa-rides/manoa-rides/tree/master/app/imports/api/profile) this class encapsulates a MongoDB collection with the same name and export a single variable Profiles that provides access to that collection. 


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


## Community Feedback

