# Chapter 1: AEM Introduction

## What is AEM?

**Adobe Experience Manager (AEM)** is an enterprise-level **Content Management System (CMS)** developed by Adobe.

A CMS allows users to create, edit, manage, and publish digital content without writing code for every page.

Examples of content managed in AEM:

* Web pages
* Images
* PDFs
* Videos
* Content Fragments
* Experience Fragments
* Product information

---

## Why do companies use AEM?

Imagine a news website with 10,000 articles.

Without AEM:

* Developers create every page manually.
* Every content update requires deployment.
* High maintenance cost.

With AEM:

* Authors edit content using a browser.
* Developers build reusable components.
* Publishing takes seconds.
* No deployment is needed for content changes.

This separation lets developers focus on features while content authors manage website content independently.

---

# AEM Architecture

```text
          Author

      Content Authors
             │
             ▼
      Author Instance
             │
      Replication
             │
             ▼
     Publish Instance
             │
             ▼
        Dispatcher
             │
             ▼
          End Users
```

### Author Instance

Used by:

* Content Authors
* Developers
* Administrators

Purpose:

* Create pages
* Edit pages
* Upload assets
* Manage workflows

---

### Publish Instance

Purpose:

* Serves content to website visitors.
* Content is read-only.
* Optimized for speed and security.

---

### Dispatcher

Dispatcher is:

* Cache server
* Load balancer
* Security layer

Benefits:

* Faster page loading
* Reduced server load
* Protection against unwanted requests

---

# What is a CMS?

CMS stands for **Content Management System**.

It helps manage digital content.

Examples:

* WordPress
* Drupal
* Joomla
* Sitecore
* Adobe Experience Manager

---

# Why is AEM considered enterprise software?

Because it supports:

* Multi-language websites
* Multi-country websites
* Millions of pages
* Workflow automation
* User permissions
* Digital Asset Management (DAM)
* Headless CMS
* Cloud deployment
* Adobe Marketing Cloud integration

---

# AEM Technical Stack

```text
Browser
   │
HTML
HTL
JavaScript
CSS
   │
Apache Sling
   │
OSGi
   │
Java
   │
JCR Repository
(Jackrabbit Oak)
```

Each layer has a different responsibility:

* **HTL** renders the UI.
* **Apache Sling** maps requests to resources.
* **OSGi** manages services and components.
* **Java** contains business logic.
* **JCR/Oak** stores content.

---

# Common AEM Modules

* **AEM Sites** – Website creation
* **AEM Assets** – Digital asset management
* **AEM Forms** – Forms and document workflows
* **AEM Headless** – Content APIs
* **AEM Cloud Service** – Cloud-native deployment

---

# AEM Developer Responsibilities

Frontend:

* HTML
* CSS
* JavaScript
* HTL
* Client Libraries

Backend:

* Java
* Sling Models
* Servlets
* OSGi Services
* Workflows
* Event Handlers

---

# Sample Project Structure

```text
my-project

core/
    Java Code

ui.apps/
    Components
    Dialogs
    Templates

ui.content/
    Sample Content

ui.config/
    OSGi Configurations

frontend/
    CSS
    JS

all/
    Deployment Package
```

---

# Simple Sling Model Example

```java
package com.mysite.core.models;

import org.apache.sling.models.annotations.Model;
import org.apache.sling.api.resource.Resource;

@Model(adaptables = Resource.class)
public class WelcomeModel {

    public String getMessage() {
        return "Welcome to AEM";
    }
}
```

### Explanation

* `@Model` registers the class as a Sling Model.
* `adaptables = Resource.class` means the model adapts from a JCR resource.
* `getMessage()` returns data that HTL can display.

---

# HTL Example

```html
<div data-sly-use.model="com.mysite.core.models.WelcomeModel">
    <h1>${model.message}</h1>
</div>
```

### Explanation

* `data-sly-use.model` creates an instance of the Sling Model.
* `${model.message}` calls `getMessage()` automatically.

Output:

```html
<h1>Welcome to AEM</h1>
```

---

# Interview Questions

**1. What is AEM?**

* Adobe Experience Manager is an enterprise Content Management System used to build, manage, and deliver digital experiences.

**2. What is the difference between Author and Publish?**

* Author is used for creating and editing content.
* Publish is used to serve content to end users.

**3. What is Dispatcher?**

* A caching, load balancing, and security layer that sits in front of the Publish instance.

**4. Why is AEM preferred over WordPress?**

* Better scalability, enterprise security, reusable components, workflow support, multi-site management, cloud integration, and Adobe ecosystem support.

---

#  2: AEM Installation & Project Setup

## Prerequisites

Before installing AEM, you need:

| Software                | Version  | Purpose                |
| ----------------------- | -------- | ---------------------- |
| Java JDK                | 11 or 17 | Runs AEM               |
| Apache Maven            | 3.8+     | Build tool             |
| Git                     | Latest   | Source code management |
| IntelliJ IDEA / Eclipse | Latest   | Java development       |
| AEM SDK                 | Latest   | Local AEM server       |

---

# Step 1: Install Java

### Why Java?

AEM is completely written in Java.

The AEM Quickstart file (`aem-sdk-quickstart.jar`) is a Java executable JAR.

Check Java version:

```bash
java -version
```

Example output:

```text
openjdk version "11.0.20"
```

---

# Step 2: Install Maven

### What is Maven?

Maven is a build automation and dependency management tool.

It:

* Downloads libraries
* Compiles Java code
* Runs tests
* Creates packages
* Deploys to AEM

Check Maven version:

```bash
mvn -version
```

Example output:

```text
Apache Maven 3.9.x
Java version: 11
```

---

# Why does AEM use Maven?

Without Maven:

* You download every JAR manually.
* Dependency conflicts become common.

With Maven:

* Dependencies are downloaded automatically.
* Builds are reproducible.
* Deployment is simpler.

---

# Typical AEM Project Structure

```text
my-site/

├── core/
│   └── Java code
│
├── ui.apps/
│   └── Components
│
├── ui.content/
│   └── Sample content
│
├── ui.config/
│   └── OSGi configs
│
├── frontend/
│   └── CSS & JS
│
├── all/
│   └── Deployment package
│
└── pom.xml
```

### Folder Explanation

### core

Contains Java code:

* Sling Models
* Servlets
* OSGi Services
* Workflows

---

### ui.apps

Contains:

* Components
* Dialogs
* Templates
* Client Libraries

---

### ui.content

Contains:

* Sample pages
* Content
* DAM assets

---

### ui.config

Contains:

* OSGi configurations
* Scheduler configs
* Service configs

---

### frontend

Contains:

* CSS
* JavaScript
* TypeScript (optional)

---

### all

Combines all modules into one installable package.

---

# Understanding `pom.xml`

`pom.xml` (Project Object Model) is Maven's main configuration file.

Example:

```xml
<project>

    <groupId>com.company</groupId>

    <artifactId>mysite</artifactId>

    <version>1.0.0</version>

    <packaging>pom</packaging>

</project>
```

### Important Tags

**groupId**

Usually:

```text
com.company.project
```

Example:

```text
com.adobe.training
```

---

**artifactId**

Project name.

Example:

```text
wknd
```

---

**version**

Current project version.

```text
1.0.0
```

---

**packaging**

Usually:

```text
pom
```

for the parent project.

---

# Creating a New AEM Project

Use the Maven Archetype:

```bash
mvn -B archetype:generate \
-D archetypeGroupId=com.adobe.aem \
-D archetypeArtifactId=aem-project-archetype \
-D archetypeVersion=41 \
-D appTitle="My Site" \
-D appId="mysite" \
-D groupId="com.mysite"
```

### Parameters

* `appTitle` → Website title
* `appId` → Project ID
* `groupId` → Java package root
* `archetypeVersion` → Version of the AEM project template

---

# Building the Project

Navigate to the project directory:

```bash
cd mysite
```

Build:

```bash
mvn clean install
```

### What happens?

1. Deletes old build files.
2. Compiles Java code.
3. Packages modules.
4. Creates ZIP packages.
5. Builds the final deployment package.

---

# Deploy to Author

```bash
mvn clean install -PautoInstallPackage
```

Deploys the full project to the Author instance (default: `localhost:4502`).

---

# Deploy to Publish

```bash
mvn clean install -PautoInstallPackagePublish
```

Deploys to the Publish instance (default: `localhost:4503`).

---

# Deploy Only Backend

```bash
mvn clean install -PautoInstallBundle
```

Deploys only the Java bundle.

---

# Starting AEM

### Author

Rename the JAR:

```text
aem-author-p4502.jar
```

Run:

```bash
java -jar aem-author-p4502.jar
```

---

### Publish

Rename:

```text
aem-publish-p4503.jar
```

Run:

```bash
java -jar aem-publish-p4503.jar
```

---

# AEM URLs

| URL                     | Purpose             |
| ----------------------- | ------------------- |
| `http://localhost:4502` | Author              |
| `http://localhost:4503` | Publish             |
| `/crx/de`               | Repository Explorer |
| `/system/console`       | OSGi Console        |
| `/crx/packmgr`          | Package Manager     |
| `/sites.html`           | Sites Console       |
| `/assets.html`          | DAM Console         |

---

# Build Flow

```text
Developer
     │
     ▼
Java + HTL + XML
     │
     ▼
Maven Build
     │
     ▼
ZIP Package
     │
     ▼
Install on Author
     │
     ▼
Author Tests
     │
Replication
     │
     ▼
Publish
```

---

# Common Interview Questions

**Q1. What is Maven?**
A build automation and dependency management tool used to compile, package, and deploy AEM projects.

**Q2. What is `pom.xml`?**
The main Maven configuration file that defines project metadata, dependencies, plugins, and modules.

**Q3. What does `mvn clean install` do?**
It removes previous build artifacts, compiles the project, runs tests (if configured), packages the modules, and installs them into the local Maven repository.

**Q4. Difference between `-PautoInstallPackage` and `-PautoInstallBundle`?**

* `-PautoInstallPackage`: Deploys the complete content package (frontend + backend).
* `-PautoInstallBundle`: Deploys only the backend Java bundle.

---
#  3: AEM Consoles

## What is an AEM Console?

An **AEM Console** is a web-based administration interface used to create, manage, configure, and monitor content and services.

Think of it as a **control panel** for AEM.

---

# Main AEM Consoles

| Console             | URL                               | Purpose                      |
| ------------------- | --------------------------------- | ---------------------------- |
| Sites               | `/sites.html`                     | Manage website pages         |
| Assets              | `/assets.html`                    | Manage images, videos, PDFs  |
| CRXDE Lite          | `/crx/de`                         | View and edit JCR repository |
| Package Manager     | `/crx/packmgr`                    | Install/export packages      |
| OSGi Console        | `/system/console`                 | Manage bundles and services  |
| User Administration | `/security/users.html`            | Users and permissions        |
| Workflow Console    | `/libs/cq/workflow/admin/console` | Manage workflows             |
| Replication Console | `/etc/replication` (6.5)          | Replication agents           |

---

# 1. Sites Console

**URL**

```text
http://localhost:4502/sites.html
```

## Purpose

The Sites Console is where content authors create and manage website pages.

### Features

* Create pages
* Delete pages
* Move pages
* Copy pages
* Publish pages
* Unpublish pages
* Edit page properties
* Manage language copies

### Example Website Structure

```text
/content

   mysite

      en

         home

         about

         contact

      fr

      de
```

### Creating a New Page

1. Open **Sites**.
2. Select a folder.
3. Click **Create → Page**.
4. Choose a template.
5. Enter:

   * Title
   * Name
6. Click **Create**.

---

# 2. Assets Console (DAM)

**URL**

```text
http://localhost:4502/assets.html
```

## What is DAM?

DAM = **Digital Asset Management**.

It stores:

* Images
* PDFs
* Videos
* Word files
* Audio
* ZIP files

### Example

```text
DAM

Marketing

    banner.jpg

    logo.png

    brochure.pdf

Products

    mobile.jpg

    laptop.jpg
```

### Why DAM?

Without DAM:

* Images are scattered.

With DAM:

* Centralized storage.
* Version history.
* Metadata.
* Search support.
* Reuse across websites.

---

# 3. CRXDE Lite

**URL**

```text
http://localhost:4502/crx/de
```

## What is CRXDE Lite?

CRXDE Lite is AEM's repository browser.

Developers use it to:

* Create components
* Create templates
* View JCR nodes
* Edit dialogs
* Add properties
* Debug content

### Repository Structure

```text
/

apps

libs

content

conf

etc

var

home

oak:index
```

### Important Folders

#### `/apps`

Custom project code.

#### `/libs`

Adobe-provided code (do not modify).

#### `/content`

Website content.

#### `/conf`

Editable templates and policies.

#### `/etc`

Legacy configurations.

#### `/var`

Temporary data.

---

# Nodes in JCR

Everything is stored as a node.

Example:

```text
/content

   mysite

      home

         jcr:content

              title = Home

              sling:resourceType = mysite/components/page
```

---

# Property Types

Common JCR property types:

* String
* Boolean
* Long
* Double
* Date
* Binary
* Path
* Reference

---

# 4. Package Manager

**URL**

```text
http://localhost:4502/crx/packmgr
```

## Purpose

Packages are used to:

* Move code
* Move content
* Deploy projects
* Back up content

### Package Contains

```text
mysite.zip

apps/

content/

conf/

install/
```

### Common Actions

* Build
* Download
* Install
* Upload
* Delete
* Replicate

---

# 5. OSGi Web Console

**URL**

```text
http://localhost:4502/system/console
```

## Most Important Menus

### Bundles

Shows all installed Java bundles.

Example:

```text
Active

Resolved

Installed
```

### Components

Shows OSGi components.

### Configurations

Edit OSGi configuration values.

### Services

Lists all registered OSGi services.

### Sling

Contains:

* Servlet Resolver
* Script Resolver
* Eventing
* Scheduler

---

# 6. User Administration

**URL**

```text
http://localhost:4502/security/users.html
```

Used to:

* Create users
* Create groups
* Assign permissions
* Reset passwords

### Common Groups

* administrators
* authors
* workflow-users
* dam-users
* content-authors

---

# 7. Workflow Console

Used to:

* Create workflows
* Monitor workflows
* View workflow history
* Manage workflow models

### Example Workflow

```text
Author

↓

Upload Image

↓

Approval

↓

Publish

↓

Live Website
```

---

# 8. Replication Console

Replication transfers content from **Author** to **Publish**.

Flow:

```text
Author

↓

Replication Agent

↓

Publish

↓

Website
```

### Agent Settings

* Enabled
* Transport URL
* Username
* Password

---

# Daily Workflow of an AEM Developer

```text
Start AEM

↓

Open Sites

↓

Create/Edit Page

↓

Open CRXDE

↓

Create Component

↓

Write Sling Model

↓

Build Project

↓

Deploy

↓

Check Bundle

↓

Test Page

↓

Publish
```

---

# Real Project Example

Suppose you need to add a new **News Banner**.

1. Upload `banner.jpg` to **Assets**.
2. Create a **Banner Component** in `/apps`.
3. Add a dialog for title and image.
4. Build using Maven.
5. Install the package.
6. Drag the Banner Component onto the page in **Sites**.
7. Publish the page.

---

# Interview Questions

### 1. What is the Sites Console?

It is used by authors to create, edit, organize, and publish website pages.

### 2. What is DAM?

A centralized repository for managing digital assets like images, PDFs, videos, and documents.

### 3. Why is CRXDE Lite important?

It allows developers to inspect and modify the JCR repository, create components, and debug content structures.

### 4. Why should you avoid changing `/libs`?

Because Adobe owns `/libs`. Any changes can be overwritten during upgrades. Customizations should always be placed under `/apps`.

### 5. What is the purpose of Package Manager?

It packages, installs, exports, imports, and deploys AEM code and content.

### 6. What is the OSGi Console used for?

To manage bundles, services, components, and configurations in the AEM runtime.

---
#  4: AEM Project Structure

## What is an AEM Project?

An AEM project is a **Maven multi-module project** that separates Java code, components, content, configurations, and frontend assets into different modules.

This separation makes the project easier to maintain, test, and deploy.

---

# Typical AEM Project Structure

```text
myproject/

│── pom.xml                (Parent Maven project)

│
├── all/
│
├── core/
│
├── ui.apps/
│
├── ui.content/
│
├── ui.config/
│
├── ui.frontend/
│
└── dispatcher/
```

---

# Overall Architecture

```text
              Developer

                  │

                  ▼

        AEM Multi Module Project

      ┌────────────────────────┐
      │        core            │
      │     Java Classes       │
      └────────────────────────┘

                  │

      ┌────────────────────────┐
      │      ui.apps           │
      │ Components Dialogs     │
      └────────────────────────┘

                  │

      ┌────────────────────────┐
      │     ui.content         │
      │ Pages Assets Content   │
      └────────────────────────┘

                  │

      ┌────────────────────────┐
      │      ui.config         │
      │ OSGi Configurations    │
      └────────────────────────┘

                  │

      ┌────────────────────────┐
      │     ui.frontend        │
      │ CSS JS React Angular   │
      └────────────────────────┘

                  │

      ┌────────────────────────┐
      │         all            │
      │ Final Deployment ZIP   │
      └────────────────────────┘

                  │

               AEM Server
```

---

# Parent Module

```
pom.xml
```

The parent `pom.xml` controls the entire project.

Responsibilities:

* Defines project version
* Lists modules
* Manages dependencies
* Configures plugins
* Builds all modules together

Example:

```xml
<modules>

    <module>core</module>

    <module>ui.apps</module>

    <module>ui.content</module>

    <module>ui.config</module>

    <module>ui.frontend</module>

    <module>all</module>

</modules>
```

---

# Module 1: core

```
core/
```

## Purpose

Contains **Java backend code**.

Examples:

```
core

models

services

servlets

filters

listeners

workflow

scheduler

utils
```

Typical package structure:

```
com.company.project

models

services

servlets

filters
```

---

## Example Sling Model

```java
package com.company.project.models;

import org.apache.sling.models.annotations.Model;
import org.apache.sling.api.resource.Resource;

@Model(adaptables = Resource.class)
public class WelcomeModel {

    public String getTitle(){

        return "Welcome";

    }

}
```

Compiled output:

```
core.jar
```

---

# Module 2: ui.apps

```
ui.apps/
```

## Purpose

Contains everything related to the AEM user interface.

Example:

```
ui.apps

apps

company

components

page

title

image

dialog

clientlibs
```

Contains:

* Components
* Templates
* Dialogs
* Client Libraries
* HTL files
* CSS
* JavaScript

---

### Example Component

```
title

title.html

_title.xml

cq:dialog

clientlibs
```

---

# Module 3: ui.content

```
ui.content/
```

Purpose:

Contains sample content.

Example:

```
content

company

home

about

contact
```

Usually stores:

* Demo pages
* Sample assets
* Experience Fragments
* Content Fragments

---

# Module 4: ui.config

Purpose:

Stores OSGi configurations.

Example:

```
config.author

config.publish

config.dev

config.stage

config.prod
```

Example configuration:

```
com.company.project.Email.cfg.json
```

---

# Module 5: ui.frontend

Purpose:

Frontend development.

Contains:

```
CSS

SCSS

JavaScript

TypeScript

React

Angular

Vue
```

Produces:

```
clientlibs
```

which are copied into **ui.apps** during the build.

---

# Module 6: all

Purpose:

Creates one final installable package.

Contains:

```
project.all.zip
```

This ZIP includes:

```
core

ui.apps

ui.content

ui.config

frontend
```

---

# Build Process

```
Developer

↓

Write Java

↓

core

↓

Compile

↓

Jar

↓

ui.apps

↓

ZIP

↓

all

↓

Install into AEM
```

---

# Maven Commands

Build project

```bash
mvn clean install
```

Deploy to Author

```bash
mvn clean install -PautoInstallPackage
```

Deploy to Publish

```bash
mvn clean install -PautoInstallPackagePublish
```

Deploy only backend

```bash
mvn clean install -PautoInstallBundle
```

---

# What happens during the build?

1. Maven reads the parent `pom.xml`.
2. It builds the `core` module into a JAR.
3. It packages `ui.apps`.
4. It packages `ui.content`.
5. It packages `ui.config`.
6. It processes frontend assets.
7. It combines everything into `project.all.zip`.
8. If an auto-install profile is used, it deploys the package to AEM.

---

# Real Project Example

Suppose you need to create a **News Component**:

* Java logic → `core`
* HTL file → `ui.apps`
* Dialog → `ui.apps`
* CSS & JS → `ui.frontend`
* Sample page → `ui.content`
* Email service configuration → `ui.config`
* Final deployment → `all`

Each module has a clear responsibility, making the application easier to maintain.

---

# Interview Questions

### 1. Why is an AEM project multi-module?

It separates backend code, UI, content, configurations, and frontend assets so each can be developed, tested, and deployed independently.

### 2. Which module contains Sling Models?

`core`

### 3. Which module contains components and dialogs?

`ui.apps`

### 4. Which module stores sample content?

`ui.content`

### 5. Which module contains OSGi configurations?

`ui.config`

### 6. Which module generates the final deployment package?

`all`

---
#  5: AEM Components

# What is a Component?

A **Component** is a reusable building block used to create web pages in AEM.

Think of a component like a LEGO block:

* A page is built by combining many components.
* Each component has a specific responsibility.

Examples:

* Title
* Text
* Image
* Carousel
* Button
* Navigation
* Hero Banner

A typical home page might look like:

```text
Home Page

├── Header Component
├── Navigation Component
├── Hero Banner Component
├── Image Component
├── Text Component
├── Button Component
├── Footer Component
```

Instead of writing one large page, AEM assembles many reusable components.

---

# Why Components?

Without components:

* Code is duplicated.
* Changes are difficult.
* Maintenance is expensive.

With components:

* Reusable code.
* Easier maintenance.
* Faster development.
* Better authoring experience.

---

# Component Location

Custom components are usually stored under:

```text
/ui.apps/src/main/content/jcr_root/apps/mysite/components
```

Example:

```text
apps
└── mysite
    └── components
        ├── page
        ├── title
        ├── image
        ├── button
        └── banner
```

---

# Component Structure

Let's create a **Title Component**.

```text
title/

├── .content.xml
├── title.html
├── _cq_dialog/.content.xml
├── TitleModel.java   (in core module)
├── clientlibs/
│   ├── css.txt
│   ├── js.txt
│   ├── title.css
│   └── title.js
└── README.md (optional)
```

Each file has a specific purpose.

---

# `.content.xml`

This file defines the component.

```xml
<?xml version="1.0" encoding="UTF-8"?>

<jcr:root
    xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:cq="http://www.day.com/jcr/cq/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Component"
    jcr:title="Title Component"
    componentGroup="My Site Components"/>
```

### Explanation

* `jcr:primaryType="cq:Component"` → Declares this node as an AEM component.
* `jcr:title` → Display name shown to authors.
* `componentGroup` → Controls where the component appears in the component browser.

---

# `componentGroup`

Example:

```xml
componentGroup="My Site Components"
```

When an author opens the component browser, they will see:

```text
My Site Components
    ├── Title
    ├── Image
    ├── Banner
```

---

# `sling:resourceType`

Every AEM page stores a resource type.

Example:

```text
sling:resourceType = mysite/components/title
```

When AEM renders the page:

1. It reads `sling:resourceType`.
2. Finds the matching component under `/apps`.
3. Executes its HTL file.
4. Produces HTML.

---

# HTL (`title.html`)

```html
<div data-sly-use.model="com.mysite.core.models.TitleModel">
    <h2>${model.title}</h2>
</div>
```

### Explanation

* `data-sly-use.model` creates an instance of the Sling Model.
* `${model.title}` calls `getTitle()` from the Java class.

---

# Sling Model

```java
package com.mysite.core.models;

import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.injectorspecific.ValueMapValue;
import org.apache.sling.api.resource.Resource;

@Model(adaptables = Resource.class)
public class TitleModel {

    @ValueMapValue
    private String title;

    public String getTitle() {
        return title;
    }
}
```

### Flow

```
Author enters title
        ↓
Stored in JCR
        ↓
Sling Model reads property
        ↓
HTL displays it
        ↓
Browser renders HTML
```

---

# Component Dialog (`_cq_dialog/.content.xml`)

```xml
<jcr:root
    xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:cq="http://www.day.com/jcr/cq/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="nt:unstructured"
    sling:resourceType="cq/gui/components/authoring/dialog">

    <content
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/container">

        <items jcr:primaryType="nt:unstructured">

            <title
                jcr:primaryType="nt:unstructured"
                sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                fieldLabel="Title"
                name="./title"/>

        </items>

    </content>

</jcr:root>
```

### Explanation

This dialog creates a text field labeled **Title**.

When an author types:

```
Welcome to AEM
```

AEM stores:

```text
title = Welcome to AEM
```

under the component node in the JCR repository.

---

# Rendering Flow

```text
Author
   │
   ▼
Dialog
   │
Stores property in JCR
   │
   ▼
Sling Model
   │
Reads property
   │
   ▼
HTL
   │
Generates HTML
   │
   ▼
Browser
```

---

# Real Project Example

Imagine you're building an e-commerce homepage.

Components might include:

* Header
* Search Bar
* Hero Banner
* Product Carousel
* Featured Categories
* Offers Banner
* Footer

Each is developed once and reused across many pages.

---

# Best Practices

* Create one component for one responsibility.
* Keep business logic in Sling Models, not in HTL.
* Use meaningful `componentGroup` names.
* Reuse Core Components where possible instead of creating everything from scratch.
* Never hardcode content in HTL.

---

# Common Mistakes

❌ Writing Java logic directly in HTL.

❌ Modifying Adobe's `/libs` components instead of creating your own under `/apps`.

❌ Storing business logic in dialogs.

❌ Duplicating similar components instead of making them configurable.

---

# Interview Questions

### 1. What is an AEM Component?

A reusable building block used to create web pages.

### 2. Where are custom components stored?

Under `/apps/<project>/components`.

### 3. What is `cq:Component`?

The node type that identifies a node as an AEM component.

### 4. What is `componentGroup`?

It groups related components in the authoring component browser.

### 5. What is `sling:resourceType`?

It tells Sling which component should render a resource.

### 6. Why do we use Sling Models?

To separate business logic from the presentation layer (HTL).

---
#  6: HTL (HTML Template Language)

## What is HTL?

**HTL (HTML Template Language)**, formerly called **Sightly**, is AEM's server-side templating language.

It is used to:

* Display content on web pages.
* Connect HTL with Sling Models.
* Render HTML dynamically.
* Keep business logic out of HTML.

**HTL is secure by default** because it automatically escapes user input to reduce XSS (Cross-Site Scripting) risks.

---

# HTL Request Flow

```text
Browser Request
       │
       ▼
AEM Page
       │
       ▼
HTL (.html)
       │
       ▼
Sling Model (Java)
       │
       ▼
JCR Repository
       │
       ▼
HTML Response
       │
       ▼
Browser
```

---

# HTL File Location

Example:

```text
/apps/mysite/components/title/title.html
```

---

# Basic HTL Syntax

```html
<h1>Hello AEM</h1>
```

Static HTML is rendered as-is.

---

# Displaying Variables

```html
<h1>${properties.jcr:title}</h1>
```

### Explanation

`properties` refers to the current resource's properties.

If JCR contains:

```text
jcr:title = Welcome to AEM
```

Output:

```html
<h1>Welcome to AEM</h1>
```

---

# Using a Sling Model

## Java

```java
@Model(adaptables = Resource.class)
public class WelcomeModel {

    public String getMessage() {
        return "Welcome to AEM";
    }
}
```

## HTL

```html
<div data-sly-use.model="com.mysite.core.models.WelcomeModel">
    <h2>${model.message}</h2>
</div>
```

Output:

```html
<h2>Welcome to AEM</h2>
```

---

# `data-sly-use`

Creates an object that HTL can use.

```html
<div data-sly-use.model="com.mysite.core.models.TitleModel">
```

Think of it like:

```java
TitleModel model = new TitleModel();
```

---

# `data-sly-test`

Used for conditional rendering.

Example:

```html
<div data-sly-test="${properties.title}">
    ${properties.title}
</div>
```

If the title exists, it is displayed.

If not, nothing is rendered.

---

# `data-sly-test` with Boolean

```html
<div data-sly-test="${model.loggedIn}">
    Welcome User
</div>
```

Java:

```java
public boolean isLoggedIn() {
    return true;
}
```

Output:

```html
Welcome User
```

---

# `data-sly-list`

Loops through a collection.

Java:

```java
public List<String> getCities() {

    return Arrays.asList(
        "Hyderabad",
        "Delhi",
        "Mumbai"
    );

}
```

HTL:

```html
<ul data-sly-list.city="${model.cities}">
    <li>${city}</li>
</ul>
```

Output:

```html
<ul>
    <li>Hyderabad</li>
    <li>Delhi</li>
    <li>Mumbai</li>
</ul>
```

---

# `data-sly-repeat`

Similar to `data-sly-list`, but repeats the entire element.

```html
<div data-sly-repeat.item="${model.products}">
    <h2>${item.name}</h2>
</div>
```

---

# Difference Between `data-sly-list` and `data-sly-repeat`

| Feature  | `data-sly-list` | `data-sly-repeat`      |
| -------- | --------------- | ---------------------- |
| Repeats  | Children        | Entire element         |
| Use case | Lists, tables   | Cards, banners, blocks |

---

# `data-sly-resource`

Includes another AEM resource.

```html
<div data-sly-resource="${'header'}"></div>
```

Useful for embedding components like a header or footer.

---

# `data-sly-include`

Includes another HTL file.

```html
<div data-sly-include="footer.html"></div>
```

---

# `data-sly-call` and Templates

Define a reusable template:

```html
<template data-sly-template.card="${@ title}">
    <h2>${title}</h2>
</template>
```

Call it:

```html
<div data-sly-call="${card @ title='AEM'}"></div>
```

Output:

```html
<h2>AEM</h2>
```

---

# Context-Aware Escaping

HTL automatically escapes special characters.

If content is:

```text
<script>alert('hack')</script>
```

Output:

```html
&lt;script&gt;alert('hack')&lt;/script&gt;
```

The script is displayed as text instead of executing.

---

# Accessing Current Page

```html
${currentPage.title}
```

Common objects available in HTL:

* `properties`
* `currentPage`
* `pageProperties`
* `resource`
* `request`

---

# Real Project Example

### Banner Component

Java:

```java
@Model(adaptables = Resource.class)
public class BannerModel {

    @ValueMapValue
    private String title;

    @ValueMapValue
    private String image;

    public String getTitle() {
        return title;
    }

    public String getImage() {
        return image;
    }
}
```

HTL:

```html
<div data-sly-use.banner="com.mysite.core.models.BannerModel">

    <img src="${banner.image}" alt="${banner.title}"/>

    <h1>${banner.title}</h1>

</div>
```

If the author enters:

* Title: **Summer Sale**
* Image: `/content/dam/banner.jpg`

The browser renders:

```html
<div>
    <img src="/content/dam/banner.jpg" alt="Summer Sale"/>
    <h1>Summer Sale</h1>
</div>
```

---

# HTL Best Practices

✅ Keep business logic in Sling Models.

✅ Use `data-sly-test` instead of Java scriptlets.

✅ Prefer Sling Models over direct property access for complex logic.

✅ Reuse templates with `data-sly-template` and `data-sly-call`.

✅ Let HTL handle escaping for security.

---

# Common Mistakes

❌ Writing Java code inside HTL.

❌ Hardcoding values that should come from author dialogs.

❌ Putting business logic in the template.

❌ Ignoring null checks before rendering values.

---

# Interview Questions

### 1. What is HTL?

A server-side templating language used by AEM to generate HTML securely.

### 2. Why is HTL preferred over JSP?

* Cleaner syntax.
* Better security (automatic XSS protection).
* Better separation of concerns.
* Recommended by Adobe.

### 3. What is `data-sly-use`?

It creates an object (usually a Sling Model) that HTL can access.

### 4. Difference between `data-sly-list` and `data-sly-repeat`?

* `data-sly-list` repeats child content.
* `data-sly-repeat` repeats the entire HTML element.

### 5. What is `data-sly-test`?

A conditional statement used to render content only when an expression evaluates to true.

---
#  7: Sling Models (Complete Guide)

## What is a Sling Model?

A **Sling Model** is a Java class that acts as a bridge between the **JCR Repository** and **HTL**.

Instead of writing Java code inside HTL (which is not recommended), HTL calls methods from a Sling Model.

### Request Flow

```text
Author enters data
        │
        ▼
JCR Repository
        │
        ▼
Resource
        │
        ▼
Sling Model
        │
        ▼
HTL
        │
        ▼
Browser
```

---

# Why Sling Models?

Without Sling Models:

* HTL becomes difficult to maintain.
* Business logic gets mixed with presentation.

With Sling Models:

* Clean architecture.
* Easier testing.
* Better code reuse.
* Separation of concerns.

---

# Simple Sling Model

```java
package com.mysite.core.models;

import org.apache.sling.models.annotations.Model;
import org.apache.sling.api.resource.Resource;

@Model(adaptables = Resource.class)
public class WelcomeModel {

    public String getMessage() {
        return "Welcome to AEM";
    }
}
```

HTL:

```html
<div data-sly-use.model="com.mysite.core.models.WelcomeModel">
    <h2>${model.message}</h2>
</div>
```

Output:

```html
<h2>Welcome to AEM</h2>
```

---

# Understanding `@Model`

## Definition

`@Model` tells Sling that this Java class is a Sling Model.

### Syntax

```java
@Model(
    adaptables = Resource.class
)
```

### Parameters

```java
@Model(
    adaptables = Resource.class,
    adapters = WelcomeModel.class,
    resourceType = "mysite/components/title",
    defaultInjectionStrategy = DefaultInjectionStrategy.OPTIONAL
)
```

### Parameter Explanation

| Parameter                | Purpose                                     |
| ------------------------ | ------------------------------------------- |
| adaptables               | Object from which the model is created      |
| adapters                 | Interface/class exposed by the model        |
| resourceType             | Restricts the model to a specific component |
| defaultInjectionStrategy | Controls required vs optional injections    |

---

# `adaptables`

Most common values:

```java
@Model(adaptables = Resource.class)
```

OR

```java
@Model(adaptables = SlingHttpServletRequest.class)
```

### Difference

`Resource.class`

* Reads data from the repository.

`SlingHttpServletRequest.class`

* Gives access to the request, selectors, parameters, headers, etc.

---

# `@ValueMapValue`

Reads a property stored in the JCR node.

Suppose the repository contains:

```text
title = Welcome
description = Sling Models
```

Java:

```java
@Model(adaptables = Resource.class)
public class TitleModel {

    @ValueMapValue
    private String title;

    @ValueMapValue
    private String description;

    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }
}
```

HTL:

```html
<div data-sly-use.model="com.mysite.core.models.TitleModel">
    <h1>${model.title}</h1>
    <p>${model.description}</p>
</div>
```

Output:

```html
<h1>Welcome</h1>
<p>Sling Models</p>
```

---

# `@Inject`

General-purpose injection annotation.

```java
@Inject
private String title;
```

It can inject values from multiple sources, depending on the context.

**Recommendation:** In modern AEM projects, prefer specific annotations like `@ValueMapValue`, `@ChildResource`, and `@OSGiService` because they make the code easier to understand.

---

# `@ChildResource`

Used to inject a child resource.

Repository:

```text
component
│
├── title = Home
│
└── links
      │
      ├── item1
      ├── item2
      └── item3
```

Java:

```java
@ChildResource
private Resource links;
```

Now the `links` resource can be iterated to access its child nodes.

---

# `@Self`

Injects the adaptable object itself.

```java
@Self
private Resource resource;
```

Or:

```java
@Self
private SlingHttpServletRequest request;
```

Useful when you need direct access to the current resource or request.

---

# `@SlingObject`

Injects Sling API objects.

Example:

```java
@SlingObject
private ResourceResolver resourceResolver;

@SlingObject
private Resource resource;

@SlingObject
private SlingHttpServletRequest request;
```

---

# `@OSGiService`

Injects an OSGi service into the model.

Service:

```java
@Component(service = GreetingService.class)
public class GreetingService {

    public String greet() {
        return "Hello";
    }
}
```

Model:

```java
@OSGiService
private GreetingService greetingService;

public String getMessage() {
    return greetingService.greet();
}
```

---

# `@PostConstruct`

Runs automatically **after all injections are complete**.

```java
@PostConstruct
protected void init() {

    System.out.println("Model initialized");

}
```

Common uses:

* Validation
* Initializing collections
* Formatting data
* Calling services

---

# `@Optional`

Marks an injected field as optional.

```java
@ValueMapValue
@Optional
private String subtitle;
```

If `subtitle` doesn't exist, the model still works without throwing an error.

---

# `@Default`

Provides a default value when the property is missing.

```java
@ValueMapValue
@Default(values = "Default Title")
private String title;
```

If the author doesn't enter a title:

Output:

```text
Default Title
```

---

# `@Named`

Maps an injected field to a different property name.

Repository:

```text
pageTitle = Adobe AEM
```

Java:

```java
@ValueMapValue
@Named("pageTitle")
private String title;
```

Now `title` contains the value of `pageTitle`.

---

# Complete Example

```java
package com.mysite.core.models;

import javax.annotation.PostConstruct;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.DefaultInjectionStrategy;
import org.apache.sling.models.annotations.injectorspecific.ValueMapValue;
import org.apache.sling.models.annotations.injectorspecific.SlingObject;

@Model(
    adaptables = Resource.class,
    defaultInjectionStrategy = DefaultInjectionStrategy.OPTIONAL
)
public class ArticleModel {

    @ValueMapValue
    private String title;

    @ValueMapValue
    private String description;

    @SlingObject
    private Resource resource;

    @PostConstruct
    protected void init() {
        if (title == null) {
            title = "Untitled Article";
        }
    }

    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }

    public String getPath() {
        return resource.getPath();
    }
}
```

---

# HTL

```html
<div data-sly-use.article="com.mysite.core.models.ArticleModel">

    <h1>${article.title}</h1>

    <p>${article.description}</p>

    <small>${article.path}</small>

</div>
```

---

# Best Practices

✅ Use `@ValueMapValue` instead of generic `@Inject` for JCR properties.

✅ Keep business logic in Sling Models, not in HTL.

✅ Use `@PostConstruct` for initialization.

✅ Use `@OSGiService` to inject services instead of manually looking them up.

✅ Keep models focused on a single responsibility.

---

# Common Interview Questions

### 1. What is a Sling Model?

A Java class that adapts Sling objects (such as a `Resource` or `SlingHttpServletRequest`) and exposes data to HTL.

### 2. Difference between `Resource` and `SlingHttpServletRequest` as adaptables?

| Resource        | SlingHttpServletRequest                        |
| --------------- | ---------------------------------------------- |
| Repository data | HTTP request data                              |
| JCR properties  | Parameters, headers, selectors, resource, etc. |

### 3. Difference between `@Inject` and `@ValueMapValue`?

* `@Inject` is generic.
* `@ValueMapValue` specifically injects values from the JCR ValueMap and is usually preferred for content properties.

### 4. When is `@PostConstruct` executed?

After all dependency injections are completed and before the model is used.

### 5. Why use `@OSGiService`?

To inject reusable OSGi services into a Sling Model without manually obtaining them.

---
# Annotation 1: `@Model`

## What is `@Model`?

`@Model` is the annotation that tells **Apache Sling**:

> "This Java class is a Sling Model and can be adapted from a Resource or a SlingHttpServletRequest."

Without `@Model`, Sling will not recognize the class as a model.

---

# Why do we use `@Model`?

Imagine you have a Title component.

The author enters:

```text
Title = Welcome to AEM
```

This value is stored in the JCR repository.

Without a Sling Model:

```text
JCR
↓

HTL
```

HTL would have to access repository properties directly.

With a Sling Model:

```text
JCR
↓

@Resource

↓

Sling Model

↓

HTL

↓

Browser
```

The Sling Model becomes the bridge between content and the presentation layer.

---

# Syntax

```java
@Model(
    adaptables = Resource.class
)
public class TitleModel {

}
```

---

# Complete Syntax

```java
@Model(
    adaptables = Resource.class,
    adapters = Title.class,
    resourceType = "mysite/components/title",
    defaultInjectionStrategy = DefaultInjectionStrategy.OPTIONAL
)
public class TitleModel {

}
```

---

# Parameter 1: `adaptables`

This is the **most important parameter**.

It tells Sling **what object can be adapted into this model**.

### Resource Adaptable

```java
@Model(
    adaptables = Resource.class
)
```

Meaning:

```
JCR Resource

↓

TitleModel
```

Use this when reading content stored in the repository.

---

### SlingHttpServletRequest Adaptable

```java
@Model(
    adaptables = SlingHttpServletRequest.class
)
```

Meaning:

```
HTTP Request

↓

TitleModel
```

Use this when you need:

* Request parameters
* Headers
* Cookies
* Selectors
* Suffix
* Request attributes

---

# Difference

| Resource                      | SlingHttpServletRequest            |
| ----------------------------- | ---------------------------------- |
| Reads JCR content             | Reads HTTP request                 |
| Faster                        | More context available             |
| Common for content components | Common for request-dependent logic |

---

# Parameter 2: `adapters`

Example

```java
@Model(
    adaptables = Resource.class,
    adapters = Title.class
)
```

Suppose:

```java
public interface Title {

    String getTitle();

}
```

Implementation:

```java
@Model(
    adaptables = Resource.class,
    adapters = Title.class
)
public class TitleModel implements Title {

    @Override
    public String getTitle() {
        return "Adobe";
    }

}
```

Now other classes can adapt directly to the `Title` interface instead of the implementation.

**Why is this useful?**

* Loose coupling.
* Easier testing.
* Better maintainability.

---

# Parameter 3: `resourceType`

```java
@Model(
    adaptables = Resource.class,
    resourceType = "mysite/components/title"
)
```

This restricts the model to a specific component.

When the current resource has:

```text
sling:resourceType = mysite/components/title
```

the model is used automatically.

If another component has:

```text
mysite/components/banner
```

this model will not be applied.

---

# Parameter 4: `defaultInjectionStrategy`

Options:

```java
DefaultInjectionStrategy.REQUIRED
```

or

```java
DefaultInjectionStrategy.OPTIONAL
```

### REQUIRED

```java
@ValueMapValue
private String title;
```

If `title` is missing, model creation fails.

---

### OPTIONAL

```java
@Model(
    adaptables = Resource.class,
    defaultInjectionStrategy = DefaultInjectionStrategy.OPTIONAL
)
```

If a property is missing, the model is still created successfully.

**Recommended for most projects**, unless a field is mandatory.

---

# Complete Working Example

## Repository

```text
/content/mysite/home

jcr:content

title = Adobe Experience Manager

description = Enterprise CMS
```

---

## Sling Model

```java
package com.mysite.core.models;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.DefaultInjectionStrategy;
import org.apache.sling.models.annotations.injectorspecific.ValueMapValue;

@Model(
    adaptables = Resource.class,
    resourceType = "mysite/components/title",
    defaultInjectionStrategy = DefaultInjectionStrategy.OPTIONAL
)
public class TitleModel {

    @ValueMapValue
    private String title;

    @ValueMapValue
    private String description;

    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }
}
```

---

## HTL

```html
<div data-sly-use.model="com.mysite.core.models.TitleModel">

    <h1>${model.title}</h1>

    <p>${model.description}</p>

</div>
```

---

## Browser Output

```html
<h1>Adobe Experience Manager</h1>

<p>Enterprise CMS</p>
```

---

# Lifecycle of a Sling Model

```text
Browser Request
       │
       ▼
Sling resolves Resource
       │
       ▼
Checks @Model annotation
       │
       ▼
Creates TitleModel object
       │
       ▼
Injects all fields
       │
       ▼
Runs @PostConstruct
       │
       ▼
HTL accesses getters
       │
       ▼
HTML sent to Browser
```

---

# Real Project Example

Suppose you're building a **News Card Component**.

The author enters:

* News Title
* News Description
* Publish Date

The Sling Model:

* Reads all three properties.
* Formats the publish date.
* Generates a short summary.
* Sends clean data to HTL.

HTL only displays the values; all business logic stays in Java.

---

# Best Practices

* ✔ Keep one model focused on one component or responsibility.
* ✔ Prefer `Resource.class` unless request-specific information is required.
* ✔ Use interfaces with the `adapters` attribute for larger projects.
* ✔ Keep business logic in the model, not in HTL.
* ✔ Use `defaultInjectionStrategy = OPTIONAL` unless strict validation is required.

---

# Common Mistakes

* ❌ Forgetting the `@Model` annotation.
* ❌ Using the wrong adaptable type.
* ❌ Mixing heavy business logic with HTML.
* ❌ Assuming every injected property will always exist without handling missing values.

---

# Interview Questions

### 1. What is `@Model`?

It marks a Java class as a Sling Model so it can be adapted from a `Resource` or `SlingHttpServletRequest`.

### 2. Why is `adaptables` mandatory?

Because Sling must know which object type can be converted into the model.

### 3. When should you use `Resource.class`?

When the model primarily reads content stored in the JCR repository.

### 4. When should you use `SlingHttpServletRequest.class`?

When you need request-specific information such as parameters, selectors, headers, or cookies.

### 5. What is the purpose of `resourceType`?

It limits the model to a specific AEM component, preventing accidental use with other components.

---
# Annotation 2: `@Inject`

## What is `@Inject`?

`@Inject` tells the Sling Models framework:

> "Find a suitable value for this field from the available injection sources and assign it automatically."

Instead of writing:

```java
String title = resource.getValueMap().get("title", String.class);
```

you simply write:

```java
@Inject
private String title;
```

The framework performs the injection for you.

---

# Why do we use `@Inject`?

Without injection:

```java
ValueMap properties = resource.getValueMap();

String title = properties.get("title", String.class);
String description = properties.get("description", String.class);
```

With `@Inject`:

```java
@Inject
private String title;

@Inject
private String description;
```

This results in cleaner and easier-to-maintain code.

---

# How does `@Inject` work?

When Sling creates your model:

```text
Browser Request
      │
      ▼
Create Sling Model
      │
      ▼
Find @Inject fields
      │
      ▼
Search available injection sources
      │
      ▼
Assign values
      │
      ▼
Run @PostConstruct
```

---

# Basic Example

Repository content:

```text
title = Welcome to AEM
description = Learning Sling Models
```

Java:

```java
@Model(adaptables = Resource.class)
public class ArticleModel {

    @Inject
    private String title;

    @Inject
    private String description;

    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }
}
```

HTL:

```html
<div data-sly-use.article="com.mysite.core.models.ArticleModel">

    <h1>${article.title}</h1>

    <p>${article.description}</p>

</div>
```

Output:

```html
<h1>Welcome to AEM</h1>

<p>Learning Sling Models</p>
```

---

# Where does `@Inject` search?

`@Inject` can obtain values from several places depending on the adaptable.

Examples include:

* JCR properties
* Request attributes
* OSGi services
* Sling objects
* Child resources

Because it searches multiple sources, it is called a **generic injection annotation**.

---

# Example: Injecting a JCR Property

Repository:

```text
title = Adobe Experience Manager
```

Java:

```java
@Inject
private String title;
```

Equivalent manual code:

```java
String title = resource.getValueMap().get("title", String.class);
```

---

# Example: Injecting an OSGi Service

Service:

```java
@Component(service = GreetingService.class)
public class GreetingService {

    public String greet() {
        return "Hello";
    }

}
```

Model:

```java
@Inject
private GreetingService greetingService;
```

The framework finds the registered OSGi service and injects it.

---

# Example: Injecting a Resource

```java
@Inject
private Resource resource;
```

Now you can use:

```java
resource.getPath();
```

---

# Real Project Example

Suppose you're building a **Product Card** component.

Repository:

```text
title = Laptop

price = 65000

brand = Dell
```

Model:

```java
@Model(adaptables = Resource.class)
public class ProductModel {

    @Inject
    private String title;

    @Inject
    private String brand;

    @Inject
    private Integer price;

    public String getTitle() {
        return title;
    }

    public String getBrand() {
        return brand;
    }

    public Integer getPrice() {
        return price;
    }

}
```

HTL:

```html
<div data-sly-use.product="com.mysite.core.models.ProductModel">

<h2>${product.title}</h2>

<p>${product.brand}</p>

<p>₹ ${product.price}</p>

</div>
```

Output:

```html
Laptop

Dell

₹ 65000
```

---

# `@Inject` vs `@ValueMapValue`

| `@Inject`                         | `@ValueMapValue`                   |
| --------------------------------- | ---------------------------------- |
| Generic injection                 | Reads only JCR properties          |
| Can inject different object types | Specifically for ValueMap content  |
| Less explicit                     | More readable and preferred        |
| Older code often uses it          | Recommended in modern AEM projects |

### Recommended Practice

Instead of:

```java
@Inject
private String title;
```

Prefer:

```java
@ValueMapValue
private String title;
```

This makes it immediately clear that the value comes from the JCR repository.

---

# Lifecycle

```text
Resource
    │
    ▼
Sling Model Created
    │
    ▼
@Inject Fields Found
    │
    ▼
Injection Performed
    │
    ▼
@PostConstruct Executed
    │
    ▼
HTL Calls Getters
```

---

# Best Practices

✅ Prefer specific annotations (`@ValueMapValue`, `@ChildResource`, `@OSGiService`) whenever possible.

✅ Use `@Inject` only when a generic injection is appropriate.

✅ Keep injected fields `private`.

✅ Perform initialization or validation in `@PostConstruct`.

---

# Common Mistakes

❌ Assuming `@Inject` only reads JCR properties.

❌ Using `@Inject` everywhere, making the code harder to understand.

❌ Not handling missing values when they are optional.

---

# Interview Questions

### 1. What is `@Inject`?

It is a generic Sling Models annotation that automatically injects values from supported injection sources into model fields.

---

### 2. Is `@Inject` only for JCR properties?

No. It can inject:

* JCR properties
* OSGi services
* Sling objects
* Request attributes
* Child resources
* Other supported injection sources

---

### 3. Which is preferred: `@Inject` or `@ValueMapValue`?

For repository properties, `@ValueMapValue` is preferred because it clearly indicates the source of the injected value.

---

### 4. When is `@Inject` executed?

During Sling Model creation, before the `@PostConstruct` method is called.

---

### 5. Can `@Inject` inject services?

Yes. If a matching OSGi service is available, it can be injected, although `@OSGiService` is the clearer and recommended annotation for that purpose.

---

# Summary

* **`@Inject`** is a **generic dependency injection annotation**.
* It reduces boilerplate code.
* It works with multiple injection sources.
* Modern AEM development favors **specific injector annotations** because they improve readability and maintainability.

---

# Annotation 3: `@ValueMapValue`

## What is `@ValueMapValue`?

`@ValueMapValue` injects a property from the **JCR repository (ValueMap)** into a Sling Model field.

Think of it as:

> "Read this property from the current resource and assign it to my Java variable."

---

# What is a ValueMap?

Every resource in AEM has properties.

Example JCR node:

```text
/content/mysite/home/jcr:content

title = Welcome to AEM
description = Learn AEM Step by Step
author = Vijay Kumar
views = 1500
published = true
```

These properties are stored in a **ValueMap**.

Without Sling Models:

```java
ValueMap properties = resource.getValueMap();

String title = properties.get("title", String.class);
```

With `@ValueMapValue`:

```java
@ValueMapValue
private String title;
```

Much simpler!

---

# How `@ValueMapValue` Works

```text
JCR Repository
      │
      ▼
Resource
      │
      ▼
ValueMap
      │
      ▼
@ValueMapValue
      │
      ▼
Java Field
      │
      ▼
HTL
```

---

# Basic Example

## JCR Properties

```text
title = Adobe Experience Manager

description = Enterprise CMS Platform
```

## Sling Model

```java
package com.mysite.core.models;

import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.injectorspecific.ValueMapValue;
import org.apache.sling.api.resource.Resource;

@Model(adaptables = Resource.class)
public class ArticleModel {

    @ValueMapValue
    private String title;

    @ValueMapValue
    private String description;

    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }
}
```

## HTL

```html
<div data-sly-use.article="com.mysite.core.models.ArticleModel">

    <h1>${article.title}</h1>

    <p>${article.description}</p>

</div>
```

### Output

```html
<h1>Adobe Experience Manager</h1>

<p>Enterprise CMS Platform</p>
```

---

# Different Data Types

### String

```java
@ValueMapValue
private String title;
```

---

### Integer

JCR:

```text
views = 1500
```

Java:

```java
@ValueMapValue
private Integer views;
```

---

### Boolean

JCR:

```text
published = true
```

Java:

```java
@ValueMapValue
private Boolean published;
```

---

### Long

```java
@ValueMapValue
private Long fileSize;
```

---

### Date

```java
@ValueMapValue
private Calendar publishDate;
```

---

### String Array (Multifield)

JCR:

```text
tags

sports

technology

news
```

Java:

```java
@ValueMapValue
private String[] tags;
```

Loop in Java:

```java
for(String tag : tags){
    System.out.println(tag);
}
```

---

# Using `@Named`

Sometimes the JCR property name and Java field name are different.

JCR:

```text
pageTitle = Welcome to AEM
```

Java:

```java
@ValueMapValue
@Named("pageTitle")
private String title;
```

Now:

```java
title
```

contains:

```text
Welcome to AEM
```

---

# Using `@Default`

```java
@ValueMapValue
@Default(values="Untitled")
private String title;
```

If no `title` exists:

Output:

```text
Untitled
```

---

# Using `@Optional`

```java
@ValueMapValue
@Optional
private String subtitle;
```

If `subtitle` doesn't exist:

* No exception is thrown.
* Value becomes `null`.

---

# Real Project Example

Imagine you're building a **Product Card**.

Author fills in:

| Field        | Value       |
| ------------ | ----------- |
| Product Name | MacBook Pro |
| Brand        | Apple       |
| Price        | 210000      |
| In Stock     | true        |

Stored in JCR:

```text
productName = MacBook Pro

brand = Apple

price = 210000

inStock = true
```

Model:

```java
@Model(adaptables = Resource.class)
public class ProductModel {

    @ValueMapValue
    private String productName;

    @ValueMapValue
    private String brand;

    @ValueMapValue
    private Integer price;

    @ValueMapValue
    private Boolean inStock;

    public String getProductName() {
        return productName;
    }

    public String getBrand() {
        return brand;
    }

    public Integer getPrice() {
        return price;
    }

    public Boolean getInStock() {
        return inStock;
    }
}
```

HTL:

```html
<div data-sly-use.product="com.mysite.core.models.ProductModel">

<h2>${product.productName}</h2>

<p>${product.brand}</p>

<p>₹ ${product.price}</p>

<p>Available: ${product.inStock}</p>

</div>
```

Output:

```html
MacBook Pro

Apple

₹ 210000

Available: true
```

---

# `@Inject` vs `@ValueMapValue`

| Feature                            | `@Inject`         | `@ValueMapValue`       |
| ---------------------------------- | ----------------- | ---------------------- |
| Purpose                            | Generic injection | JCR property injection |
| Readability                        | Less explicit     | Very clear             |
| Recommended for content properties | ❌                 | ✅                      |
| Used in modern AEM                 | Sometimes         | Very frequently        |

---

# Internal Lifecycle

```text
Browser Request
      │
      ▼
Resource Found
      │
      ▼
Resource.getValueMap()
      │
      ▼
Find Property
      │
      ▼
Assign Field
      │
      ▼
@PostConstruct
      │
      ▼
HTL Calls Getter
```

---

# Best Practices

✅ Use `@ValueMapValue` for all simple content properties.

✅ Use wrapper classes (`Integer`, `Boolean`, `Long`) instead of primitive types (`int`, `boolean`, `long`) because wrapper types can be `null` if a property is missing.

✅ Keep field names aligned with JCR property names unless you intentionally use `@Named`.

✅ Use `@Default` or handle `null` values when appropriate.

---

# Common Mistakes

❌ Using primitive types when properties may not exist.

```java
@ValueMapValue
private int views; // Risky if property is missing
```

Prefer:

```java
@ValueMapValue
private Integer views;
```

---

❌ Forgetting getters.

HTL accesses values through getter methods, so without them your values won't be available.

---

❌ Expecting `@ValueMapValue` to read child resources.

It only reads properties from the **current resource**. For child nodes, use `@ChildResource`.

---

# Interview Questions

### 1. What is `@ValueMapValue`?

It injects a property from the current resource's `ValueMap` into a Sling Model field.

---

### 2. Why is it preferred over `@Inject`?

Because it clearly indicates that the value comes from the JCR repository, making the code more readable and maintainable.

---

### 3. Can `@ValueMapValue` read child nodes?

No. It reads only properties of the current resource. Use `@ChildResource` for child resources.

---

### 4. Can it inject arrays?

Yes. For example:

```java
@ValueMapValue
private String[] tags;
```

---

### 5. What happens if the property doesn't exist?

The field becomes `null` (unless a default value is provided or the injection strategy requires the property).

---
# Annotation 4: `@ChildResource`

## What is `@ChildResource`?

`@ChildResource` injects a **child resource (child node)** of the current resource into a Sling Model.

> It is used when data is stored **inside child nodes**, not as simple properties.

---

# Why do we need `@ChildResource`?

Consider this repository:

```text
/content/mysite/home/banner

title = Summer Sale
description = Up to 50% Off
```

Both `title` and `description` are properties, so you can use:

```java
@ValueMapValue
private String title;

@ValueMapValue
private String description;
```

But now imagine the structure changes:

```text
banner
│
├── title = Summer Sale
│
└── buttons
     │
     ├── item0
     │     text = Shop Now
     │     link = /products
     │
     └── item1
           text = Learn More
           link = /about
```

Here, `buttons` is a **child node**, not a property.

`@ValueMapValue` cannot read it.

You need:

```java
@ChildResource
private Resource buttons;
```

---

# How `@ChildResource` Works

```text
Current Resource
       │
       ▼
Find Child Node
       │
       ▼
Inject Resource
       │
       ▼
Java Object
       │
       ▼
HTL
```

---

# Basic Example

Repository:

```text
article

title = AEM

links
│
├── item1
├── item2
└── item3
```

Java:

```java
@Model(adaptables = Resource.class)
public class ArticleModel {

    @ChildResource
    private Resource links;

    public Resource getLinks() {
        return links;
    }
}
```

---

# Reading Child Resources

```java
for(Resource child : links.getChildren()){

    System.out.println(child.getName());

}
```

Output:

```text
item1

item2

item3
```

---

# Real Project Example – Navigation Menu

Repository:

```text
navigation

menuItems

    item0

        title = Home

        path = /content/home

    item1

        title = About

        path = /content/about

    item2

        title = Contact

        path = /content/contact
```

---

### Child Model

```java
package com.mysite.core.models;

import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.injectorspecific.ValueMapValue;
import org.apache.sling.api.resource.Resource;

@Model(adaptables = Resource.class)
public class MenuItemModel {

    @ValueMapValue
    private String title;

    @ValueMapValue
    private String path;

    public String getTitle() {
        return title;
    }

    public String getPath() {
        return path;
    }
}
```

---

### Parent Model

```java
package com.mysite.core.models;

import java.util.List;

import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.injectorspecific.ChildResource;

import org.apache.sling.api.resource.Resource;

@Model(adaptables = Resource.class)
public class NavigationModel {

    @ChildResource
    private List<MenuItemModel> menuItems;

    public List<MenuItemModel> getMenuItems() {
        return menuItems;
    }
}
```

---

### HTL

```html
<ul data-sly-use.nav="com.mysite.core.models.NavigationModel">

    <li data-sly-repeat.item="${nav.menuItems}">
        <a href="${item.path}">
            ${item.title}
        </a>
    </li>

</ul>
```

---

### Browser Output

```html
<ul>

<li>
<a href="/content/home">Home</a>
</li>

<li>
<a href="/content/about">About</a>
</li>

<li>
<a href="/content/contact">Contact</a>
</li>

</ul>
```

---

# Using `List<Model>` with `@ChildResource`

This is the **most common enterprise pattern**.

```java
@ChildResource
private List<ProductModel> products;
```

Each child node is automatically adapted into a `ProductModel`.

Repository:

```text
products

item0

item1

item2
```

Flow:

```text
products
     │
     ▼
item0
item1
item2
     │
     ▼
ProductModel
ProductModel
ProductModel
```

---

# `@ChildResource` vs `@ValueMapValue`

| `@ValueMapValue`               | `@ChildResource`                        |
| ------------------------------ | --------------------------------------- |
| Reads properties               | Reads child nodes                       |
| String, Integer, Boolean, etc. | Resource or List of Resources           |
| Used for simple fields         | Used for multifields and nested content |

---

# Common Use Cases

### 1. Multifield

```text
Employees

Employee1

Employee2

Employee3
```

Use:

```java
@ChildResource
private List<EmployeeModel> employees;
```

---

### 2. Carousel

```text
Slides

Slide1

Slide2

Slide3
```

Use:

```java
@ChildResource
private List<SlideModel> slides;
```

---

### 3. FAQ

```text
Questions

Question1

Question2

Question3
```

Use:

```java
@ChildResource
private List<QuestionModel> questions;
```

---

### 4. Footer Links

```text
footer

links

item0

item1

item2
```

Use:

```java
@ChildResource
private List<LinkModel> links;
```

---

# Lifecycle

```text
Current Resource
        │
        ▼
Find Child Node
        │
        ▼
Adapt Child Nodes
        │
        ▼
Create Child Models
        │
        ▼
Inject into Parent Model
        │
        ▼
@PostConstruct
        │
        ▼
HTL Displays Data
```

---

# Best Practices

✅ Use `List<ChildModel>` instead of manually iterating over `Resource` objects whenever possible.

✅ Create a separate Sling Model for child nodes.

✅ Keep parent and child models focused on their own responsibilities.

✅ Use meaningful node names (`menuItems`, `slides`, `products`) to make the repository structure easy to understand.

---

# Common Mistakes

❌ Using `@ValueMapValue` to read child nodes.

```java
@ValueMapValue
private List<ProductModel> products; // Incorrect
```

Use:

```java
@ChildResource
private List<ProductModel> products;
```

---

❌ Assuming the child node always exists.

If a child node is optional, check for `null` before using it or configure your model appropriately.

---

# Interview Questions

### 1. What is `@ChildResource`?

It injects a child resource or a list of child resources from the current resource into a Sling Model.

---

### 2. When should you use `@ChildResource`?

When data is stored as **child nodes**, such as:

* Multifields
* Navigation items
* Carousel slides
* FAQ entries
* Accordion panels

---

### 3. Can `@ChildResource` inject a list?

Yes.

```java
@ChildResource
private List<MenuItemModel> menuItems;
```

This is a very common pattern in enterprise AEM projects.

---

### 4. What is the difference between `@ValueMapValue` and `@ChildResource`?

* `@ValueMapValue` reads properties from the current resource.
* `@ChildResource` reads child resources (nested nodes).

---

### 5. Can `@ChildResource` adapt child nodes into Sling Models automatically?

Yes. If the target type is another Sling Model, Sling automatically adapts each child resource into that model.

---
# Annotation 5: `@Self`

## What is `@Self`?

`@Self` injects **the current adaptable object itself** into your Sling Model.

Think of it like this:

> "Give me the same object from which this Sling Model was created."

If your model is adapted from `Resource.class`, `@Self` injects the current `Resource`.

If your model is adapted from `SlingHttpServletRequest.class`, `@Self` injects the current request.

---

# Why do we use `@Self`?

Suppose your model is created from a request.

Without `@Self`:

```java
public String getPath() {
    return request.getResource().getPath();
}
```

But where does `request` come from?

You need:

```java
@Self
private SlingHttpServletRequest request;
```

Now you can use the current request anywhere in the model.

---

# Internal Working

```text
Browser Request
        │
        ▼
Sling Creates Model
        │
        ▼
Current Adaptable
(Resource or Request)
        │
        ▼
@Self
        │
        ▼
Java Field
```

---

# Example 1 – Inject Current Resource

```java
package com.mysite.core.models;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.injectorspecific.Self;

@Model(adaptables = Resource.class)
public class ArticleModel {

    @Self
    private Resource resource;

    public String getPath() {
        return resource.getPath();
    }

}
```

### Output

```
/content/mysite/en/home/jcr:content/root/article
```

---

# Example 2 – Inject Current Request

```java
package com.mysite.core.models;

import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.injectorspecific.Self;

@Model(adaptables = SlingHttpServletRequest.class)
public class RequestModel {

    @Self
    private SlingHttpServletRequest request;

    public String getMethod() {
        return request.getMethod();
    }

}
```

If the browser sends:

```
GET /content/mysite/en.html
```

Output:

```
GET
```

---

# Access Current Resource from Request

```java
@Model(adaptables = SlingHttpServletRequest.class)
public class DemoModel {

    @Self
    private SlingHttpServletRequest request;

    public String getResourcePath() {

        return request.getResource().getPath();

    }

}
```

---

# Real Project Example

Imagine you're building a **Product Detail Component**.

The URL is:

```
http://localhost:4502/content/mysite/products/laptop.html
```

Model:

```java
@Model(adaptables = SlingHttpServletRequest.class)
public class ProductModel {

    @Self
    private SlingHttpServletRequest request;

    public String getCurrentPagePath() {

        return request.getResource().getPath();

    }

}
```

Output:

```
/content/mysite/products/laptop
```

---

# Using `@Self` with Another Model

You can also adapt the current resource/request into another Sling Model.

```java
@Self
private ImageModel imageModel;
```

This is useful when one model needs functionality from another model.

---

# `@Self` vs `@SlingObject`

| `@Self`                                         | `@SlingObject`                                                  |
| ----------------------------------------------- | --------------------------------------------------------------- |
| Injects the current adaptable object            | Injects Sling API objects                                       |
| Usually `Resource` or `SlingHttpServletRequest` | `ResourceResolver`, `Resource`, `SlingHttpServletRequest`, etc. |
| Represents the object that created the model    | Provides commonly used Sling objects                            |

### Example

```java
@Self
private SlingHttpServletRequest request;
```

```java
@SlingObject
private ResourceResolver resourceResolver;
```

---

# Lifecycle

```text
Request Received
       │
       ▼
Model Created
       │
       ▼
Current Adaptable Identified
       │
       ▼
@Inject Fields
       │
       ▼
@Self Injection
       │
       ▼
@PostConstruct
       │
       ▼
HTL Uses Getters
```

---

# Best Practices

✅ Use `@Self` when you need the current `Resource` or `SlingHttpServletRequest`.

✅ Keep business logic in the model instead of HTL.

✅ Prefer `Resource.class` as the adaptable when request information is not needed.

---

# Common Mistakes

❌ Using the wrong adaptable.

Example:

```java
@Model(adaptables = Resource.class)

@Self
private SlingHttpServletRequest request;
```

This will fail because the model was adapted from a `Resource`, not a request.

Correct:

```java
@Model(adaptables = SlingHttpServletRequest.class)

@Self
private SlingHttpServletRequest request;
```

---

❌ Using `@Self` when `@SlingObject` is more appropriate.

If you only need a `ResourceResolver`, use:

```java
@SlingObject
private ResourceResolver resourceResolver;
```

instead of trying to derive it from another object.

---

# Interview Questions

### 1. What is `@Self`?

`@Self` injects the **current adaptable object** (such as a `Resource` or `SlingHttpServletRequest`) into a Sling Model.

---

### 2. When should you use `@Self`?

When you need direct access to the object that was used to create the Sling Model.

---

### 3. Can `@Self` inject a request?

Yes, if the model is adapted from `SlingHttpServletRequest.class`.

---

### 4. What happens if the adaptable type doesn't match?

Injection fails because Sling cannot inject a request into a model created from a `Resource`, or vice versa.

---

### 5. What is the difference between `@Self` and `@SlingObject`?

* `@Self` injects **the current adaptable object**.
* `@SlingObject` injects **Sling framework objects** like `ResourceResolver`, `Resource`, `SlingHttpServletRequest`, and others.

---

# Summary

* `@Self` gives you the object that the Sling Model was adapted from.
* It is commonly used with `Resource` and `SlingHttpServletRequest`.
* Always ensure the field type matches the model's `adaptables` value.
* Use it when you need direct access to the current request or resource.

---
# Annotation 6: `@SlingObject`

## What is `@SlingObject`?

`@SlingObject` injects **core Sling framework objects** into a Sling Model.

Instead of reading these objects manually, Sling injects them automatically.

---

# Why do we use `@SlingObject`?

Suppose you want to:

* Read another page.
* Access the DAM.
* Get the current request.
* Navigate the JCR repository.
* Search for resources.

You need Sling framework objects like:

* `Resource`
* `ResourceResolver`
* `SlingHttpServletRequest`
* `SlingHttpServletResponse`

`@SlingObject` injects these objects automatically.

---

# Internal Working

```text
Browser Request
        │
        ▼
Sling Creates Model
        │
        ▼
Looks for @SlingObject
        │
        ▼
Injects Sling Objects
        │
        ▼
@PostConstruct
        │
        ▼
HTL Uses Model
```

---

# Syntax

```java
@SlingObject
private ResourceResolver resourceResolver;
```

---

# Objects Supported by `@SlingObject`

| Object                   | Purpose           |
| ------------------------ | ----------------- |
| Resource                 | Current resource  |
| ResourceResolver         | Access repository |
| SlingHttpServletRequest  | Current request   |
| SlingHttpServletResponse | Current response  |

---

# Example 1 – Inject Resource

```java
@Model(adaptables = Resource.class)
public class DemoModel {

    @SlingObject
    private Resource resource;

    public String getPath() {
        return resource.getPath();
    }
}
```

Output:

```text
/content/mysite/en/home/jcr:content/root/title
```

---

# Example 2 – Inject ResourceResolver

## What is ResourceResolver?

`ResourceResolver` is one of the **most important APIs in AEM**.

It allows you to:

* Read repository data
* Find resources
* Access DAM assets
* Navigate pages
* Adapt resources to models

Think of it as your **gateway to the JCR repository**.

---

### Inject ResourceResolver

```java
@Model(adaptables = Resource.class)
public class PageModel {

    @SlingObject
    private ResourceResolver resourceResolver;

}
```

---

# Read Another Resource

```java
public String getHomePageTitle() {

    Resource resource = resourceResolver.getResource(
        "/content/mysite/en/home"
    );

    if(resource != null){

        return resource.getValueMap()
                       .get("jcr:title", "");

    }

    return "";

}
```

---

# Example Repository

```text
/content

    mysite

        en

            home

                jcr:content

                    jcr:title = Home
```

Output:

```text
Home
```

---

# Example 3 – Inject Request

```java
@Model(adaptables = SlingHttpServletRequest.class)
public class RequestModel {

    @SlingObject
    private SlingHttpServletRequest request;

    public String getMethod(){

        return request.getMethod();

    }

}
```

Output

```text
GET
```

---

# Example 4 – Request Parameter

URL

```text
/content/mysite/en/search.html?q=laptop
```

Java

```java
public String getKeyword(){

    return request.getParameter("q");

}
```

Output

```text
laptop
```

---

# Example 5 – Current Resource

```java
public String getCurrentPath(){

    return resource.getPath();

}
```

Output

```text
/content/mysite/en/home
```

---

# Real Project Example

Suppose you have a **Product Detail Component**.

Current Page

```text
/content/store/laptop
```

Using `ResourceResolver`, you read related products stored elsewhere.

```java
@ResourceResolver
↓

/content/store/products
↓

Product1

Product2

Product3
```

Java

```java
@SlingObject
private ResourceResolver resourceResolver;

public List<Resource> getProducts(){

    Resource parent =
        resourceResolver.getResource(
            "/content/store/products"
        );

    List<Resource> list = new ArrayList<>();

    if(parent != null){

        parent.getChildren().forEach(list::add);

    }

    return list;

}
```

Now HTL can display all related products.

---

# `@Self` vs `@SlingObject`

| @Self                  | @SlingObject                                  |
| ---------------------- | --------------------------------------------- |
| Current adaptable      | Sling framework object                        |
| Resource or Request    | Resource, ResourceResolver, Request, Response |
| Represents model input | Provides framework APIs                       |

---

# Lifecycle

```text
Current Resource
       │
       ▼
Model Created
       │
       ▼
Inject ResourceResolver
       │
       ▼
Inject Resource
       │
       ▼
Inject Request
       │
       ▼
@PostConstruct
       │
       ▼
HTL Calls Methods
```

---

# Best Practices

### ✅ Use `ResourceResolver` only when required

If all you need is the current component's properties, use `@ValueMapValue` instead of traversing the repository.

---

### ✅ Always check for `null`

```java
Resource resource =
    resourceResolver.getResource(path);

if(resource != null){

    // Safe to use

}
```

---

### ✅ Close service `ResourceResolver`s

If you obtain a `ResourceResolver` from a **service user** (using `ResourceResolverFactory`), always close it after use.

> **Note:** A `ResourceResolver` injected with `@SlingObject` is managed by Sling. **Do not close it manually.**

---

### ✅ Keep repository access efficient

Avoid repeatedly calling:

```java
resourceResolver.getResource(...)
```

inside loops when you can fetch data once and reuse it.

---

# Common Mistakes

❌ Using `ResourceResolver` for data already available through `@ValueMapValue`.

❌ Forgetting to check for `null` when reading another resource.

❌ Closing the request-bound `ResourceResolver` injected by `@SlingObject`.

❌ Performing heavy repository traversal in getter methods. Put initialization logic in `@PostConstruct` instead.

---

# Interview Questions

### 1. What is `@SlingObject`?

It injects Sling framework objects such as `Resource`, `ResourceResolver`, `SlingHttpServletRequest`, and `SlingHttpServletResponse` into a Sling Model.

---

### 2. What is a `ResourceResolver`?

It is the primary API used to access and navigate the AEM repository (JCR). It can retrieve resources, adapt them to models, and access content across the repository.

---

### 3. What is the difference between `Resource` and `ResourceResolver`?

| Resource                     | ResourceResolver                       |
| ---------------------------- | -------------------------------------- |
| Represents one node/resource | Used to find and access many resources |
| Current content              | Repository access API                  |

---

### 4. When should you use `@SlingObject`?

When you need Sling framework objects for repository access or request processing.

---

### 5. Can `@SlingObject` inject `ResourceResolver`?

**Yes.** This is one of its most common uses in enterprise AEM applications.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Which Sling Model annotations do you use most?"**

A strong answer is:

> "For component properties, I usually use `@ValueMapValue`. For multifields, I use `@ChildResource`. When I need repository access, I inject a `ResourceResolver` with `@SlingObject`. To consume reusable business logic, I use `@OSGiService`. I also use `@PostConstruct` for initialization and keep HTL free of business logic."

That demonstrates not only knowledge of the annotations but also an understanding of **when** to use each one.

---
# Annotation 7: `@OSGiService`

## What is `@OSGiService`?

`@OSGiService` injects an **OSGi Service** into a Sling Model.

Instead of creating an object manually:

```java
GreetingService service = new GreetingServiceImpl();
```

Sling automatically injects the registered service:

```java
@OSGiService
private GreetingService greetingService;
```

---

# What is an OSGi Service?

An **OSGi Service** is a reusable Java class that contains **business logic**.

Examples:

* Email sending
* Database access
* REST API calls
* Product search
* Currency conversion
* PDF generation

Think of it like this:

```text
HTL
   │
   ▼
Sling Model
   │
   ▼
OSGi Service
   │
   ▼
Business Logic
```

---

# Why use OSGi Services?

Without OSGi Service:

```java
public class ProductModel {

    public String calculateDiscount() {
        // Business logic here
    }

    public void sendEmail() {
        // Email logic here
    }

    public void callAPI() {
        // API logic here
    }
}
```

Problems:

* Huge model class.
* Difficult to test.
* Code duplication.

---

With OSGi Service:

```text
Sling Model
     │
     ▼
ProductService
EmailService
SearchService
PaymentService
```

Each service has **one responsibility**.

---

# Step 1: Create a Service Interface

```java
package com.mysite.core.services;

public interface GreetingService {

    String greet(String name);

}
```

---

# Step 2: Implement the Service

```java
package com.mysite.core.services.impl;

import org.osgi.service.component.annotations.Component;

import com.mysite.core.services.GreetingService;

@Component(service = GreetingService.class)
public class GreetingServiceImpl implements GreetingService {

    @Override
    public String greet(String name) {

        return "Welcome " + name;

    }

}
```

### Explanation

```java
@Component(service = GreetingService.class)
```

This registers the class as an OSGi Service.

When the bundle starts:

```text
GreetingServiceImpl

↓

OSGi Container

↓

Registered Service
```

---

# Step 3: Inject into Sling Model

```java
package com.mysite.core.models;

import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.injectorspecific.OSGiService;
import org.apache.sling.api.resource.Resource;

import com.mysite.core.services.GreetingService;

@Model(adaptables = Resource.class)
public class WelcomeModel {

    @OSGiService
    private GreetingService greetingService;

    public String getMessage() {

        return greetingService.greet("Vijay");

    }

}
```

---

# HTL

```html
<div data-sly-use.model="com.mysite.core.models.WelcomeModel">

    <h2>${model.message}</h2>

</div>
```

---

# Browser Output

```html
<h2>Welcome Vijay</h2>
```

---

# Internal Working

```text
AEM Starts
      │
      ▼
OSGi Scans @Component
      │
      ▼
Registers GreetingService
      │
      ▼
Sling Model Created
      │
      ▼
@OSGiService Found
      │
      ▼
Inject GreetingService
      │
      ▼
HTL Calls Model
```

---

# Real Project Example 1 – Email Service

Interface

```java
public interface EmailService {

    void sendEmail(String to,
                   String subject,
                   String body);

}
```

Implementation

```java
@Component(service = EmailService.class)
public class EmailServiceImpl
        implements EmailService {

    @Override
    public void sendEmail(String to,
                          String subject,
                          String body) {

        System.out.println("Email Sent");

    }

}
```

Sling Model

```java
@OSGiService
private EmailService emailService;

public void send(){

    emailService.sendEmail(
        "abc@gmail.com",
        "Welcome",
        "Hello"
    );

}
```

---

# Real Project Example 2 – Product Service

```java
public interface ProductService {

    List<Product> getProducts();

}
```

Model

```java
@OSGiService
private ProductService productService;

public List<Product> getProducts(){

    return productService.getProducts();

}
```

HTL

```html
<ul data-sly-repeat.product="${model.products}">

<li>

${product.name}

</li>

</ul>
```

---

# Real Project Example 3 – Currency Service

Suppose your company supports:

* India
* USA
* Europe

Service

```java
public interface CurrencyService {

    String format(double amount);

}
```

Implementation

```java
@Component(service = CurrencyService.class)
public class CurrencyServiceImpl
implements CurrencyService {

    public String format(double amount){

        return "₹ " + amount;

    }

}
```

Model

```java
@OSGiService
private CurrencyService currencyService;
```

Now every component uses the same formatting logic.

---

# `@OSGiService` vs `@Reference`

| `@OSGiService`             | `@Reference`                                   |
| -------------------------- | ---------------------------------------------- |
| Used in Sling Models       | Used in OSGi Components                        |
| Injects service into model | Injects service into another service/component |
| Sling Models API           | OSGi Declarative Services                      |

Example:

Inside a Sling Model:

```java
@OSGiService
private EmailService emailService;
```

Inside another OSGi service:

```java
@Reference
private EmailService emailService;
```

---

# Lifecycle

```text
Bundle Starts
      │
      ▼
@Component Found
      │
      ▼
Service Registered
      │
      ▼
Request Arrives
      │
      ▼
Model Created
      │
      ▼
@OSGiService Injected
      │
      ▼
@PostConstruct
      │
      ▼
HTL Displays Data
```

---

# Best Practices

✅ Create an interface for every service.

```java
ProductService
```

Implementation

```java
ProductServiceImpl
```

---

✅ Keep business logic inside services.

The Sling Model should prepare data for the view, not contain complex business rules.

---

✅ Make services reusable.

One `ProductService` can be used by:

* Components
* Servlets
* Workflows
* Schedulers
* Event Handlers

---

# Common Mistakes

### ❌ Creating services without an interface

Bad

```java
@Component
public class EmailService {

}
```

Good

```java
public interface EmailService {

}
```

```java
@Component(service=EmailService.class)
public class EmailServiceImpl
implements EmailService{

}
```

---

### ❌ Writing business logic inside Sling Models

Bad

```java
public String calculateDiscount(){

    // 300 lines

}
```

Move this logic into:

```java
DiscountService
```

---

### ❌ Forgetting `@Component`

Without it:

```java
@OSGiService
private EmailService service;
```

will be `null` because the service was never registered.

---

# Interview Questions

### 1. What is `@OSGiService`?

It injects an OSGi service into a Sling Model so that the model can use reusable business logic.

---

### 2. Why use OSGi Services?

* Code reuse
* Separation of concerns
* Easier testing
* Cleaner architecture
* Shared business logic

---

### 3. Difference between `@OSGiService` and `@Reference`?

* `@OSGiService` → Used in Sling Models.
* `@Reference` → Used in OSGi Components and Services.

---

### 4. Why create an interface?

Programming to interfaces:

* Makes implementations replaceable.
* Improves testing (mocking).
* Reduces coupling.

---

### 5. Can multiple components use the same service?

**Yes.** That's one of the biggest advantages of OSGi services.

---

# Enterprise Example

```text
Hero Component
        │
        │
Search Component
        │
        ▼
ProductService
        │
        ▼
External REST API
```

Instead of each component calling the REST API separately, they all use the shared `ProductService`. This centralizes logic, reduces duplication, and makes future changes much easier.

---

# Annotation 8: `@PostConstruct`

## What is `@PostConstruct`?

`@PostConstruct` is a lifecycle annotation.

It tells Sling:

> "Execute this method automatically **after all dependency injections are completed** and **before the model is used by HTL**."

You don't call this method yourself—Sling calls it automatically.

---

# Why do we use `@PostConstruct`?

Suppose your model has:

* `@ValueMapValue`
* `@ChildResource`
* `@OSGiService`

You want to:

* Validate data
* Format values
* Call a service
* Create lists
* Sort data

You should do all of this in `@PostConstruct`.

---

# Lifecycle

```text
Browser Request
        │
        ▼
Create Sling Model
        │
        ▼
Inject @ValueMapValue
        │
        ▼
Inject @ChildResource
        │
        ▼
Inject @OSGiService
        │
        ▼
Run @PostConstruct ⭐
        │
        ▼
HTL Calls Getters
        │
        ▼
Browser Response
```

---

# Syntax

```java
@PostConstruct
protected void init() {

}
```

---

# Simple Example

```java
@Model(adaptables = Resource.class)
public class WelcomeModel {

    @ValueMapValue
    private String title;

    @PostConstruct
    protected void init() {

        System.out.println("Model Initialized");

    }

    public String getTitle() {

        return title;

    }

}
```

Execution order:

```text
Inject title

↓

@PostConstruct

↓

getTitle()

↓

HTL
```

---

# Example 1 – Default Value

Repository:

```text
title = null
```

Java:

```java
@Model(adaptables = Resource.class)
public class ArticleModel {

    @ValueMapValue
    private String title;

    @PostConstruct
    protected void init() {

        if(title == null){

            title = "Untitled Article";

        }

    }

    public String getTitle(){

        return title;

    }

}
```

Output:

```text
Untitled Article
```

---

# Example 2 – Calling an OSGi Service

Service

```java
public interface GreetingService {

    String greet();

}
```

Model

```java
@OSGiService
private GreetingService greetingService;

private String message;

@PostConstruct
protected void init(){

    message = greetingService.greet();

}

public String getMessage(){

    return message;

}
```

HTL:

```html
<h1>${model.message}</h1>
```

---

# Example 3 – Format Author Data

Repository:

```text
title = adobe experience manager
```

Java:

```java
@ValueMapValue
private String title;

@PostConstruct
protected void init(){

    title = title.toUpperCase();

}
```

Output:

```text
ADOBE EXPERIENCE MANAGER
```

---

# Example 4 – Sort a List

```java
private List<String> cities;

@PostConstruct
protected void init(){

    cities = Arrays.asList(
            "Delhi",
            "Mumbai",
            "Hyderabad"
    );

    Collections.sort(cities);

}
```

Output:

```text
Delhi

Hyderabad

Mumbai
```

---

# Example 5 – Build a Custom Object

Repository:

```text
firstName = Vijay

lastName = Kumar
```

Java:

```java
@ValueMapValue
private String firstName;

@ValueMapValue
private String lastName;

private String fullName;

@PostConstruct
protected void init(){

    fullName = firstName + " " + lastName;

}

public String getFullName(){

    return fullName;

}
```

Output:

```text
Vijay Kumar
```

---

# Real Project Example – Product Component

Repository:

```text
price = 25000

discount = 10
```

Java:

```java
@ValueMapValue
private Double price;

@ValueMapValue
private Double discount;

private Double finalPrice;

@PostConstruct
protected void init(){

    finalPrice =
        price - (price * discount / 100);

}

public Double getFinalPrice(){

    return finalPrice;

}
```

Output:

```text
22500
```

HTL:

```html
<p>₹ ${model.finalPrice}</p>
```

---

# Why Not Do This in a Getter?

❌ Bad:

```java
public Double getFinalPrice(){

    return price -
           (price * discount / 100);

}
```

Every time HTL calls:

```html
${model.finalPrice}
```

the calculation runs again.

---

✅ Better:

```java
@PostConstruct
protected void init(){

    finalPrice =
        price - (price * discount / 100);

}
```

The calculation happens only **once**.

---

# Best Practices

### ✅ Use `@PostConstruct` for:

* Validation
* Default values
* Formatting
* Sorting
* Service calls
* Creating DTOs
* Preparing lists

---

### ❌ Avoid Heavy Processing

Don't do expensive operations like:

```java
@PostConstruct
protected void init(){

    for(int i=0;i<1000000;i++){

        // Heavy processing

    }

}
```

Heavy logic should be moved to an OSGi service.

---

### ✅ Keep Getters Simple

Good:

```java
public String getTitle(){

    return title;

}
```

Avoid calculations inside getters.

---

# Common Mistakes

### ❌ Expecting `@PostConstruct` to run before injection

It always runs **after** all injections are complete.

---

### ❌ Calling `init()` manually

Don't do:

```java
model.init();
```

Sling calls it automatically.

---

### ❌ Multiple `@PostConstruct` methods

A Sling Model should generally have **one** `@PostConstruct` method to keep initialization clear and predictable.

---

# Lifecycle Diagram

```text
@Resource

↓

Create Model

↓

Inject Properties

↓

Inject Child Resources

↓

Inject Services

↓

@PostConstruct ⭐

↓

Getters

↓

HTL

↓

Browser
```

---

# Interview Questions

### 1. What is `@PostConstruct`?

A lifecycle annotation that executes automatically after all dependencies have been injected and before the model is used.

---

### 2. When is `@PostConstruct` executed?

After:

* `@ValueMapValue`
* `@ChildResource`
* `@OSGiService`
* `@SlingObject`

have all been injected.

---

### 3. Why is `@PostConstruct` preferred over getters for calculations?

Because initialization happens **once**, improving readability and avoiding repeated work every time a getter is called.

---

### 4. Can you call an OSGi service inside `@PostConstruct`?

**Yes.** This is a very common pattern in enterprise AEM applications.

---

### 5. What should you avoid in `@PostConstruct`?

* Long-running tasks
* Network calls that block page rendering
* Large loops or expensive repository traversals

If such work is needed, move it to an OSGi service or another appropriate layer.

---

# Enterprise Example

Imagine an **E-commerce Product Component**.

When the page loads:

1. `@ValueMapValue` injects product ID.
2. `@OSGiService` injects `ProductService`.
3. `@PostConstruct` calls `ProductService` to fetch product details.
4. The model stores the product name, price, and stock.
5. HTL simply displays:

```html
<h2>${model.productName}</h2>
<p>₹ ${model.price}</p>
<p>In Stock: ${model.inStock}</p>
```

This keeps HTL clean and all business logic inside Java.

---

# Annotation 9: `@ScriptVariable`

## What is `@ScriptVariable`?

`@ScriptVariable` injects **AEM script bindings** (objects already available during page rendering) into a Sling Model.

Instead of manually looking up objects like `currentPage`, `PageManager`, or `currentStyle`, Sling injects them for you.

---

# Why do we use `@ScriptVariable`?

When AEM renders an HTL page, it automatically provides several useful objects.

Examples:

* `currentPage`
* `pageManager`
* `currentStyle`
* `component`
* `designer`

Instead of writing complex lookup code, you simply inject them.

---

# Internal Working

```text
Browser Request
        │
        ▼
HTL Rendering Starts
        │
        ▼
Script Bindings Created
        │
        ▼
@ScriptVariable Injection
        │
        ▼
Sling Model
        │
        ▼
HTL
```

---

# Syntax

```java
@ScriptVariable
private Page currentPage;
```

---

# Most Common Script Variables

| Script Variable | Java Type     | Purpose                 |
| --------------- | ------------- | ----------------------- |
| currentPage     | `Page`        | Current page            |
| pageManager     | `PageManager` | Manage pages            |
| currentStyle    | `Style`       | Component policy/design |
| component       | `Component`   | Current component       |
| designer        | `Designer`    | Design information      |

---

# Example 1 – Current Page

```java
package com.mysite.core.models;

import com.day.cq.wcm.api.Page;
import org.apache.sling.models.annotations.Model;
import org.apache.sling.models.annotations.injectorspecific.ScriptVariable;

import org.apache.sling.api.SlingHttpServletRequest;

@Model(adaptables = SlingHttpServletRequest.class)
public class PageModel {

    @ScriptVariable
    private Page currentPage;

    public String getTitle() {
        return currentPage.getTitle();
    }
}
```

---

Suppose your page is:

```text
/content/mysite/en/home

Title = Home Page
```

Output:

```text
Home Page
```

---

# Example 2 – Current Page Path

```java
public String getPath(){

    return currentPage.getPath();

}
```

Output:

```text
/content/mysite/en/home
```

---

# Example 3 – Page Name

```java
public String getName(){

    return currentPage.getName();

}
```

Output:

```text
home
```

---

# Example 4 – Page Depth

Repository:

```text
/content

mysite

en

home
```

Java:

```java
public int getDepth(){

    return currentPage.getDepth();

}
```

Output:

```text
4
```

---

# Example 5 – Parent Page

```java
public String getParentTitle(){

    return currentPage
            .getParent()
            .getTitle();

}
```

Suppose:

```text
Parent Page = English
```

Output:

```text
English
```

---

# HTL Example

```html
<div data-sly-use.page="com.mysite.core.models.PageModel">

<h1>${page.title}</h1>

<p>${page.path}</p>

</div>
```

Output:

```html
<h1>Home Page</h1>

<p>/content/mysite/en/home</p>
```

---

# Using `PageManager`

```java
@ScriptVariable
private PageManager pageManager;
```

Now you can retrieve any page:

```java
Page aboutPage =
pageManager.getPage(
"/content/mysite/en/about"
);
```

---

# Using `currentStyle`

Suppose a component policy defines:

```text
Theme = Dark
```

Inject:

```java
@ScriptVariable
private Style currentStyle;
```

Read the value:

```java
String theme =
currentStyle.get(
"theme",
String.class
);
```

Output:

```text
Dark
```

---

# Real Project Example

Imagine a **Breadcrumb Component**.

Current page:

```text
/content/company/en/products/laptop
```

Model:

```java
@ScriptVariable
private Page currentPage;

public List<String> getBreadcrumb(){

    List<String> list = new ArrayList<>();

    Page page = currentPage;

    while(page != null){

        list.add(page.getTitle());

        page = page.getParent();

    }

    Collections.reverse(list);

    return list;
}
```

Output:

```text
Company

English

Products

Laptop
```

HTL:

```html
<ul data-sly-repeat.item="${model.breadcrumb}">

<li>${item}</li>

</ul>
```

---

# `@ScriptVariable` vs `@SlingObject`

| `@ScriptVariable`                     | `@SlingObject`                                                     |
| ------------------------------------- | ------------------------------------------------------------------ |
| Injects AEM script bindings           | Injects Sling framework objects                                    |
| Example: `currentPage`, `pageManager` | Example: `Resource`, `ResourceResolver`, `SlingHttpServletRequest` |
| Used during page rendering            | Used for repository and request access                             |

---

# Lifecycle

```text
Request

↓

HTL Rendering

↓

Script Bindings Created

↓

@ScriptVariable Injected

↓

@PostConstruct

↓

HTL Calls Methods

↓

Browser
```

---

# Best Practices

✅ Use `@ScriptVariable` for page-related objects.

✅ Use `Page` APIs instead of manually traversing JCR.

✅ Check for `null` when working with parent pages.

---

# Common Mistakes

### ❌ Using `@ScriptVariable` in a `Resource` adaptable model

Most script variables are available only when the model is adapted from:

```java
SlingHttpServletRequest.class
```

---

### ❌ Confusing `currentPage` with `resource`

* `resource` → Current component resource.
* `currentPage` → The page containing the component.

---

# Interview Questions

### 1. What is `@ScriptVariable`?

It injects AEM script bindings (such as `currentPage` and `pageManager`) into a Sling Model.

---

### 2. Name some commonly used script variables.

* `currentPage`
* `pageManager`
* `currentStyle`
* `component`
* `designer`

---

### 3. What is the difference between `currentPage` and `resource`?

* `currentPage` represents the page being rendered.
* `resource` represents the current component on that page.

---

### 4. Can `@ScriptVariable` inject `currentPage`?

**Yes.** This is one of its most common uses.

---

### 5. When should you use `@ScriptVariable` instead of `@SlingObject`?

Use `@ScriptVariable` when you need AEM-specific page objects like `currentPage` or `PageManager`. Use `@SlingObject` for Sling framework objects like `ResourceResolver` or `Resource`.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do you get the current page title inside a Sling Model?"**

A strong answer is:

```java
@Model(adaptables = SlingHttpServletRequest.class)
public class PageModel {

    @ScriptVariable
    private Page currentPage;

    public String getTitle() {
        return currentPage.getTitle();
    }
}
```

This demonstrates that you know the correct annotation and the correct adaptable type.

---
# Annotation 10: `@RequestAttribute`

## What is `@RequestAttribute`?

`@RequestAttribute` injects an attribute stored in the **current HTTP request** into a Sling Model.

Unlike `@ValueMapValue`, which reads from the JCR repository, `@RequestAttribute` reads values that exist only for the lifetime of the current request.

---

# Why do we use `@RequestAttribute`?

Suppose a Servlet calculates a discount.

Instead of storing it in JCR, it passes it through the request.

Servlet:

```java
request.setAttribute("discount", 20);
```

Sling Model:

```java
@RequestAttribute
private Integer discount;
```

HTL:

```html
<p>Discount: ${model.discount}%</p>
```

Output:

```text
Discount: 20%
```

---

# Internal Flow

```text
Browser Request
        │
        ▼
Servlet / Filter
        │
request.setAttribute()
        │
        ▼
Sling Model
        │
@RequestAttribute
        │
        ▼
HTL
        │
        ▼
Browser
```

---

# Basic Example

## Servlet

```java
@Component(service = Servlet.class)
public class DemoServlet extends SlingSafeMethodsServlet {

    @Override
    protected void doGet(SlingHttpServletRequest request,
                         SlingHttpServletResponse response) {

        request.setAttribute("username", "Vijay");

    }

}
```

---

## Sling Model

```java
@Model(adaptables = SlingHttpServletRequest.class)
public class UserModel {

    @RequestAttribute
    private String username;

    public String getUsername() {

        return username;

    }

}
```

---

## HTL

```html
<div data-sly-use.user="com.mysite.core.models.UserModel">

<h1>${user.username}</h1>

</div>
```

Output

```html
<h1>Vijay</h1>
```

---

# Example 2 – Passing an Object

Servlet

```java
Product product = new Product();

product.setName("Laptop");

request.setAttribute("product", product);
```

Model

```java
@RequestAttribute
private Product product;
```

Getter

```java
public Product getProduct(){

    return product;

}
```

HTL

```html
<h2>${model.product.name}</h2>
```

Output

```text
Laptop
```

---

# Example 3 – Passing a List

Servlet

```java
List<String> cities =
Arrays.asList(
    "Hyderabad",
    "Delhi",
    "Mumbai"
);

request.setAttribute("cities", cities);
```

Model

```java
@RequestAttribute
private List<String> cities;
```

HTL

```html
<ul data-sly-repeat.city="${model.cities}">

<li>${city}</li>

</ul>
```

Output

```text
Hyderabad

Delhi

Mumbai
```

---

# Real Project Example – Search Results

Suppose a user searches for:

```text
Laptop
```

Flow

```text
Browser

↓

Search Servlet

↓

Calls SearchService

↓

Gets Products

↓

request.setAttribute("products")

↓

Sling Model

↓

HTL
```

Servlet

```java
List<Product> products =
productService.search("Laptop");

request.setAttribute(
    "products",
    products
);
```

Model

```java
@RequestAttribute
private List<Product> products;
```

HTL

```html
<div data-sly-repeat.product="${model.products}">

${product.name}

</div>
```

---

# `@RequestAttribute` vs `@ValueMapValue`

| @RequestAttribute                | @ValueMapValue                    |
| -------------------------------- | --------------------------------- |
| Reads request attributes         | Reads JCR properties              |
| Temporary (per request)          | Persistent (stored in repository) |
| Used for calculated/runtime data | Used for authored content         |

---

# `@RequestAttribute` vs `@ScriptVariable`

| @RequestAttribute                  | @ScriptVariable                       |
| ---------------------------------- | ------------------------------------- |
| Values explicitly added to request | Built-in AEM objects                  |
| Example: `discount`, `products`    | Example: `currentPage`, `pageManager` |

---

# Lifecycle

```text
Browser Request
        │
        ▼
Servlet Executes
        │
        ▼
request.setAttribute()
        │
        ▼
Model Created
        │
        ▼
@RequestAttribute Injected
        │
        ▼
@PostConstruct
        │
        ▼
HTL
```

---

# Best Practices

### ✅ Use for temporary data

Good examples:

* Search results
* Calculated discounts
* User session data
* Request-specific flags

---

### ✅ Keep attribute names meaningful

Good:

```java
request.setAttribute(
    "searchResults",
    results
);
```

Avoid:

```java
request.setAttribute("x", results);
```

---

### ✅ Handle missing attributes

```java
@PostConstruct
protected void init() {

    if (discount == null) {
        discount = 0;
    }

}
```

---

# Common Mistakes

### ❌ Expecting request attributes to be saved in JCR

They exist only for the current request.

---

### ❌ Using `@RequestAttribute` in a `Resource` adaptable model

Correct:

```java
@Model(adaptables = SlingHttpServletRequest.class)
```

because request attributes belong to the HTTP request.

---

### ❌ Using it for authorable content

If authors edit the value in a dialog, use `@ValueMapValue`, not `@RequestAttribute`.

---

# Interview Questions

### 1. What is `@RequestAttribute`?

It injects an attribute stored in the current `SlingHttpServletRequest` into a Sling Model.

---

### 2. When should you use `@RequestAttribute`?

When data is calculated or added during request processing and should not be stored in the repository.

---

### 3. What is the difference between `@RequestAttribute` and `@ValueMapValue`?

* `@RequestAttribute` reads **temporary request data**.
* `@ValueMapValue` reads **persistent JCR properties**.

---

### 4. Can `@RequestAttribute` inject objects?

**Yes.** It can inject:

* `String`
* `Integer`
* Custom Java objects
* Lists
* Any object placed into the request.

---

### 5. Which adaptable should you use?

```java
@Model(adaptables = SlingHttpServletRequest.class)
```

because request attributes are available only through the HTTP request.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do you pass data from a Servlet to a Sling Model?"**

A strong answer is:

1. In the Servlet:

```java
request.setAttribute("products", productList);
```

2. In the Sling Model:

```java
@RequestAttribute
private List<Product> products;
```

3. Display it in HTL:

```html
${model.products}
```

This demonstrates that you understand how Servlets, Sling Models, and HTL work together.

---

# Annotation 11: `@ResourcePath`

## What is `@ResourcePath`?

`@ResourcePath` injects a **Resource** from a specified JCR path.

Normally, a Sling Model works with the **current resource**. With `@ResourcePath`, you can directly inject another resource anywhere in the repository.

Think of it as:

> "Go to this repository path and inject that resource into my model."

---

# Why do we use `@ResourcePath`?

Suppose your current component is:

```text
/content/mysite/en/home/jcr:content/root/banner
```

But you need data from:

```text
/content/dam/mysite/logo.png
```

or

```text
/content/mysite/en/footer
```

Instead of manually calling:

```java
resourceResolver.getResource("/content/dam/mysite/logo.png");
```

you can use `@ResourcePath`.

---

# Internal Working

```text
Current Model
      │
      ▼
@ResourcePath
      │
      ▼
Given Repository Path
      │
      ▼
Find Resource
      │
      ▼
Inject Resource
```

---

# Syntax

```java
@ResourcePath(path="/content/mysite/en/home")
private Resource homePage;
```

---

# Example 1 – Inject a Page

Repository

```text
/content

    mysite

        en

            home

                jcr:content
```

Model

```java
@Model(adaptables = Resource.class)
public class HomeModel {

    @ResourcePath(path="/content/mysite/en/home")
    private Resource homePage;

    public String getPath() {

        return homePage.getPath();

    }

}
```

Output

```text
/content/mysite/en/home
```

---

# Example 2 – Read Page Title

Repository

```text
/content/mysite/en/home

jcr:title = Home Page
```

Java

```java
public String getTitle(){

    return homePage
            .getValueMap()
            .get("jcr:title", "");

}
```

Output

```text
Home Page
```

---

# Example 3 – Inject DAM Asset

Repository

```text
/content

dam

mysite

logo.png
```

Java

```java
@ResourcePath(path="/content/dam/mysite/logo.png")
private Resource logo;
```

Getter

```java
public String getLogoPath(){

    return logo.getPath();

}
```

Output

```text
/content/dam/mysite/logo.png
```

---

# Example 4 – Inject Content Fragment

Repository

```text
/content/dam

content-fragments

article1
```

Model

```java
@ResourcePath(
path="/content/dam/content-fragments/article1"
)
private Resource article;
```

Now you can adapt the resource to the appropriate Content Fragment API or read its properties.

---

# Real Project Example – Global Footer

Suppose every page needs the same footer stored at:

```text
/content/mysite/global/footer
```

Model

```java
@Model(adaptables = Resource.class)
public class FooterModel {

    @ResourcePath(
    path="/content/mysite/global/footer"
    )
    private Resource footer;

    public String getFooterTitle(){

        return footer
                .getValueMap()
                .get("title","");

    }

}
```

All pages reuse the same footer content.

---

# `@ResourcePath` vs `@ChildResource`

| @ResourcePath                                     | @ChildResource                              |
| ------------------------------------------------- | ------------------------------------------- |
| Reads a resource using a specific repository path | Reads a child node of the current resource  |
| Can access any resource                           | Limited to children of the current resource |

---

# `@ResourcePath` vs `@SlingObject`

| @ResourcePath                     | @SlingObject                                            |
| --------------------------------- | ------------------------------------------------------- |
| Injects a specific resource       | Injects `ResourceResolver`, `Resource`, `Request`, etc. |
| Path is defined in the annotation | Objects come from the current Sling context             |

---

# Lifecycle

```text
Model Created
      │
      ▼
@ResourcePath Found
      │
      ▼
Find Resource by Path
      │
      ▼
Inject Resource
      │
      ▼
@PostConstruct
      │
      ▼
HTL
```

---

# Best Practices

### ✅ Use `@ResourcePath` for shared content

Examples:

* Global footer
* Shared navigation
* Company logo
* Shared configuration pages

---

### ✅ Check for `null`

```java
public String getFooterTitle(){

    if(footer == null){
        return "";
    }

    return footer
            .getValueMap()
            .get("title","");
}
```

---

### ✅ Avoid hardcoding too many paths

Instead of:

```java
@ResourcePath(path="/content/mysite/global/footer")
```

consider storing configurable paths in OSGi configuration or component dialog properties if they may vary by environment or site.

---

# Common Mistakes

### ❌ Using an invalid path

```java
@ResourcePath(path="/wrong/path")
```

The injected resource will be `null`.

---

### ❌ Using `@ResourcePath` for the current resource

If you need the current resource, use:

```java
@SlingObject
private Resource resource;
```

or

```java
@Self
private Resource resource;
```

---

### ❌ Hardcoding environment-specific paths

Avoid embedding paths that differ between environments unless they are truly fixed.

---

# Interview Questions

### 1. What is `@ResourcePath`?

It injects a `Resource` from a specified JCR repository path into a Sling Model.

---

### 2. When should you use it?

When you need to access a known, shared resource such as:

* Global navigation
* Footer
* DAM assets
* Shared configuration content

---

### 3. Can `@ResourcePath` inject DAM assets?

**Yes.** Since assets are stored as resources in the JCR, they can be injected by path.

---

### 4. What is the difference between `@ResourcePath` and `@ChildResource`?

* `@ChildResource` reads child nodes of the current resource.
* `@ResourcePath` reads any resource identified by a repository path.

---

### 5. What happens if the resource doesn't exist?

The injected field is typically `null`, so your code should handle that safely.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How would you access a shared footer stored at `/content/mysite/global/footer` from a Sling Model?"**

A good answer is:

```java
@ResourcePath(path="/content/mysite/global/footer")
private Resource footer;
```

Then use:

```java
footer.getValueMap().get("title", "");
```

to read its properties.

---

# Summary of Sling Model Annotations Covered So Far

| Annotation          | Primary Purpose                       |
| ------------------- | ------------------------------------- |
| `@Model`            | Marks a class as a Sling Model        |
| `@Inject`           | Generic dependency injection          |
| `@ValueMapValue`    | Reads JCR properties                  |
| `@ChildResource`    | Injects child resources               |
| `@Self`             | Injects the current adaptable         |
| `@SlingObject`      | Injects Sling framework objects       |
| `@OSGiService`      | Injects OSGi services                 |
| `@PostConstruct`    | Initializes the model after injection |
| `@ScriptVariable`   | Injects AEM script bindings           |
| `@RequestAttribute` | Reads request-scoped attributes       |
| `@ResourcePath`     | Injects a resource by repository path |

---

# Annotation 12: `@Via`

## What is `@Via`?

`@Via` tells Sling:

> **"Don't inject this field directly. First go through another object, then inject it."**

It changes the source from which Sling performs the injection.

---

# Why do we need `@Via`?

Suppose your component has this structure:

```text
/content/mysite/home/banner

bannerTitle = Summer Sale

image
    fileReference = /content/dam/banner.jpg
```

Current Resource:

```text
banner
```

But the property you need is inside:

```text
image
```

Instead of manually writing:

```java
Resource image = resource.getChild("image");
```

You can use `@Via`.

---

# Internal Working

```text
Current Resource
       │
       ▼
@Via("image")
       │
       ▼
Child Resource
       │
       ▼
Inject Property
```

---

# Basic Syntax

```java
@ValueMapValue
@Via("image")
private String fileReference;
```

Sling first enters the `image` child resource and then injects `fileReference`.

---

# Example 1 – Child Resource

Repository

```text
banner

title = Sale

image

    fileReference = /content/dam/banner.jpg
```

Model

```java
@Model(adaptables = Resource.class)
public class BannerModel {

    @ValueMapValue
    @Via("image")
    private String fileReference;

    public String getFileReference() {
        return fileReference;
    }
}
```

Output

```text
/content/dam/banner.jpg
```

---

# Example 2 – Nested Sling Model

Repository

```text
product

details

    name = Laptop

    price = 65000
```

Child Model

```java
@Model(adaptables = Resource.class)
public class ProductDetailsModel {

    @ValueMapValue
    private String name;

    @ValueMapValue
    private Integer price;

    public String getName() {
        return name;
    }

    public Integer getPrice() {
        return price;
    }
}
```

Parent Model

```java
@Model(adaptables = Resource.class)
public class ProductModel {

    @Inject
    @Via("details")
    private ProductDetailsModel details;

    public ProductDetailsModel getDetails() {
        return details;
    }
}
```

HTL

```html
<h2>${model.details.name}</h2>

<p>₹ ${model.details.price}</p>
```

Output

```text
Laptop

₹65000
```

---

# Real Project Example – Hero Banner

Repository

```text
hero

content

    title = Adobe Summit

    description = Join us today
```

Model

```java
@Inject
@Via("content")
private HeroContentModel content;
```

HTL

```html
<h1>${model.content.title}</h1>

<p>${model.content.description}</p>
```

---

# `@Via` with Request

Suppose a wrapped request changes the adaptable.

```java
@Inject
@Via(type = ResourceSuperType.class)
private SomeModel model;
```

This is commonly used when extending AEM Core Components.

---

# Common `@Via` Types

| Type                 | Purpose                                   |
| -------------------- | ----------------------------------------- |
| `@Via("childName")`  | Inject through a child resource           |
| `ResourceSuperType`  | Read from a component's supertype         |
| `ForcedResourceType` | Treat a resource as another resource type |

The **child resource** form is the most common for beginners.

---

# `@Via` vs `@ChildResource`

### `@ChildResource`

```java
@ChildResource
private Resource image;
```

You get the `Resource` itself.

---

### `@Via`

```java
@ValueMapValue
@Via("image")
private String fileReference;
```

You directly get the property inside that child.

---

# Lifecycle

```text
Create Model
      │
      ▼
Find @Via
      │
      ▼
Navigate to Child Resource
      │
      ▼
Inject Property
      │
      ▼
@PostConstruct
      │
      ▼
HTL
```

---

# Best Practices

✅ Use `@Via` only when another adaptable or child resource is genuinely needed.

✅ For simple child nodes, `@ChildResource` is often easier to understand.

✅ Combine `@Via` with `@ValueMapValue` or another injector to make the injection source explicit.

---

# Common Mistakes

❌ Using `@Via` when the property already exists on the current resource.

❌ Using the wrong child node name.

Example:

```java
@Via("img")
```

when the repository contains:

```text
image
```

The injection will fail because the path doesn't exist.

---

# Interview Questions

### 1. What is `@Via`?

`@Via` changes the object used for injection. Instead of injecting directly from the current adaptable, Sling first navigates through another object (such as a child resource).

---

### 2. When should you use `@Via`?

When the data is not on the current resource but is available through:

* A child resource
* A wrapped request
* A resource supertype

---

### 3. What is the difference between `@Via` and `@ChildResource`?

* `@ChildResource` injects the child resource itself.
* `@Via` changes the injection source so you can inject properties or models through that child resource.

---

### 4. Is `@Via` commonly used?

It is **less common** than `@ValueMapValue` or `@ChildResource`, but it is frequently used in advanced AEM projects, especially when extending Core Components.

---

# Summary

* `@Via` is an **advanced injection annotation**.
* It redirects the injection to another adaptable.
* It's useful for nested content and Core Component customization.
* Use it only when it makes the code clearer than using `@ChildResource`.

---

# Sling Model s Covered So Far

|             | Status    |
| --------------------- | --------- |
| ✅ `@Model`            | Completed |
| ✅ `@Inject`           | Completed |
| ✅ `@ValueMapValue`    | Completed |
| ✅ `@ChildResource`    | Completed |
| ✅ `@Self`             | Completed |
| ✅ `@SlingObject`      | Completed |
| ✅ `@OSGiService`      | Completed |
| ✅ `@PostConstruct`    | Completed |
| ✅ `@ScriptVariable`   | Completed |
| ✅ `@RequestAttribute` | Completed |
| ✅ `@ResourcePath`     | Completed |
| ✅ `@Via`              | Completed |

---

# Annotation 13: `@Named`

## What is `@Named`?

`@Named` tells Sling to inject a value from a property with a **different name** than the Java field.

Normally:

```java
@ValueMapValue
private String title;
```

Sling looks for:

```text
title
```

But suppose the repository contains:

```text
pageTitle = Welcome to AEM
```

Your Java field is:

```java
private String title;
```

The names don't match.

Use:

```java
@ValueMapValue
@Named("pageTitle")
private String title;
```

Now Sling injects:

```text
pageTitle
      ↓
title
```

---

## Real Example

Repository

```text
productName = MacBook Pro
```

Model

```java
@ValueMapValue
@Named("productName")
private String name;
```

Getter

```java
public String getName() {
    return name;
}
```

HTL

```html
${model.name}
```

Output

```text
MacBook Pro
```

---

## When should you use `@Named`?

Use it when:

* JCR property name and Java field name are different.
* You want cleaner Java variable names.
* You cannot change the repository property name.

---

# Annotation 14: `@Default`

## What is `@Default`?

`@Default` provides a **default value** if the property is missing.

Without it:

Repository

```text
title = null
```

Java

```java
@ValueMapValue
private String title;
```

Output

```text
null
```

With `@Default`:

```java
@ValueMapValue
@Default(values = "Untitled")
private String title;
```

Output

```text
Untitled
```

---

## Different Types

### String

```java
@Default(values = "Adobe")
private String company;
```

---

### Integer

```java
@Default(intValues = 10)
private Integer count;
```

---

### Boolean

```java
@Default(booleanValues = true)
private Boolean enabled;
```

---

### Long

```java
@Default(longValues = 100L)
private Long size;
```

---

### Double

```java
@Default(doubleValues = 99.99)
private Double price;
```

---

## Real Project Example

Repository

```text
discount = null
```

Java

```java
@ValueMapValue
@Default(intValues = 0)
private Integer discount;
```

Output

```text
0
```

---

# Annotation 15: `@Optional`

## What is `@Optional`?

`@Optional` tells Sling:

> "If this value is not available, don't fail. Continue creating the model."

Example

```java
@ValueMapValue
@Optional
private String subtitle;
```

Repository

```text
title = Adobe
```

No:

```text
subtitle
```

Without `@Optional`

The injection may fail depending on the model's injection strategy.

With `@Optional`

```text
subtitle = null
```

The model still works.

---

# Complete Example

```java
package com.mysite.core.models;

import org.apache.sling.api.resource.Resource;

import org.apache.sling.models.annotations.Model;

import org.apache.sling.models.annotations.DefaultInjectionStrategy;

import org.apache.sling.models.annotations.injectorspecific.ValueMapValue;

import org.apache.sling.models.annotations.injectorspecific.Optional;

import org.apache.sling.models.annotations.injectorspecific.Named;

import org.apache.sling.models.annotations.injectorspecific.Default;

@Model(
    adaptables = Resource.class,
    defaultInjectionStrategy =
        DefaultInjectionStrategy.OPTIONAL
)
public class ProductModel {

    @ValueMapValue
    @Named("productName")
    private String name;

    @ValueMapValue
    @Default(intValues = 0)
    private Integer discount;

    @ValueMapValue
    @Optional
    private String subtitle;

    public String getName() {
        return name;
    }

    public Integer getDiscount() {
        return discount;
    }

    public String getSubtitle() {
        return subtitle;
    }
}
```

---

# Comparison

| Annotation  | Purpose                           |
| ----------- | --------------------------------- |
| `@Named`    | Maps to a different property name |
| `@Default`  | Supplies a default value          |
| `@Optional` | Makes the field optional          |

---

# Real Enterprise Example

Suppose your JCR has:

```text
productName = Laptop

price = 65000
```

There is **no**:

```text
discount
subtitle
```

Model

```java
@ValueMapValue
@Named("productName")
private String name;

@ValueMapValue
@Default(intValues = 0)
private Integer discount;

@ValueMapValue
@Optional
private String subtitle;
```

Result

```text
name = Laptop

discount = 0

subtitle = null
```

The component renders successfully without errors.

---

# Best Practices

✅ Use `@Named` when Java field names differ from JCR property names.

✅ Use `@Default` for values that should always have a fallback.

✅ Use `@Optional` only for fields that are truly optional.

✅ Prefer wrapper types (`Integer`, `Boolean`) instead of primitive types (`int`, `boolean`) when fields can be missing.

---

# Common Mistakes

❌ Using `@Default` with primitive types incorrectly.

❌ Forgetting that `@Named` changes only the mapping, not the property stored in JCR.

❌ Marking every field as `@Optional` even when some fields are required.

---

# Interview Questions

### 1. What is `@Named`?

It maps a Java field to a JCR property with a different name.

---

### 2. What is `@Default`?

It provides a fallback value if the property is not present.

---

### 3. What is `@Optional`?

It tells Sling that a missing value should not prevent the model from being created.

---

### 4. Can `@Named` be used with `@ValueMapValue`?

**Yes.** This is the most common combination.

---

### 5. Why use wrapper classes with `@Optional`?

Wrapper classes (`Integer`, `Boolean`) can hold `null`, while primitive types (`int`, `boolean`) cannot.

---

# 🎉 Sling Model Annotations Completed

You have now learned all the major Sling Model annotations used in enterprise AEM development:

* ✅ `@Model`
* ✅ `@Inject`
* ✅ `@ValueMapValue`
* ✅ `@ChildResource`
* ✅ `@Self`
* ✅ `@SlingObject`
* ✅ `@OSGiService`
* ✅ `@PostConstruct`
* ✅ `@ScriptVariable`
* ✅ `@RequestAttribute`
* ✅ `@ResourcePath`
* ✅ `@Via`
* ✅ `@Named`
* ✅ `@Default`
* ✅ `@Optional`

---
# Chapter 2: OSGi Annotations

# Annotation 1: `@Component` ⭐⭐⭐⭐⭐

---

# What is `@Component`?

`@Component` is an OSGi Declarative Services annotation.

It tells the OSGi container:

> **"This Java class is an OSGi Component. Create, manage, and register it."**

Without `@Component`, AEM treats your class as a normal Java class. It **will not** become an OSGi service.

---

# Why do we use `@Component`?

Suppose you create:

```java
public class EmailServiceImpl {

}
```

Can another class inject it?

❌ **No.**

Because OSGi doesn't know it exists.

Now add:

```java
@Component(service = EmailService.class)
public class EmailServiceImpl
        implements EmailService {

}
```

Now OSGi registers it automatically.

---

# Internal Working

```text
AEM Starts

      │

Bundle Loaded

      │

OSGi Scans @Component

      │

Creates Component

      │

Registers Service

      │

Available for Injection
```

---

# Basic Syntax

```java
@Component(
    service = GreetingService.class
)
public class GreetingServiceImpl
        implements GreetingService {

}
```

---

# Complete Syntax

```java
@Component(

    service = GreetingService.class,

    immediate = true,

    property = {
        "service.description=Greeting Service",
        "service.vendor=Adobe"
    },

    configurationPolicy =
        ConfigurationPolicy.OPTIONAL

)
public class GreetingServiceImpl
implements GreetingService {

}
```

---

# Parameter 1: `service`

This tells OSGi which interface this implementation provides.

Example

```java
@Component(
    service = GreetingService.class
)
```

Interface

```java
public interface GreetingService {

    String greet();

}
```

Implementation

```java
@Component(service = GreetingService.class)
public class GreetingServiceImpl
implements GreetingService {

    @Override
    public String greet(){

        return "Hello";

    }

}
```

Now another class can inject:

```java
@OSGiService
private GreetingService greetingService;
```

---

# Parameter 2: `immediate`

Default

```java
immediate = false
```

Meaning

The component starts **only when needed**.

---

Example

```java
@Component(
    immediate = true
)
```

Meaning

```text
Bundle Starts

↓

Component Starts Immediately
```

Use this when:

* Scheduler
* Listener
* Event Handler
* Startup initialization

---

# Parameter 3: `property`

Adds metadata.

Example

```java
@Component(

property = {

"service.description=Product Service",

"service.vendor=MyCompany"

}

)
```

Viewable in:

```text
/system/console/components
```

---

# Parameter 4: `configurationPolicy`

Options

```java
ConfigurationPolicy.OPTIONAL
```

```java
ConfigurationPolicy.REQUIRE
```

```java
ConfigurationPolicy.IGNORE
```

Most projects use

```java
OPTIONAL
```

---

# Complete Working Example

## Interface

```java
package com.mysite.core.services;

public interface GreetingService {

    String greet(String name);

}
```

---

## Implementation

```java
package com.mysite.core.services.impl;

import org.osgi.service.component.annotations.Component;

import com.mysite.core.services.GreetingService;

@Component(
        service = GreetingService.class
)
public class GreetingServiceImpl
implements GreetingService {

    @Override
    public String greet(String name){

        return "Welcome " + name;

    }

}
```

---

## Sling Model

```java
@Model(adaptables = Resource.class)
public class WelcomeModel {

    @OSGiService
    private GreetingService greetingService;

    public String getMessage(){

        return greetingService.greet("Vijay");

    }

}
```

---

## HTL

```html
<h2>${model.message}</h2>
```

Output

```text
Welcome Vijay
```

---

# Real Enterprise Example 1 – Email Service

```java
@Component(
service = EmailService.class
)
public class EmailServiceImpl
implements EmailService{

    @Override
    public void sendEmail(){

    }

}
```

Used by:

* Servlets
* Workflows
* Sling Models
* Event Handlers
* Schedulers

---

# Real Enterprise Example 2 – Search Service

```java
@Component(
service = SearchService.class
)
public class SearchServiceImpl
implements SearchService{

}
```

Every component can search using the same service.

---

# Real Enterprise Example 3 – REST API Service

```java
@Component(
service = WeatherService.class
)
public class WeatherServiceImpl
implements WeatherService{

}
```

Reads weather from an external API.

Reusable everywhere.

---

# Component Lifecycle

```text
Bundle Installed

↓

Bundle Started

↓

@Component Found

↓

Component Created

↓

Dependencies Injected

↓

@Activate

↓

Ready

↓

@Deactivate

↓

Destroyed
```

---

# Where can you verify it?

Go to:

```text
http://localhost:4502/system/console/components
```

Search

```text
GreetingServiceImpl
```

Status

```text
Satisfied
```

means it is active and ready.

---

# Best Practices

### ✅ Always program to interfaces

Good

```java
GreetingService

GreetingServiceImpl
```

Bad

```java
GreetingServiceImpl only
```

---

### ✅ One responsibility per component

Good

```text
EmailService

SearchService

ProductService
```

Bad

```text
UtilityService

5000 lines
```

---

### ✅ Use `@Component` only for reusable services

Do **not** annotate ordinary helper classes that are never managed by OSGi.

---

# Common Mistakes

### ❌ Forgetting `service=`

```java
@Component
```

Although DS can infer services in some cases, explicitly specifying the service interface is a common best practice for clarity.

---

### ❌ No interface

Bad

```java
@Component
public class ProductService{

}
```

Good

```java
ProductService

↓

ProductServiceImpl
```

---

### ❌ Heavy work in constructor

Don't do:

```java
public GreetingServiceImpl(){

// Read DB

// REST Call

}
```

Instead use:

```java
@Activate
```

---

# Interview Questions

### 1. What is `@Component`?

It marks a Java class as an OSGi Declarative Services component so AEM can create and manage it.

---

### 2. Why do we use `service=`?

It registers the implementation under the specified interface, allowing other components to depend on the interface rather than the implementation.

---

### 3. What is `immediate=true`?

The component is activated as soon as its dependencies are satisfied, instead of waiting until the service is first requested.

---

### 4. Can multiple services use `@Component`?

**Yes.** Almost every reusable backend service in AEM uses `@Component`.

---

### 5. Where can you check component status?

```
/system/console/components
```

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How does an OSGi service become available in AEM?"**

Answer:

1. Create an interface.
2. Implement it.
3. Annotate the implementation with:

```java
@Component(service = InterfaceName.class)
```

4. Deploy the bundle.
5. OSGi registers the service.
6. Inject it using `@Reference` (in another OSGi component) or `@OSGiService` (in a Sling Model).

This demonstrates the full OSGi service lifecycle.

---

# Annotation 2: `@Reference` ⭐⭐⭐⭐⭐

---

# What is `@Reference`?

`@Reference` is an **OSGi Dependency Injection annotation**.

It tells OSGi:

> **"Inject another OSGi service into this component."**

Think of it like Spring's `@Autowired`, but for OSGi.

---

# Why do we use `@Reference`?

Suppose you have two services:

```text
EmailService
```

and

```text
OrderService
```

`OrderService` needs to send an email after placing an order.

Instead of:

```java
EmailService emailService = new EmailServiceImpl();
```

Use:

```java
@Reference
private EmailService emailService;
```

OSGi automatically injects the service.

---

# Internal Working

```text
AEM Starts
      │
      ▼
Registers EmailService
      │
      ▼
Creates OrderService
      │
      ▼
Finds @Reference
      │
      ▼
Injects EmailService
      │
      ▼
OrderService Ready
```

---

# Basic Example

## Step 1: Service Interface

```java
public interface EmailService {

    void sendEmail(String to,
                   String subject,
                   String body);

}
```

---

## Step 2: Implementation

```java
@Component(service = EmailService.class)
public class EmailServiceImpl
implements EmailService {

    @Override
    public void sendEmail(String to,
                          String subject,
                          String body){

        System.out.println("Email Sent");

    }

}
```

---

## Step 3: Another Service

```java
@Component(service = OrderService.class)
public class OrderService {

    @Reference
    private EmailService emailService;

    public void placeOrder(){

        emailService.sendEmail(
                "user@gmail.com",
                "Order",
                "Order Successful"
        );

    }

}
```

---

# Flow Diagram

```text
EmailService
      │
      ▼
OSGi Container
      │
      ▼
@Reference
      │
      ▼
OrderService
      │
      ▼
placeOrder()
      │
      ▼
sendEmail()
```

---

# Constructor Injection (Recommended)

Instead of field injection:

```java
@Component(service = OrderService.class)
public class OrderService {

    private final EmailService emailService;

    @Activate
    public OrderService(@Reference EmailService emailService) {
        this.emailService = emailService;
    }

}
```

**Why?**

* Easier to test.
* Dependencies are immutable.
* Required dependencies are obvious.

Many modern AEM projects prefer constructor injection.

---

# Reference Cardinality

## 1. Mandatory (Default)

```java
@Reference
private EmailService emailService;
```

If the service is unavailable:

```text
Component will NOT start.
```

---

## 2. Multiple Services

Suppose:

```text
GoogleSearchService

AzureSearchService

ElasticSearchService
```

Inject all:

```java
@Reference
private List<SearchService> searchServices;
```

OSGi injects every implementation.

---

# Reference Policy

## Static (Default)

```text
Component Starts

↓

Reference Injected

↓

Never Changes
```

Good for most projects.

---

## Dynamic

```java
@Reference(
    policy = ReferencePolicy.DYNAMIC
)
```

If the service disappears:

* OSGi updates the reference automatically.
* Component continues running.

Mostly used in advanced scenarios.

---

# Real Project Example 1

## Payment Service

```java
@Component(service = PaymentService.class)
public class PaymentService {

    @Reference
    private EmailService emailService;

    public void pay(){

        emailService.sendEmail(
                "abc@gmail.com",
                "Payment",
                "Payment Success"
        );

    }

}
```

---

# Real Project Example 2

## Workflow

```java
@Component(
service = WorkflowProcess.class
)
public class ApprovalWorkflow
implements WorkflowProcess{

    @Reference
    private EmailService emailService;

}
```

Workflow sends email after approval.

---

# Real Project Example 3

## Scheduler

```java
@Component(
service = Runnable.class
)
public class DailyScheduler
implements Runnable{

    @Reference
    private ReportService reportService;

    @Override
    public void run(){

        reportService.generate();

    }

}
```

---

# `@Reference` vs `@OSGiService`

| `@Reference`                   | `@OSGiService`               |
| ------------------------------ | ---------------------------- |
| Used in OSGi Components        | Used in Sling Models         |
| Injects services into services | Injects services into models |
| OSGi Declarative Services      | Sling Models                 |

Example:

### OSGi Component

```java
@Reference
private EmailService emailService;
```

### Sling Model

```java
@OSGiService
private EmailService emailService;
```

---

# Lifecycle

```text
Bundle Starts
      │
      ▼
Register EmailService
      │
      ▼
Create OrderService
      │
      ▼
Inject @Reference
      │
      ▼
@Activate
      │
      ▼
Ready
```

---

# Best Practices

### ✅ Program to interfaces

Good:

```java
@Reference
private EmailService emailService;
```

Avoid:

```java
@Reference
private EmailServiceImpl emailService;
```

---

### ✅ Keep services focused

One service should have one responsibility.

Examples:

* EmailService
* SearchService
* ProductService

---

### ✅ Use constructor injection for required dependencies

Constructor injection makes dependencies explicit and simplifies unit testing.

---

# Common Mistakes

### ❌ Referencing implementation instead of interface

Wrong:

```java
@Reference
private EmailServiceImpl service;
```

Correct:

```java
@Reference
private EmailService service;
```

---

### ❌ Creating service objects manually

Wrong:

```java
EmailService service =
new EmailServiceImpl();
```

Always let OSGi manage service creation.

---

### ❌ Circular dependencies

Example:

```text
Service A

↓

Service B

↓

Service A
```

This can prevent components from becoming active.

---

# Interview Questions

### 1. What is `@Reference`?

It injects one OSGi service into another OSGi component.

---

### 2. Where is `@Reference` used?

Inside:

* OSGi Services
* Servlets
* Schedulers
* Workflow Processes
* Event Handlers
* Filters

---

### 3. What is the difference between `@Reference` and `@OSGiService`?

* `@Reference` → OSGi Components.
* `@OSGiService` → Sling Models.

---

### 4. What happens if a mandatory referenced service is unavailable?

The component will remain **unsatisfied** and will not become active.

---

### 5. Where can you verify references?

Open:

```text
http://localhost:4502/system/console/components
```

Select your component to see:

* References
* Bound services
* Component state

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do two OSGi services communicate?"**

A strong answer is:

1. Create a service interface.
2. Register its implementation using `@Component`.
3. Inject it into another service using `@Reference`.
4. Let OSGi manage the lifecycle and dependency injection.

This demonstrates a solid understanding of OSGi's service-oriented architecture.

---
# OSGi Annotation 3: `@Activate` ⭐⭐⭐⭐⭐

---

# What is `@Activate`?

`@Activate` is called **automatically by the OSGi framework** when a component becomes active.

Think of it as the **initialization method** of an OSGi component.

> It is called **only once** when the component is activated (or reactivated after configuration changes).

---

# Component Lifecycle

```text
Bundle Installed
       │
       ▼
Bundle Started
       │
       ▼
@Component Found
       │
       ▼
Dependencies (@Reference) Injected
       │
       ▼
@Activate ⭐
       │
       ▼
Component Ready
       │
       ▼
@Deactivate
```

---

# Why do we use `@Activate`?

Typical uses:

* Read OSGi configuration
* Initialize variables
* Create caches
* Open connections (if appropriate)
* Log startup information
* Validate configuration

---

# Basic Syntax

```java
@Component(service = GreetingService.class)
public class GreetingServiceImpl
        implements GreetingService {

    @Activate
    protected void activate() {

        System.out.println("Greeting Service Started");

    }

}
```

When AEM starts:

```
Greeting Service Started
```

is printed once.

---

# Complete Example

```java
@Component(service = GreetingService.class)
public class GreetingServiceImpl
implements GreetingService {

    private String message;

    @Activate
    protected void activate(){

        message = "Welcome to AEM";

    }

    @Override
    public String greet(){

        return message;

    }

}
```

Output

```
Welcome to AEM
```

---

# Reading OSGi Configuration

Suppose you have this configuration:

```text
Email Host

smtp.gmail.com

Port

587

Username

admin@gmail.com
```

Configuration Interface

```java
@ObjectClassDefinition(
    name = "Email Configuration"
)
public @interface EmailConfig {

    @AttributeDefinition(
        name="SMTP Host"
    )
    String host();

}
```

Service

```java
@Component(service = EmailService.class)
@Designate(ocd = EmailConfig.class)
public class EmailServiceImpl
implements EmailService {

    private String host;

    @Activate
    protected void activate(
            EmailConfig config){

        host = config.host();

    }

}
```

Now `host` contains:

```
smtp.gmail.com
```

---

# Constructor vs `@Activate`

### Constructor

```java
public GreetingServiceImpl(){

}
```

Runs when the object is created.

At this stage:

* OSGi references may **not** yet be injected.
* Configuration is **not** yet available.

---

### `@Activate`

Runs after:

* `@Reference`
* Configuration
* Component creation

Therefore:

```java
@Activate
```

is the correct place for initialization.

---

# Example with `@Reference`

```java
@Component(service = OrderService.class)
public class OrderService {

    @Reference
    private EmailService emailService;

    @Activate
    protected void activate(){

        System.out.println(
            "Email Service Ready = "
            + (emailService != null)
        );

    }

}
```

Output

```
Email Service Ready = true
```

---

# Real Project Example 1 – Cache Initialization

```java
@Component(service = ProductService.class)
public class ProductService {

    private Map<String,String> cache;

    @Activate
    protected void activate(){

        cache = new HashMap<>();

    }

}
```

---

# Real Project Example 2 – Scheduler

```java
@Component(
service = Runnable.class,
immediate = true
)
public class DailyJob
implements Runnable {

    @Activate
    protected void activate(){

        System.out.println(
            "Scheduler Started"
        );

    }

    @Override
    public void run(){

    }

}
```

---

# Real Project Example 3 – REST Client

```java
@Component(service = WeatherService.class)
public class WeatherService {

    private HttpClient client;

    @Activate
    protected void activate(){

        client = HttpClient.newHttpClient();

    }

}
```

The HTTP client is created once during activation instead of every request.

---

# Lifecycle Diagram

```text
Bundle Starts
      │
      ▼
@Component
      │
      ▼
@Reference Injection
      │
      ▼
Read Configuration
      │
      ▼
@Activate ⭐
      │
      ▼
Ready
```

---

# Best Practices

### ✅ Read configuration in `@Activate`

```java
@Activate
protected void activate(Config config){

}
```

---

### ✅ Initialize reusable objects

Examples:

* Cache
* Formatter
* Validator
* HTTP Client

---

### ✅ Keep `@Activate` fast

Initialization should be lightweight.

---

# Common Mistakes

### ❌ Heavy database operations

Avoid:

```java
@Activate
protected void activate(){

// Load 5 million records

}
```

This delays bundle startup.

---

### ❌ REST API calls during startup

Bad:

```java
@Activate
protected void activate(){

// Call external REST API

}
```

Do this lazily when needed unless startup validation is required.

---

### ❌ Using constructor instead of `@Activate`

Constructors are **not** the correct place for OSGi initialization because references and configuration may not yet be available.

---

# Interview Questions

### 1. What is `@Activate`?

It is an OSGi lifecycle annotation that is called when the component becomes active.

---

### 2. When is `@Activate` executed?

After:

* The component is created.
* `@Reference` dependencies are injected.
* OSGi configuration is available.

---

### 3. Why use `@Activate` instead of a constructor?

Because OSGi services and configuration are guaranteed to be available during `@Activate`, but not necessarily in the constructor.

---

### 4. Can `@Activate` receive configuration?

**Yes.**

```java
@Activate
protected void activate(MyConfig config){

}
```

---

### 5. What should you do in `@Activate`?

* Read configuration.
* Initialize resources.
* Prepare caches.
* Validate startup state.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"What is the execution order of an OSGi component?"**

A strong answer is:

```text
Bundle Starts
      ↓
@Component detected
      ↓
@Reference dependencies injected
      ↓
OSGi configuration loaded
      ↓
@Activate executes
      ↓
Component becomes active
      ↓
Business methods are called
      ↓
@Deactivate executes when the component stops
```

This answer demonstrates a clear understanding of the OSGi component lifecycle.

---


# OSGi Annotation 4: `@Deactivate` ⭐⭐⭐⭐⭐

---

# What is `@Deactivate`?

`@Deactivate` is an **OSGi lifecycle annotation**.

It tells the OSGi framework:

> **"Call this method before the component is destroyed or stopped."**

It is the last lifecycle method executed for an OSGi component.

---

# Why do we use `@Deactivate`?

When a component stops, you should release any resources it owns.

Typical cleanup includes:

* Closing database connections
* Closing HTTP clients
* Stopping scheduler threads
* Clearing caches
* Closing file streams
* Logging shutdown information

---

# Component Lifecycle

```text
Bundle Installed
       │
       ▼
Bundle Started
       │
       ▼
@Component
       │
       ▼
@Reference Injection
       │
       ▼
@Activate
       │
       ▼
Component Running
       │
       ▼
Bundle Stopped
       │
       ▼
@Deactivate ⭐
       │
       ▼
Component Destroyed
```

---

# Basic Syntax

```java
@Component(service = GreetingService.class)
public class GreetingServiceImpl
        implements GreetingService {

    @Activate
    protected void activate() {
        System.out.println("Service Started");
    }

    @Deactivate
    protected void deactivate() {
        System.out.println("Service Stopped");
    }

}
```

Console Output:

```
Service Started

...

Service Stopped
```

---

# Example 1 – Clearing Cache

```java
@Component(service = ProductService.class)
public class ProductService {

    private Map<String, String> cache;

    @Activate
    protected void activate() {
        cache = new HashMap<>();
    }

    @Deactivate
    protected void deactivate() {

        cache.clear();

        System.out.println("Cache Cleared");

    }

}
```

---

# Example 2 – Closing HTTP Client

```java
@Component(service = WeatherService.class)
public class WeatherService {

    private HttpClient client;

    @Activate
    protected void activate() {

        client = HttpClient.newHttpClient();

    }

    @Deactivate
    protected void deactivate() {

        client = null;

        System.out.println("HTTP Client Released");

    }

}
```

> In real applications, use the appropriate `close()` or cleanup method if the resource implements `AutoCloseable`.

---

# Example 3 – Scheduler Cleanup

```java
@Component(
    service = Runnable.class,
    immediate = true
)
public class DailyScheduler implements Runnable {

    @Activate
    protected void activate() {
        System.out.println("Scheduler Started");
    }

    @Deactivate
    protected void deactivate() {
        System.out.println("Scheduler Stopped");
    }

    @Override
    public void run() {

    }
}
```

---

# Real Enterprise Example – Email Service

```java
@Component(service = EmailService.class)
public class EmailServiceImpl
implements EmailService {

    private Session session;

    @Activate
    protected void activate() {

        // Initialize mail session

    }

    @Deactivate
    protected void deactivate() {

        session = null;

        System.out.println(
            "Email Session Closed"
        );

    }

}
```

---

# Lifecycle Flow

```text
AEM Starts
      │
      ▼
@Component Found
      │
      ▼
@Reference Injected
      │
      ▼
@Activate
      │
      ▼
Service Running
      │
      ▼
AEM Stops / Bundle Stops
      │
      ▼
@Deactivate
      │
      ▼
Cleanup Completed
```

---

# `@Activate` vs `@Deactivate`

| `@Activate`                | `@Deactivate`             |
| -------------------------- | ------------------------- |
| Runs when component starts | Runs when component stops |
| Initializes resources      | Releases resources        |
| Reads configuration        | Cleans up state           |
| Creates caches             | Clears caches             |

---

# Best Practices

## ✅ Release resources

```java
@Deactivate
protected void deactivate() {

    cache.clear();

}
```

---

## ✅ Log shutdown

```java
@Deactivate
protected void deactivate() {

    LOG.info("ProductService stopped");

}
```

---

## ✅ Keep cleanup lightweight

Cleanup should finish quickly.

---

# Common Mistakes

## ❌ Forgetting cleanup

Bad:

```java
private Connection connection;
```

Never closing it.

---

## ❌ Heavy processing

Avoid:

```java
@Deactivate
protected void deactivate() {

    // Process millions of records

}
```

Shutdown should not be delayed by expensive work.

---

## ❌ Throwing exceptions

If cleanup fails, catch and log the exception rather than letting it terminate the shutdown unexpectedly.

Example:

```java
@Deactivate
protected void deactivate() {

    try {
        cache.clear();
    } catch (Exception e) {
        LOG.error("Cleanup failed", e);
    }

}
```

---

# Complete Lifecycle

```text
Bundle Installed
       │
       ▼
@Component
       │
       ▼
@Reference
       │
       ▼
@Activate
       │
       ▼
Business Methods
       │
       ▼
@Deactivate
       │
       ▼
Bundle Removed
```

---

# Real Project Example

Imagine an **AEM Search Service**.

When AEM starts:

```
@Activate

↓

Create Search Cache

↓

Load Configuration

↓

Ready
```

When AEM stops:

```
@Deactivate

↓

Clear Cache

↓

Close Search Client

↓

Release Resources
```

This ensures that no memory or resources are left allocated after the service stops.

---

# Interview Questions

### 1. What is `@Deactivate`?

It is an OSGi lifecycle annotation that is called when an OSGi component is being stopped or destroyed.

---

### 2. When is `@Deactivate` executed?

It executes when:

* The bundle is stopped.
* The component is disabled.
* The component is removed.
* The component is reactivated because of configuration changes (the old instance is deactivated before a new one is activated).

---

### 3. What should you do inside `@Deactivate`?

* Close resources.
* Clear caches.
* Stop background tasks.
* Log shutdown information.

---

### 4. Is `@Deactivate` mandatory?

No. Use it only when your component has cleanup work to perform.

---

### 5. What is the difference between `@Activate` and `@Deactivate`?

* `@Activate` prepares the component.
* `@Deactivate` cleans up the component.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain the lifecycle of an OSGi component."**

A strong answer is:

```text
Bundle Starts
      ↓
@Component discovered
      ↓
@Reference dependencies injected
      ↓
@Activate called
      ↓
Component serves requests
      ↓
Bundle stops or configuration changes
      ↓
@Deactivate called
      ↓
Resources released
```

This demonstrates that you understand both startup and shutdown phases of OSGi services.

---



# OSGi Annotation 5: `@Modified` ⭐⭐⭐⭐⭐

---

# What is `@Modified`?

`@Modified` is called automatically by the OSGi framework whenever the **OSGi configuration of a component changes**.

Think of it as:

> **"My configuration has changed. Reload the new values."**

Without `@Modified`, you may need to restart the bundle or recreate the component to use updated configuration.

---

# Why do we use `@Modified`?

Imagine an Email Service.

Initially:

```text
SMTP Host = smtp.gmail.com

Port = 587
```

Later, an administrator changes:

```text
SMTP Host = smtp.office365.com

Port = 465
```

Instead of restarting AEM, `@Modified` reloads the configuration automatically.

---

# Component Lifecycle

```text
Bundle Starts
      │
      ▼
@Component
      │
      ▼
@Reference Injection
      │
      ▼
@Activate
      │
      ▼
Component Running
      │
      ▼
Configuration Changed
      │
      ▼
@Modified ⭐
      │
      ▼
Continue Running
```

---

# Basic Syntax

```java
@Component(service = GreetingService.class)
public class GreetingServiceImpl
implements GreetingService {

    @Activate
    protected void activate() {

        System.out.println("Activated");

    }

    @Modified
    protected void modified() {

        System.out.println("Configuration Changed");

    }

}
```

---

# Reading Configuration

Configuration Interface

```java
@ObjectClassDefinition(
    name="Email Configuration"
)
public @interface EmailConfig {

    @AttributeDefinition(
        name="SMTP Host"
    )
    String host();

    @AttributeDefinition(
        name="SMTP Port"
    )
    int port();

}
```

---

# Service

```java
@Component(service = EmailService.class)

@Designate(ocd = EmailConfig.class)

public class EmailServiceImpl
implements EmailService {

    private String host;

    private int port;

    @Activate
    @Modified
    protected void activate(
            EmailConfig config){

        host = config.host();

        port = config.port();

    }

}
```

Notice something important:

```java
@Activate
@Modified
protected void activate(EmailConfig config) {

    host = config.host();

    port = config.port();

}
```

The **same method** handles both activation and configuration updates.

This is the **recommended pattern** in modern AEM.

---

# Internal Working

```text
Configuration Saved

↓

OSGi Detects Change

↓

@Modified

↓

Read New Configuration

↓

Update Variables

↓

Continue Running
```

No restart required.

---

# Example 1 – Email Service

Current configuration

```text
Host

smtp.gmail.com
```

Admin changes

```text
Host

smtp.office365.com
```

`@Modified`

```java
@Modified
protected void modified(
        EmailConfig config){

    host = config.host();

}
```

New value

```text
smtp.office365.com
```

Immediately available.

---

# Example 2 – Scheduler Interval

Current

```text
Interval

60 seconds
```

Administrator changes

```text
10 seconds
```

```java
@Modified
protected void modified(
        SchedulerConfig config){

    interval =
        config.interval();

}
```

The scheduler now uses:

```text
10 seconds
```

without restarting AEM.

---

# Example 3 – REST API URL

Configuration

```text
API URL

https://api1.company.com
```

Later changed to

```text
https://api2.company.com
```

```java
@Modified
protected void modified(
        APIConfig config){

    apiUrl =
        config.apiUrl();

}
```

All future API calls use:

```text
https://api2.company.com
```

---

# Real Enterprise Example

Suppose your Product Service connects to:

```text
ElasticSearch
```

Configuration

```text
Host

localhost

Port

9200
```

Production administrator changes

```text
Host

elastic.company.com
```

`@Modified`

```java
@Modified
protected void modified(
ProductConfig config){

host = config.host();

}
```

No deployment.

No restart.

No downtime.

---

# Lifecycle Diagram

```text
Bundle Start

↓

@Component

↓

@Activate

↓

Running

↓

Admin Updates Config

↓

@Modified ⭐

↓

Running with New Config

↓

@Deactivate
```

---

# `@Activate` vs `@Modified`

| @Activate                    | @Modified                                  |
| ---------------------------- | ------------------------------------------ |
| Called when component starts | Called when configuration changes          |
| Initializes component        | Reloads configuration                      |
| Executes once per activation | Executes whenever configuration is updated |

---

# Best Practice ⭐

Use one method for both.

```java
@Activate

@Modified

protected void activate(
Config config){

}
```

This avoids duplicate code.

---

# Best Practices

### ✅ Read configuration inside `@Modified`

```java
host =
config.host();
```

---

### ✅ Keep update fast

Only update:

* Variables
* Cache
* Configuration

---

### ✅ Reuse activate()

```java
@Activate

@Modified
```

One method.

---

# Common Mistakes

### ❌ Restarting bundle

Not needed.

`@Modified`

handles configuration updates automatically.

---

### ❌ Duplicating code

Bad

```java
@Activate

activate(){

}
```

```java
@Modified

modified(){

}
```

Same code copied twice.

Better

```java
@Activate

@Modified
```

One shared method.

---

### ❌ Heavy processing

Avoid

```java
@Modified

{

// Read millions of records

}
```

Configuration updates should remain fast.

---

# Complete Lifecycle

```text
Bundle Starts

↓

@Component

↓

@Reference

↓

@Activate

↓

Running

↓

Configuration Updated

↓

@Modified

↓

Running

↓

@Deactivate
```

---

# Interview Questions

### 1. What is `@Modified`?

It is an OSGi lifecycle annotation that is called when the component's configuration changes.

---

### 2. Why use `@Modified`?

To reload configuration values without restarting the bundle or AEM instance.

---

### 3. Can `@Activate` and `@Modified` be on the same method?

**Yes.** This is the recommended pattern:

```java
@Activate
@Modified
protected void activate(MyConfig config) {
    // Load configuration
}
```

---

### 4. Does `@Modified` restart the component?

No. It updates the component's configuration while it continues running.

---

### 5. What should you do inside `@Modified`?

* Read updated configuration.
* Refresh caches if needed.
* Update in-memory variables.
* Avoid expensive operations.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How can you change an OSGi service configuration without restarting AEM?"**

A strong answer is:

1. Define an OSGi configuration interface using `@ObjectClassDefinition`.
2. Link it with the service using `@Designate`.
3. Read the configuration in a method annotated with both `@Activate` and `@Modified`.

This ensures that configuration changes are applied immediately at runtime.

---

# OSGi Annotations Covered So Far

* ✅ `@Component`
* ✅ `@Reference`
* ✅ `@Activate`
* ✅ `@Deactivate`
* ✅ `@Modified`


---

# OSGi Annotation 6: `@ObjectClassDefinition` ⭐⭐⭐⭐⭐

---

# What is `@ObjectClassDefinition`?

`@ObjectClassDefinition` is used to **define an OSGi configuration interface**.

Think of it as:

> **"This interface describes all the configuration properties for my OSGi service."**

It **does not create the service**.

It **defines the configuration** that administrators can edit.

---

# Why do we need it?

Imagine your Email Service.

Without configuration:

```java
String host = "smtp.gmail.com";
int port = 587;
String username = "admin@gmail.com";
```

If tomorrow your company changes to Office365:

```
smtp.office365.com
```

You must:

* Modify code
* Build bundle
* Deploy bundle
* Restart if needed

❌ Not good.

Instead:

```
AEM Configuration

↓

Change Value

↓

Save

↓

Done
```

No code changes.

---

# Internal Working

```text
Developer Creates Interface

↓

@ObjectClassDefinition

↓

AEM Generates Configuration Screen

↓

Administrator Updates Values

↓

Service Reads Configuration

↓

Application Uses Updated Values
```

---

# Basic Syntax

```java
import org.osgi.service.metatype.annotations.ObjectClassDefinition;

@ObjectClassDefinition(
    name = "Email Configuration",
    description = "SMTP Server Configuration"
)
public @interface EmailConfig {

}
```

---

# Explanation

```java
name = "Email Configuration"
```

Displayed in AEM Configuration Manager.

Example:

```
Email Configuration
```

---

```java
description =
"SMTP Server Configuration"
```

Displayed below the title.

---

# Complete Example

```java
package com.mysite.core.config;

import org.osgi.service.metatype.annotations.ObjectClassDefinition;
import org.osgi.service.metatype.annotations.AttributeDefinition;

@ObjectClassDefinition(

name="Email Configuration",

description="SMTP Server Configuration"

)

public @interface EmailConfig {

    @AttributeDefinition(
            name="SMTP Host"
    )
    String host();

    @AttributeDefinition(
            name="SMTP Port"
    )
    int port();

    @AttributeDefinition(
            name="Username"
    )
    String username();

}
```

Notice:

```
host()

port()

username()
```

These methods become configuration fields in AEM.

---

# AEM Configuration Screen

```
Email Configuration

SMTP Host

smtp.gmail.com

SMTP Port

587

Username

admin@gmail.com
```

The administrator fills these values.

---

# Using Configuration in Service

```java
@Component(service = EmailService.class)

@Designate(
    ocd = EmailConfig.class
)

public class EmailServiceImpl
implements EmailService {

    private String host;

    private int port;

    @Activate
    @Modified
    protected void activate(
            EmailConfig config){

        host = config.host();

        port = config.port();

    }

}
```

Now:

```
config.host()
```

returns:

```
smtp.gmail.com
```

---

# Real Project Example 1

## REST API

Configuration

```java
@ObjectClassDefinition(
name="Weather API"
)
public @interface WeatherConfig{

    @AttributeDefinition(
            name="API URL"
    )
    String apiUrl();

}
```

Service

```java
@Activate
protected void activate(
WeatherConfig config){

apiUrl =
config.apiUrl();

}
```

Administrator changes

```
https://api.company.com
```

No deployment needed.

---

# Real Project Example 2

## Search Service

Configuration

```
Elastic Host

Elastic Port

Index Name
```

Admin changes:

```
Host

elastic.company.com
```

Search starts using the new server immediately.

---

# Real Project Example 3

## Scheduler

Configuration

```
Run Every

30

minutes
```

Admin changes:

```
5
```

Scheduler reads:

```java
config.interval()
```

No restart.

---

# Lifecycle

```text
Bundle Starts

↓

@Component

↓

@ObjectClassDefinition

↓

Configuration Available

↓

@Activate

↓

Running

↓

Admin Updates

↓

@Modified
```

---

# `@ObjectClassDefinition` vs `@Component`

| @ObjectClassDefinition  | @Component               |
| ----------------------- | ------------------------ |
| Defines configuration   | Defines service          |
| Creates config metadata | Registers OSGi component |
| Interface               | Java class               |

---

# Best Practices

### ✅ Keep configuration in its own package

```
com.mysite.core.config
```

---

### ✅ Use meaningful names

Good

```
Email Configuration
```

Bad

```
Config1
```

---

### ✅ One configuration interface per service

Good

```
EmailConfig

↓

EmailService
```

Avoid putting unrelated settings into one configuration.

---

# Common Mistakes

### ❌ Hardcoding values

Bad

```java
String url =
"https://api.company.com";
```

Better

```java
config.apiUrl();
```

---

### ❌ Mixing configuration and business logic

Configuration belongs in the interface.

Business logic belongs in the service.

---

### ❌ Forgetting `@Designate`

Without:

```java
@Designate(
ocd=EmailConfig.class
)
```

the service won't automatically use the configuration interface.

---

# Complete Flow

```text
Developer

↓

Creates Config Interface

↓

@ObjectClassDefinition

↓

AEM Generates UI

↓

Administrator Saves Values

↓

@Activate

↓

Service Uses Config

↓

@Modified

↓

Updates Immediately
```

---

# Interview Questions

### 1. What is `@ObjectClassDefinition`?

It defines the metadata for an OSGi configuration, including its fields, labels, and descriptions.

---

### 2. Is `@ObjectClassDefinition` used on a class?

**No.**

It is used on an **interface**.

---

### 3. What does it generate?

It generates an editable configuration definition that appears in AEM's OSGi Configuration Manager.

---

### 4. Does it create an OSGi service?

**No.**

It only defines configuration metadata.

---

### 5. Which annotation connects it to a service?

```java
@Designate
```

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do you make an OSGi service configurable without changing code?"**

A complete answer is:

1. Create a configuration interface using `@ObjectClassDefinition`.
2. Define configuration fields using `@AttributeDefinition`.
3. Connect the interface to the service using `@Designate`.
4. Read values in a method annotated with `@Activate` and `@Modified`.

This is the standard pattern used in enterprise AEM projects.

---

# OSGi Annotations Covered

* ✅ `@Component`
* ✅ `@Reference`
* ✅ `@Activate`
* ✅ `@Deactivate`
* ✅ `@Modified`
* ✅ `@ObjectClassDefinition`

---


# OSGi Annotation 7: `@AttributeDefinition` ⭐⭐⭐⭐⭐

---

# What is `@AttributeDefinition`?

`@AttributeDefinition` defines **one configuration property** inside an OSGi configuration interface.

Think of it like this:

```
@ObjectClassDefinition
        │
        ├── @AttributeDefinition → SMTP Host
        ├── @AttributeDefinition → SMTP Port
        ├── @AttributeDefinition → Username
        └── @AttributeDefinition → Password
```

Each method in the interface becomes one field in the AEM configuration screen.

---

# Why do we use it?

Suppose you have an Email Service.

Instead of hardcoding:

```java
String host = "smtp.gmail.com";
int port = 587;
```

You define configurable fields:

```java
@AttributeDefinition(name="SMTP Host")
String host();

@AttributeDefinition(name="SMTP Port")
int port();
```

Now the administrator can change them without modifying code.

---

# Basic Syntax

```java
@AttributeDefinition(
    name = "SMTP Host"
)
String host();
```

---

# Complete Example

```java
package com.mysite.core.config;

import org.osgi.service.metatype.annotations.*;

@ObjectClassDefinition(
    name = "Email Configuration"
)
public @interface EmailConfig {

    @AttributeDefinition(
        name = "SMTP Host",
        description = "SMTP Server Host Name"
    )
    String host() default "smtp.gmail.com";

    @AttributeDefinition(
        name = "SMTP Port",
        description = "SMTP Server Port"
    )
    int port() default 587;

    @AttributeDefinition(
        name = "Username"
    )
    String username();

    @AttributeDefinition(
        name = "Password"
    )
    String password();

}
```

---

# AEM Configuration Screen

```
-------------------------------------
Email Configuration
-------------------------------------

SMTP Host
[smtp.gmail.com]

SMTP Port
[587]

Username
[admin@gmail.com]

Password
[********]

-------------------------------------
```

---

# Parameter 1: `name`

```java
@AttributeDefinition(
    name = "SMTP Host"
)
```

This is the **label** shown in AEM.

Screen:

```
SMTP Host
```

---

# Parameter 2: `description`

```java
@AttributeDefinition(
    name = "SMTP Host",
    description = "SMTP server hostname"
)
```

Displayed as help text to administrators.

---

# Default Values

You can assign defaults using Java interface defaults.

```java
String host() default "smtp.gmail.com";
```

or

```java
int port() default 587;
```

If no value is configured, these defaults are used.

---

# Boolean Example

```java
@AttributeDefinition(
    name = "Enable Email"
)
boolean enabled() default true;
```

Configuration

```
Enable Email

☑ Checked
```

---

# Integer Example

```java
@AttributeDefinition(
    name = "Retry Count"
)
int retryCount() default 3;
```

Output

```
Retry Count

3
```

---

# String Array Example

```java
@AttributeDefinition(
    name = "Allowed Domains"
)
String[] domains() default {
    "company.com",
    "gmail.com"
};
```

Output

```
Allowed Domains

company.com

gmail.com
```

---

# Using Configuration in Service

```java
@Component(service = EmailService.class)

@Designate(
        ocd = EmailConfig.class
)

public class EmailServiceImpl
implements EmailService {

    private String host;

    private int port;

    @Activate
    @Modified
    protected void activate(
            EmailConfig config){

        host = config.host();

        port = config.port();

    }

}
```

Now:

```java
config.host();
```

returns

```
smtp.gmail.com
```

---

# Real Project Example 1

## Search Configuration

```java
@AttributeDefinition(
    name="Elastic Host"
)
String host();

@AttributeDefinition(
    name="Elastic Port"
)
int port();
```

Admin enters

```
elastic.company.com

9200
```

---

# Real Project Example 2

## Scheduler

```java
@AttributeDefinition(
    name="Interval"
)
int interval() default 30;
```

Admin changes

```
30

↓

5
```

Scheduler starts every:

```
5 minutes
```

---

# Real Project Example 3

## REST API

```java
@AttributeDefinition(
    name="Base URL"
)
String apiUrl();

@AttributeDefinition(
    name="API Key"
)
String apiKey();
```

No code change needed when the API endpoint changes.

---

# Lifecycle

```
Developer

↓

@AttributeDefinition

↓

AEM Generates Field

↓

Administrator Saves Value

↓

@Activate

↓

Service Uses Value

↓

@Modified

↓

Updated Immediately
```

---

# `@ObjectClassDefinition` vs `@AttributeDefinition`

| `@ObjectClassDefinition`  | `@AttributeDefinition`  |
| ------------------------- | ----------------------- |
| Defines the configuration | Defines one field       |
| Used once                 | Used for every property |
| Interface level           | Method level            |

---

# Best Practices

### ✅ Give meaningful names

Good

```java
@AttributeDefinition(
    name="SMTP Host"
)
```

Bad

```java
@AttributeDefinition(
    name="Field1"
)
```

---

### ✅ Add descriptions

```java
description =
"SMTP Server Host Name"
```

This helps administrators understand the purpose of the field.

---

### ✅ Use default values where appropriate

```java
int port() default 587;
```

Avoid unnecessary mandatory configuration.

---

### ✅ Choose the correct Java type

| Java Type  | Configuration Type |
| ---------- | ------------------ |
| `String`   | Text               |
| `int`      | Number             |
| `boolean`  | Checkbox           |
| `String[]` | Multiple values    |

---

# Common Mistakes

### ❌ No default value

If a sensible default exists, provide one.

---

### ❌ Poor naming

Bad

```
Value1
```

Good

```
SMTP Host
```

---

### ❌ Using the wrong type

Bad

```java
String port();
```

Better

```java
int port();
```

---

# Interview Questions

### 1. What is `@AttributeDefinition`?

It defines a single configuration property inside an `@ObjectClassDefinition` interface.

---

### 2. Where is it used?

Inside an interface annotated with `@ObjectClassDefinition`.

---

### 3. Can it have default values?

**Yes.**

```java
int port() default 587;
```

---

### 4. Does `@AttributeDefinition` create a service?

**No.**

It only defines configuration metadata.

---

### 5. How does the service read these values?

Using:

```java
@Activate
@Modified
protected void activate(
    EmailConfig config
)
```

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do you create configurable fields for an OSGi service?"**

Answer:

1. Create an interface with `@ObjectClassDefinition`.
2. Add one `@AttributeDefinition` for each configuration property.
3. Connect the interface to the service using `@Designate`.
4. Read the values in an `@Activate`/`@Modified` method.

This is the standard enterprise AEM approach.

---

# OSGi Annotations Completed So Far

* ✅ `@Component`
* ✅ `@Reference`
* ✅ `@Activate`
* ✅ `@Deactivate`
* ✅ `@Modified`
* ✅ `@ObjectClassDefinition`
* ✅ `@AttributeDefinition`


---

# OSGi Annotation 8: `@Designate` ⭐⭐⭐⭐⭐

---

# What is `@Designate`?

`@Designate` links:

* An **OSGi Service** (`@Component`)
* An **OSGi Configuration Interface** (`@ObjectClassDefinition`)

Think of it as:

> **"This service should use this configuration."**

Without `@Designate`:

```text
EmailConfig

Exists

↓

EmailService

Exists

↓

No Connection
```

With `@Designate`:

```text
EmailConfig

↓

@Designate

↓

EmailService
```

Now the service receives configuration values automatically.

---

# Why do we need `@Designate`?

Suppose you create:

```java
@ObjectClassDefinition
public @interface EmailConfig {

    String host();

}
```

And a service:

```java
@Component(service = EmailService.class)
public class EmailServiceImpl {

}
```

Will the service receive the configuration?

❌ **No.**

You must connect them:

```java
@Designate(
    ocd = EmailConfig.class
)
```

---

# Internal Working

```text
Developer

↓

@ObjectClassDefinition

↓

@Designate

↓

@Component

↓

AEM Configuration Manager

↓

Administrator Saves Values

↓

@Activate

↓

Service Uses Configuration
```

---

# Basic Syntax

```java
@Component(service = EmailService.class)

@Designate(
    ocd = EmailConfig.class
)

public class EmailServiceImpl {

}
```

---

# Parameter: `ocd`

```java
@Designate(
    ocd = EmailConfig.class
)
```

`ocd` means:

> **Object Class Definition**

It specifies which configuration interface the service should use.

---

# Complete Working Example

## Step 1 – Configuration Interface

```java
package com.mysite.core.config;

import org.osgi.service.metatype.annotations.*;

@ObjectClassDefinition(
    name = "Email Configuration"
)
public @interface EmailConfig {

    @AttributeDefinition(
        name = "SMTP Host"
    )
    String host() default "smtp.gmail.com";

    @AttributeDefinition(
        name = "SMTP Port"
    )
    int port() default 587;
}
```

---

## Step 2 – Service

```java
package com.mysite.core.services.impl;

@Component(service = EmailService.class)

@Designate(
    ocd = EmailConfig.class
)

public class EmailServiceImpl
implements EmailService {

    private String host;

    private int port;

    @Activate
    @Modified
    protected void activate(
            EmailConfig config){

        host = config.host();

        port = config.port();

    }

}
```

---

## Step 3 – Configuration Screen

Open:

```text
/system/console/configMgr
```

You will see:

```text
Email Configuration

SMTP Host

smtp.gmail.com

SMTP Port

587
```

---

# What Happens Internally?

```text
Bundle Starts
      │
      ▼
@Component Registered
      │
      ▼
@Designate Found
      │
      ▼
EmailConfig Linked
      │
      ▼
Configuration Loaded
      │
      ▼
@Activate
      │
      ▼
Service Ready
```

---

# Factory Configuration

Sometimes you need **multiple instances** of the same service.

Example:

```text
SMTP Server 1

smtp.gmail.com

SMTP Server 2

smtp.office365.com

SMTP Server 3

mail.company.com
```

Use:

```java
@Designate(
    ocd = EmailConfig.class,
    factory = true
)
```

Now AEM allows multiple configurations of the same service.

---

# Real Project Example 1 – Search Service

Configuration:

```text
Elastic Host

Elastic Port
```

Service:

```java
@Designate(
    ocd = SearchConfig.class
)
```

Administrator changes:

```text
localhost

↓

elastic.company.com
```

The service starts using the new server immediately.

---

# Real Project Example 2 – Scheduler

Configuration:

```text
Interval

30
```

Admin changes:

```text
5
```

Service reads:

```java
config.interval();
```

Scheduler now runs every **5 minutes**.

---

# Real Project Example 3 – Payment Gateway

Configuration:

```text
API URL

Merchant ID

Secret Key
```

Instead of hardcoding:

```java
String apiKey = "...";
```

Use:

```java
config.apiKey();
```

Now administrators can update credentials without changing code.

---

# `@Designate` vs `@ObjectClassDefinition`

| `@Designate`                   | `@ObjectClassDefinition`        |
| ------------------------------ | ------------------------------- |
| Used on service class          | Used on configuration interface |
| Links service to configuration | Defines configuration fields    |

---

# Complete Lifecycle

```text
Developer

↓

@ObjectClassDefinition

↓

@AttributeDefinition

↓

@Component

↓

@Designate

↓

Admin Configures

↓

@Activate

↓

Running

↓

@Modified

↓

Configuration Updated
```

---

# Best Practices

### ✅ One configuration interface per service

```text
EmailConfig

↓

EmailService
```

Avoid using one configuration interface for unrelated services.

---

### ✅ Use `@Activate` + `@Modified`

```java
@Activate
@Modified
protected void activate(
EmailConfig config){

}
```

This ensures configuration is loaded both at startup and after updates.

---

### ✅ Use `factory = true` only when multiple service instances are required

Examples:

* Multiple SMTP servers
* Multiple REST API endpoints
* Multiple scheduler jobs

---

# Common Mistakes

### ❌ Forgetting `@Designate`

```java
@Component
```

Only.

The service won't automatically receive the configuration interface.

---

### ❌ Hardcoding values

Bad:

```java
String host =
"smtp.gmail.com";
```

Better:

```java
config.host();
```

---

### ❌ Duplicating configuration interfaces

Each service should generally have its own dedicated configuration interface unless sharing is intentional.

---

# Interview Questions

### 1. What is `@Designate`?

It links an OSGi component with an `@ObjectClassDefinition` configuration interface.

---

### 2. Why do we use `@Designate`?

To allow an OSGi service to receive configuration values defined in an OSGi configuration interface.

---

### 3. What does `ocd` mean?

**Object Class Definition**.

It specifies which configuration interface belongs to the service.

---

### 4. What is `factory = true`?

It enables **factory configurations**, allowing multiple independent instances of the same service, each with its own configuration.

---

### 5. Can `@Designate` work without `@ObjectClassDefinition`?

**No.** `@Designate` must reference an interface annotated with `@ObjectClassDefinition`.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain the complete OSGi configuration flow in AEM."**

A strong answer is:

```text
1. Create a configuration interface using @ObjectClassDefinition.
2. Define configuration fields using @AttributeDefinition.
3. Create an OSGi service using @Component.
4. Link the service to the configuration using @Designate.
5. Read values in an @Activate/@Modified method.
6. Administrators update values through /system/console/configMgr without changing code.
```

This is exactly how configurable OSGi services are built in enterprise AEM applications.

---

# OSGi Configuration Flow (Complete)

```text
@ObjectClassDefinition
        │
        ▼
@AttributeDefinition
        │
        ▼
@Designate
        │
        ▼
@Component
        │
        ▼
@Activate / @Modified
        │
        ▼
Business Logic
```

---

## 🎉 OSGi Configuration Annotations Completed

You have now learned:

* ✅ `@Component`
* ✅ `@Reference`
* ✅ `@Activate`
* ✅ `@Deactivate`
* ✅ `@Modified`
* ✅ `@ObjectClassDefinition`
* ✅ `@AttributeDefinition`
* ✅ `@Designate`

These are the core OSGi annotations used in almost every enterprise AEM backend project.




---

# Chapter 3: AEM Servlets

# What is a Servlet? ⭐⭐⭐⭐⭐

---

# What is a Servlet?

A **Servlet** is a Java class that handles **HTTP requests** (GET, POST, PUT, DELETE) and sends an **HTTP response**.

Think of it as a **controller** in the MVC architecture.

```text
Browser
   │
   ▼
HTTP Request
   │
   ▼
AEM Servlet
   │
   ▼
Business Logic (OSGi Service)
   │
   ▼
HTTP Response (HTML / JSON / XML)
```

---

# Why do we use Servlets?

Use Servlets when you need to:

* Process forms
* Return JSON for AJAX calls
* Call external REST APIs
* Upload files
* Download files
* Perform CRUD operations
* Validate user input
* Integrate React/Angular applications

---

# Real Project Example

Imagine an e-commerce website.

When the user clicks:

```text
Add to Cart
```

The browser sends:

```http
POST /bin/cart
```

Servlet Flow:

```text
Browser
     │
     ▼
CartServlet
     │
     ▼
CartService
     │
     ▼
Repository / Database
     │
     ▼
JSON Response
```

---

# Servlet Lifecycle

```text
AEM Starts
      │
      ▼
Servlet Registered
      │
      ▼
Waiting for Requests
      │
      ▼
GET / POST Request
      │
      ▼
doGet() / doPost()
      │
      ▼
Business Logic
      │
      ▼
Response Sent
```

---

# Types of Servlets in AEM

## 1. Path-based Servlet

Example:

```text
/bin/search
```

Access:

```text
http://localhost:4502/bin/search
```

---

## 2. Resource Type Servlet ⭐⭐⭐⭐⭐

Example:

```text
mysite/components/page
```

Accessed through a component's resource type instead of a fixed URL.

**Adobe recommends Resource Type Servlets** because they fit naturally into Sling's resource-oriented architecture.

---

# Basic Servlet Example

```java
package com.mysite.core.servlets;

import java.io.IOException;

import javax.servlet.Servlet;

import org.osgi.service.component.annotations.Component;

import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

import org.apache.sling.api.SlingHttpServletRequest;

import org.apache.sling.api.SlingHttpServletResponse;

@Component(service = Servlet.class)
public class HelloServlet extends SlingSafeMethodsServlet {

    @Override
    protected void doGet(
            SlingHttpServletRequest request,
            SlingHttpServletResponse response)
            throws IOException {

        response.getWriter().write("Hello AEM");

    }

}
```

---

# Browser

```text
GET

↓

HelloServlet

↓

Hello AEM
```

Output

```text
Hello AEM
```

---

# HTTP Methods

| Method | Purpose     |
| ------ | ----------- |
| GET    | Read data   |
| POST   | Create data |
| PUT    | Update data |
| DELETE | Delete data |

Example:

```text
GET

↓

Read Product
```

```text
POST

↓

Create Product
```

```text
PUT

↓

Update Product
```

```text
DELETE

↓

Delete Product
```

---

# `SlingSafeMethodsServlet`

```java
public class DemoServlet
extends SlingSafeMethodsServlet
```

Supports:

* GET
* HEAD
* OPTIONS

Used when the servlet **does not modify data**.

---

# `SlingAllMethodsServlet`

```java
public class DemoServlet
extends SlingAllMethodsServlet
```

Supports:

* GET
* POST
* PUT
* DELETE

Used for CRUD operations.

---

# Difference

| SlingSafeMethodsServlet | SlingAllMethodsServlet    |
| ----------------------- | ------------------------- |
| Read-only operations    | Read and write operations |
| GET, HEAD               | GET, POST, PUT, DELETE    |

---

# Request & Response Objects

Inside a servlet:

```java
protected void doGet(
    SlingHttpServletRequest request,
    SlingHttpServletResponse response)
```

### Request

Contains:

* Parameters
* Headers
* Cookies
* URL
* Selectors
* Extension

Example:

```java
String name = request.getParameter("name");
```

---

### Response

Used to send data back.

```java
response.getWriter().write("Hello");
```

---

# Real Project Example

URL

```text
http://localhost:4502/bin/greet?name=Vijay
```

Servlet

```java
@Override
protected void doGet(
        SlingHttpServletRequest request,
        SlingHttpServletResponse response)
        throws IOException {

    String name =
        request.getParameter("name");

    response.getWriter().write(
        "Hello " + name
    );
}
```

Output

```text
Hello Vijay
```

---

# Best Practices

✅ Keep Servlets lightweight.

A Servlet should:

* Read the request.
* Call an OSGi Service.
* Return the response.

Business logic should stay in OSGi Services.

---

### Good Architecture

```text
Browser
    │
    ▼
Servlet
    │
    ▼
ProductService
    │
    ▼
Repository / API
```

---

### Bad Architecture

```text
Servlet

↓

1000 Lines

↓

Business Logic

↓

Repository Access

↓

REST Calls
```

---

# Common Mistakes

❌ Writing all business logic inside the Servlet.

❌ Accessing the repository directly everywhere instead of using services.

❌ Returning plain text when JSON is expected.

❌ Not validating request parameters.

---

# Interview Questions

### 1. What is a Servlet?

A Java class that processes HTTP requests and generates HTTP responses.

---

### 2. Why do we use Servlets in AEM?

To:

* Process HTTP requests.
* Build APIs.
* Handle forms.
* Return JSON.
* Integrate with frontend applications.

---

### 3. What is the difference between `SlingSafeMethodsServlet` and `SlingAllMethodsServlet`?

* `SlingSafeMethodsServlet` is for safe/read-only methods (GET, HEAD, OPTIONS).
* `SlingAllMethodsServlet` supports both read and write operations (GET, POST, PUT, DELETE).

---

### 4. What objects are available in `doGet()`?

* `SlingHttpServletRequest`
* `SlingHttpServletResponse`

---

### 5. Should business logic be written in a Servlet?

**No.** The Servlet should delegate business logic to OSGi Services.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"Explain the flow of a Servlet in AEM."**

A strong answer is:

```text
Browser
    ↓
HTTP Request
    ↓
Servlet (Controller)
    ↓
OSGi Service (Business Logic)
    ↓
Repository / External API
    ↓
Servlet creates Response
    ↓
Browser
```

This demonstrates a solid understanding of AEM's layered architecture.


---

# Chapter 4 - Servlet Annotation 1

# `@SlingServletResourceTypes` ⭐⭐⭐⭐⭐

---

# What is `@SlingServletResourceTypes`?

`@SlingServletResourceTypes` registers a servlet **for a resource type** instead of a fixed URL path.

Instead of saying:

> "Run this servlet when `/bin/test` is requested."

You say:

> "Run this servlet whenever a resource of type `mysite/components/page` is requested."

---

# Why is it Preferred?

Adobe recommends it because it follows **Sling's resource-based architecture**.

### Path-based Servlet

```text
URL
 │
 ▼
/bin/search
 │
 ▼
Servlet
```

### Resource Type Servlet

```text
Page
 │
 ▼
sling:resourceType
 │
 ▼
mysite/components/page
 │
 ▼
Servlet
```

It is more secure, reusable, and aligned with AEM's content model.

---

# Basic Syntax

```java
@Component(service = Servlet.class)

@SlingServletResourceTypes(

    resourceTypes = "mysite/components/page",

    methods = HttpConstants.METHOD_GET,

    extensions = "json"

)

public class PageServlet
extends SlingSafeMethodsServlet {

}
```

---

# Parameters

## 1. `resourceTypes`

This tells Sling:

> "Execute this servlet only for resources of this type."

Example:

```java
resourceTypes = "mysite/components/page"
```

Repository:

```text
/content/mysite/en

jcr:content

sling:resourceType = mysite/components/page
```

When this page is requested, Sling matches the resource type and invokes the servlet.

---

## 2. `methods`

Specifies which HTTP methods are supported.

Example:

```java
methods = HttpConstants.METHOD_GET
```

Other options:

```java
HttpConstants.METHOD_POST
```

```java
HttpConstants.METHOD_PUT
```

```java
HttpConstants.METHOD_DELETE
```

Or multiple methods:

```java
methods = {
    HttpConstants.METHOD_GET,
    HttpConstants.METHOD_POST
}
```

---

## 3. `extensions`

Specifies the URL extension.

Example:

```java
extensions = "json"
```

URL:

```text
/content/mysite/en/home.json
```

---

## 4. `selectors`

Selectors appear **between the page name and the extension**.

URL:

```text
/content/mysite/en/home.products.json
```

Here:

```text
Page

home

↓

Selector

products

↓

Extension

json
```

Servlet:

```java
selectors = "products"
```

---

# Complete Working Example

```java
package com.mysite.core.servlets;

import java.io.IOException;

import javax.servlet.Servlet;

import org.osgi.service.component.annotations.Component;

import org.apache.sling.api.servlets.HttpConstants;

import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

import org.apache.sling.api.SlingHttpServletRequest;

import org.apache.sling.api.SlingHttpServletResponse;

import org.apache.sling.servlets.annotations.SlingServletResourceTypes;

@Component(service = Servlet.class)

@SlingServletResourceTypes(

        resourceTypes = "mysite/components/page",

        selectors = "info",

        extensions = "json",

        methods = HttpConstants.METHOD_GET

)

public class PageInfoServlet
extends SlingSafeMethodsServlet {

    @Override
    protected void doGet(

            SlingHttpServletRequest request,

            SlingHttpServletResponse response)

            throws IOException {

        response.setContentType("application/json");

        response.getWriter().write(

                "{\"message\":\"Hello AEM\"}"

        );

    }

}
```

---

# URL

```text
http://localhost:4502/content/mysite/en/home.info.json
```

---

# Output

```json
{
  "message": "Hello AEM"
}
```

---

# Request Flow

```text
Browser
      │
      ▼
/content/mysite/en/home.info.json
      │
      ▼
Resource Resolver
      │
      ▼
Check sling:resourceType
      │
      ▼
mysite/components/page
      │
      ▼
@ResourceType Servlet
      │
      ▼
doGet()
      │
      ▼
JSON Response
```

---

# Real Project Example 1 - Product API

URL

```text
/content/store/products.list.json
```

Servlet

```java
@SlingServletResourceTypes(

resourceTypes="store/components/page",

selectors="list",

extensions="json"

)
```

Response

```json
[
   {
      "name":"Laptop",
      "price":65000
   },
   {
      "name":"Phone",
      "price":30000
   }
]
```

---

# Real Project Example 2 - Search API

URL

```text
/content/search.results.json?q=laptop
```

Servlet

```java
String keyword =
request.getParameter("q");
```

Calls:

```text
SearchService
```

Returns JSON.

---

# Real Project Example 3 - User Profile

URL

```text
/content/profile.details.json
```

Servlet

```java
selectors="details"
```

Returns:

```json
{
 "name":"Vijay",
 "country":"India"
}
```

---

# `@SlingServletResourceTypes` vs Path-based Servlet

| Resource Type Servlet           | Path-based Servlet            |
| ------------------------------- | ----------------------------- |
| Uses `resourceTypes`            | Uses `/bin/...` path          |
| Recommended by Adobe            | Use only when necessary       |
| Integrates with Sling resources | Fixed URL                     |
| More secure and flexible        | Simpler for utility endpoints |

---

# Best Practices

### ✅ Prefer Resource Type Servlets

Use:

```java
resourceTypes="mysite/components/page"
```

instead of exposing unnecessary `/bin` endpoints.

---

### ✅ Return proper JSON

```java
response.setContentType(
"application/json"
);
```

---

### ✅ Delegate business logic

Servlet

↓

ProductService

↓

Repository

Don't put repository or business logic directly into the servlet.

---

# Common Mistakes

### ❌ Forgetting the selector

If the servlet is registered with:

```java
selectors="info"
```

then requesting:

```text
/home.json
```

will **not** invoke it.

You must request:

```text
/home.info.json
```

---

### ❌ Wrong resource type

If the page has:

```text
sling:resourceType

foundation/components/page
```

but the servlet expects:

```text
mysite/components/page
```

it will not execute.

---

### ❌ Wrong extension

Servlet:

```java
extensions="json"
```

URL:

```text
/home.html
```

The servlet will not match.

---

# Interview Questions

### 1. What is `@SlingServletResourceTypes`?

It registers a servlet for one or more Sling resource types rather than a fixed path.

---

### 2. Why is it preferred over path-based servlets?

Because it aligns with Sling's resource-oriented architecture, is more flexible, and is the recommended approach in modern AEM development.

---

### 3. What are the important parameters?

* `resourceTypes`
* `selectors`
* `extensions`
* `methods`

---

### 4. Explain this URL:

```text
/content/mysite/en/home.info.json
```

* Resource: `/content/mysite/en/home`
* Selector: `info`
* Extension: `json`

---

### 5. Can a servlet support multiple HTTP methods?

**Yes.**

Example:

```java
methods = {
    HttpConstants.METHOD_GET,
    HttpConstants.METHOD_POST
}
```

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Which servlet type do you prefer in AEM?"**

A strong answer is:

> "I prefer **Resource Type Servlets** using `@SlingServletResourceTypes` because Adobe recommends them. They integrate with Sling's resource resolution, support selectors and extensions, and avoid exposing unnecessary `/bin` endpoints. I usually keep the servlet lightweight and delegate business logic to OSGi services."

This is the answer interviewers typically expect from an experienced AEM developer.


---

# Chapter 5 - Servlet Annotation 2

# `@SlingServletPaths` ⭐⭐⭐⭐⭐

---

# What is `@SlingServletPaths`?

`@SlingServletPaths` registers a servlet using a **fixed URL path**.

Instead of matching a resource type, Sling matches the request path.

Example:

```text
Browser
      │
      ▼
/bin/search
      │
      ▼
@Path Servlet
      │
      ▼
Response
```

---

# Why do we use `@SlingServletPaths`?

Use it when you need:

* Utility APIs
* AJAX endpoints
* External system integrations
* Health check endpoints
* Authentication APIs
* Login/Logout APIs
* Legacy AEM integrations

---

# Basic Syntax

```java
@Component(service = Servlet.class)

@SlingServletPaths("/bin/hello")

public class HelloServlet
extends SlingSafeMethodsServlet {

}
```

Now the servlet is available at:

```text
http://localhost:4502/bin/hello
```

---

# Complete Working Example

```java
package com.mysite.core.servlets;

import java.io.IOException;

import javax.servlet.Servlet;

import org.osgi.service.component.annotations.Component;

import org.apache.sling.api.SlingHttpServletRequest;

import org.apache.sling.api.SlingHttpServletResponse;

import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

import org.apache.sling.servlets.annotations.SlingServletPaths;

@Component(service = Servlet.class)

@SlingServletPaths("/bin/hello")

public class HelloServlet
extends SlingSafeMethodsServlet {

    @Override
    protected void doGet(

            SlingHttpServletRequest request,

            SlingHttpServletResponse response)

            throws IOException {

        response.getWriter().write("Hello AEM");

    }

}
```

---

# Browser

```text
GET

↓

http://localhost:4502/bin/hello

↓

HelloServlet

↓

Hello AEM
```

Output

```text
Hello AEM
```

---

# Example 2 – Request Parameters

URL

```text
http://localhost:4502/bin/greet?name=Vijay
```

Servlet

```java
@Component(service = Servlet.class)

@SlingServletPaths("/bin/greet")

public class GreetServlet
extends SlingSafeMethodsServlet {

    @Override
    protected void doGet(

            SlingHttpServletRequest request,

            SlingHttpServletResponse response)

            throws IOException {

        String name =
            request.getParameter("name");

        response.getWriter().write(

                "Hello " + name

        );

    }

}
```

Output

```text
Hello Vijay
```

---

# Example 3 – Returning JSON

```java
@Override
protected void doGet(

SlingHttpServletRequest request,

SlingHttpServletResponse response)

throws IOException {

response.setContentType(
"application/json"
);

response.getWriter().write(

"{\"status\":\"success\"}"

);

}
```

Output

```json
{
   "status":"success"
}
```

---

# Example 4 – POST Servlet

```java
@Component(service = Servlet.class)

@SlingServletPaths("/bin/register")

public class RegisterServlet
extends SlingAllMethodsServlet {

    @Override
    protected void doPost(

        SlingHttpServletRequest request,

        SlingHttpServletResponse response)

        throws IOException {

        String username =
                request.getParameter(
                        "username"
                );

        response.getWriter().write(

                "Registered : " + username

        );

    }

}
```

---

# Request Flow

```text
Browser

↓

POST /bin/register

↓

Servlet

↓

Read Parameters

↓

Call UserService

↓

Return Response
```

---

# Real Project Example 1 – Login API

URL

```text
POST

/bin/login
```

Request

```text
username=admin

password=admin123
```

Servlet

```java
@SlingServletPaths("/bin/login")
```

Calls

```text
AuthenticationService
```

Returns

```json
{
"success":true
}
```

---

# Real Project Example 2 – Search API

URL

```text
GET

/bin/search?q=laptop
```

Servlet

```java
String keyword =
request.getParameter("q");
```

Calls

```text
SearchService
```

Returns

```json
[
{
"name":"Laptop"
}
]
```

---

# Real Project Example 3 – Health Check

URL

```text
GET

/bin/health
```

Servlet

```java
@SlingServletPaths("/bin/health")
```

Output

```json
{
"status":"UP"
}
```

Monitoring tools use endpoints like this.

---

# Internal Flow

```text
Browser

↓

/bin/search

↓

Sling

↓

@Path Mapping

↓

Servlet

↓

OSGi Service

↓

Repository / API

↓

JSON Response
```

---

# `@SlingServletPaths` vs `@SlingServletResourceTypes`

| `@SlingServletPaths`                 | `@SlingServletResourceTypes`               |
| ------------------------------------ | ------------------------------------------ |
| Fixed URL (`/bin/...`)               | Based on `sling:resourceType`              |
| Good for utility APIs                | Best for page/component APIs               |
| Easier for external integrations     | Recommended for component-related requests |
| Doesn't depend on repository content | Uses Sling resource resolution             |

---

# Best Practices

### ✅ Keep Servlets Thin

Good architecture:

```text
Browser

↓

Servlet

↓

OSGi Service

↓

Repository
```

Avoid putting business logic directly in the servlet.

---

### ✅ Validate Request Parameters

```java
String name = request.getParameter("name");

if(name == null || name.isEmpty()){

    response.sendError(400, "Name is required");

    return;
}
```

---

### ✅ Return Proper Content Type

```java
response.setContentType("application/json");
response.setCharacterEncoding("UTF-8");
```

---

### ✅ Secure `/bin` Endpoints

Many `/bin` endpoints are directly accessible.

Consider:

* Authentication
* Authorization
* CSRF protection (for POST requests)
* Input validation

---

# Common Mistakes

### ❌ Writing business logic inside the servlet

Wrong:

```java
doGet(){

// Repository

// Database

// REST

// Validation

// Business Logic

}
```

Correct:

```text
Servlet

↓

Service

↓

Repository
```

---

### ❌ Forgetting Content Type

Wrong:

```java
response.getWriter().write(json);
```

Correct:

```java
response.setContentType("application/json");
```

---

### ❌ Not Validating Input

Wrong:

```java
String id =
request.getParameter("id");
```

Without checking for null or invalid values.

---

# Interview Questions

### 1. What is `@SlingServletPaths`?

It registers a servlet using one or more fixed URL paths.

---

### 2. When should you use it?

For:

* Utility endpoints
* External integrations
* AJAX APIs
* Health checks
* Legacy path-based APIs

---

### 3. Why does Adobe generally recommend Resource Type Servlets instead?

Because they integrate with Sling's resource-based architecture, are more flexible for AEM components, and avoid exposing unnecessary fixed endpoints.

---

### 4. Can you use multiple paths?

Yes.

```java
@SlingServletPaths({
    "/bin/search",
    "/bin/find"
})
```

---

### 5. Which servlet base class should you extend?

* `SlingSafeMethodsServlet` → GET, HEAD, OPTIONS
* `SlingAllMethodsServlet` → GET, POST, PUT, DELETE

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"When do you use a Path-Based Servlet instead of a Resource Type Servlet?"**

A good answer is:

> "I use **`@SlingServletResourceTypes`** for component- or page-related functionality because it's the recommended Sling approach. I use **`@SlingServletPaths`** for utility APIs, AJAX endpoints, health checks, or integrations with external systems that need a stable URL such as `/bin/search`."

This shows you understand the strengths of both approaches.

---

# Servlets Covered So Far

* ✅ What is a Servlet?
* ✅ `SlingSafeMethodsServlet`
* ✅ `SlingAllMethodsServlet`
* ✅ `@SlingServletResourceTypes`
* ✅ `@SlingServletPaths`

---

# Chapter 6 - Selectors & Extensions ⭐⭐⭐⭐⭐

---

# What is a Selector?

A **selector** is the part of the URL that comes **after the resource name** and **before the extension**.

Example URL:

```text
/content/mysite/en/home.print.json
```

Breakdown:

```text
/content/mysite/en/home.print.json

│
├── Resource Path
│   /content/mysite/en/home
│
├── Selector
│   print
│
└── Extension
    json
```

---

# What is an Extension?

The **extension** is the last part of the URL.

Example:

```text
/content/mysite/en/home.print.json
```

Extension:

```text
json
```

Other examples:

```text
html
json
xml
txt
pdf
```

---

# URL Structure in Sling

```text
/resource-path.selector1.selector2.extension/suffix
```

Example:

```text
/content/mysite/en/home.mobile.preview.json/content/dam/logo.png
```

Breakdown:

```text
Resource Path:
/content/mysite/en/home

Selector 1:
mobile

Selector 2:
preview

Extension:
json

Suffix:
/content/dam/logo.png
```

---

# Single Selector Example

Servlet

```java
@Component(service = Servlet.class)

@SlingServletResourceTypes(

resourceTypes = "mysite/components/page",

selectors = "product",

extensions = "json"

)

public class ProductServlet
extends SlingSafeMethodsServlet {

}
```

URL

```text
/content/mysite/en/home.product.json
```

Sling checks:

```text
Resource Type

↓

Selector

↓

Extension

↓

Servlet
```

---

# Multiple Selectors

URL

```text
/content/mysite/en/home.mobile.preview.json
```

Selectors

```text
mobile

preview
```

Retrieve them:

```java
String[] selectors =
request.getRequestPathInfo().getSelectors();
```

Output

```text
selectors[0] = mobile

selectors[1] = preview
```

---

# Getting the Extension

```java
String extension =
request.getRequestPathInfo()
       .getExtension();
```

Output

```text
json
```

---

# Getting the Resource Path

```java
String path =
request.getRequestPathInfo()
       .getResourcePath();
```

Output

```text
/content/mysite/en/home
```

---

# Complete Example

```java
@Component(service = Servlet.class)

@SlingServletResourceTypes(

resourceTypes = "mysite/components/page",

selectors = "info",

extensions = "json",

methods = HttpConstants.METHOD_GET

)

public class InfoServlet
extends SlingSafeMethodsServlet {

@Override

protected void doGet(

SlingHttpServletRequest request,

SlingHttpServletResponse response)

throws IOException {

String selector =
request.getRequestPathInfo()
.getSelectorString();

String extension =
request.getRequestPathInfo()
.getExtension();

response.getWriter().write(

"Selector : "
+ selector

+ "\nExtension : "
+ extension

);

}

}
```

---

# URL

```text
/content/mysite/en/home.info.json
```

Output

```text
Selector : info

Extension : json
```

---

# Multiple Selector Example

URL

```text
/content/mysite/en/home.mobile.preview.json
```

Java

```java
String[] selectors =
request.getRequestPathInfo()
.getSelectors();

for(String selector : selectors){

System.out.println(selector);

}
```

Output

```text
mobile

preview
```

---

# Real Project Example 1 – Mobile/Desktop Rendering

URL

```text
/content/mysite/en/home.mobile.html
```

Selector

```text
mobile
```

Servlet

```java
if(selectors[0].equals("mobile")){

// Return mobile data

}
```

---

# Real Project Example 2 – Product API

URL

```text
/content/store/products.list.json
```

Selector

```text
list
```

Output

```json
[
{
"id":1,
"name":"Laptop"
}
]
```

---

# Real Project Example 3 – Preview Mode

URL

```text
/content/mysite/en/home.preview.html
```

Selector

```text
preview
```

Logic

```text
Normal User

↓

Published Page

Editor

↓

Preview Page
```

---

# Internal Sling Resolution

```text
Browser Request
      │
      ▼
URL
      │
      ▼
Resource Path
      │
      ▼
Resource Type
      │
      ▼
Selector
      │
      ▼
Extension
      │
      ▼
Matching Servlet
      │
      ▼
Response
```

---

# RequestPathInfo API

```java
RequestPathInfo info =
request.getRequestPathInfo();
```

Useful methods:

```java
info.getResourcePath();
```

Returns:

```text
/content/mysite/en/home
```

---

```java
info.getSelectorString();
```

Returns:

```text
mobile.preview
```

---

```java
info.getSelectors();
```

Returns:

```text
mobile

preview
```

---

```java
info.getExtension();
```

Returns:

```text
json
```

---

```java
info.getSuffix();
```

Example URL

```text
/content/mysite/en/home.info.json/content/dam/logo.png
```

Returns

```text
/content/dam/logo.png
```

---

# Best Practices

### ✅ Use meaningful selectors

Good:

```text
preview

details

list

download

mobile
```

Avoid:

```text
abc

xyz

test
```

---

### ✅ Use JSON for APIs

Example:

```text
/products.list.json
```

---

### ✅ Use selectors instead of many `/bin` endpoints

Instead of:

```text
/bin/listProducts

/bin/getProducts

/bin/productDetails
```

Prefer:

```text
/Products.list.json

/Products.details.json
```

---

# Common Mistakes

### ❌ Confusing selector with extension

Wrong:

```text
home.json.print
```

Correct:

```text
home.print.json
```

---

### ❌ Wrong selector

Servlet

```java
selectors="details"
```

URL

```text
home.info.json
```

The servlet will **not** execute.

---

### ❌ Wrong extension

Servlet

```java
extensions="json"
```

URL

```text
home.info.html
```

The servlet won't match.

---

# Interview Questions

### 1. What is a selector?

A selector is the part of the URL between the resource name and the extension. It is used by Sling to select specific servlet behavior.

---

### 2. What is an extension?

The extension is the last part of the URL (such as `html`, `json`, or `xml`) and often represents the response format.

---

### 3. Can a URL have multiple selectors?

**Yes.**

Example:

```text
home.mobile.preview.json
```

Selectors:

* `mobile`
* `preview`

---

### 4. How do you get selectors?

```java
String[] selectors =
request.getRequestPathInfo()
.getSelectors();
```

---

### 5. How do you get the extension?

```java
String extension =
request.getRequestPathInfo()
.getExtension();
```

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"Explain this URL:"**

```text
/content/mysite/en/home.mobile.preview.json
```

You can answer:

* **Resource Path:** `/content/mysite/en/home`
* **Selectors:** `mobile`, `preview`
* **Extension:** `json`

This clearly demonstrates that you understand Sling URL decomposition and servlet resolution.

---

# What You've Learned in Servlets

* ✅ What is a Servlet?
* ✅ `SlingSafeMethodsServlet`
* ✅ `SlingAllMethodsServlet`
* ✅ `@SlingServletResourceTypes`
* ✅ `@SlingServletPaths`
* ✅ Selectors
* ✅ Extensions
* ✅ `RequestPathInfo`


---

# Chapter 7 - Request Parameters & JSON Responses ⭐⭐⭐⭐⭐

---

# What are Request Parameters?

Request parameters are values sent by the client (browser, frontend, Postman, or another service) to the servlet.

Example URL:

```text
http://localhost:4502/bin/search?q=laptop&page=1
```

Parameters:

```text
q = laptop
page = 1
```

---

# Types of Request Parameters

### 1. Query Parameters (GET)

URL:

```text
/bin/search?q=laptop&category=electronics
```

---

### 2. Form Parameters (POST)

Request Body:

```text
username=vijay

password=12345
```

---

### 3. Path Information

```text
/content/mysite/en/home.info.json
```

Contains:

* Resource Path
* Selectors
* Extension

---

# Reading One Parameter

```java
String keyword =
request.getParameter("q");
```

URL

```text
/bin/search?q=laptop
```

Output

```text
laptop
```

---

# Complete GET Example

```java
@Component(service = Servlet.class)

@SlingServletPaths("/bin/search")

public class SearchServlet
extends SlingSafeMethodsServlet {

    @Override
    protected void doGet(

            SlingHttpServletRequest request,

            SlingHttpServletResponse response)

            throws IOException {

        String keyword =
                request.getParameter("q");

        response.getWriter().write(

                "Searching : " + keyword

        );

    }

}
```

---

Browser

```text
/bin/search?q=laptop
```

Output

```text
Searching : laptop
```

---

# Reading Multiple Parameters

URL

```text
/bin/product?id=10&category=laptop
```

Java

```java
String id =
request.getParameter("id");

String category =
request.getParameter("category");
```

Output

```text
10

laptop
```

---

# Reading All Parameters

```java
Map<String,String[]> params =
request.getParameterMap();

for(String key : params.keySet()){

    System.out.println(key);

}
```

Output

```text
id

category

page
```

---

# Validating Parameters

Always validate input.

```java
String name =
request.getParameter("name");

if(name == null || name.isEmpty()){

    response.sendError(

            400,

            "Name Required"

    );

    return;

}
```

---

# Reading POST Parameters

```java
@Override

protected void doPost(

SlingHttpServletRequest request,

SlingHttpServletResponse response)

throws IOException {

String username =
request.getParameter("username");

String password =
request.getParameter("password");

}
```

---

POST Request

```text
username=vijay

password=123
```

---

# Returning JSON

Always set Content-Type.

```java
response.setContentType(
"application/json"
);

response.setCharacterEncoding("UTF-8");
```

---

# Simple JSON Response

```java
response.getWriter().write(

"{\"status\":\"success\"}"

);
```

Output

```json
{
   "status":"success"
}
```

---

# Returning JSON Using Gson ⭐⭐⭐⭐⭐

**Gson** is commonly used in AEM projects.

Java Object

```java
public class Product {

    private String name;

    private int price;

}
```

Servlet

```java
Gson gson = new Gson();

Product product =
new Product();

product.setName("Laptop");

product.setPrice(65000);

String json =
gson.toJson(product);

response.setContentType(
"application/json"
);

response.getWriter().write(json);
```

Output

```json
{
   "name":"Laptop",
   "price":65000
}
```

---

# Returning List as JSON

```java
List<Product> products =
productService.getProducts();

String json =
new Gson().toJson(products);

response.getWriter().write(json);
```

Output

```json
[
   {
      "name":"Laptop"
   },
   {
      "name":"Phone"
   }
]
```

---

# HTTP Status Codes

```java
response.setStatus(200);
```

Success

---

```java
response.sendError(400);
```

Bad Request

---

```java
response.sendError(404);
```

Not Found

---

```java
response.sendError(500);
```

Server Error

---

# Complete Enterprise Example

Servlet

```java
@Component(service = Servlet.class)

@SlingServletPaths("/bin/product")

public class ProductServlet
extends SlingSafeMethodsServlet {

    @Reference
    private ProductService productService;

    @Override

    protected void doGet(

            SlingHttpServletRequest request,

            SlingHttpServletResponse response)

            throws IOException {

        String id =
                request.getParameter("id");

        if(id == null){

            response.sendError(
                    400,
                    "Product Id Required"
            );

            return;

        }

        Product product =
                productService.getProduct(id);

        String json =
                new Gson().toJson(product);

        response.setContentType(
                "application/json"
        );

        response.setCharacterEncoding("UTF-8");

        response.getWriter().write(json);

    }

}
```

---

Request

```text
GET

/bin/product?id=100
```

Flow

```text
Browser

↓

Servlet

↓

Read id

↓

ProductService

↓

Repository

↓

Product Object

↓

Gson

↓

JSON

↓

Browser
```

Output

```json
{
    "id":"100",
    "name":"Laptop",
    "price":65000
}
```

---

# Best Practices

### ✅ Validate request parameters

```java
if(id == null){

response.sendError(400);

return;

}
```

---

### ✅ Return JSON instead of plain text

Good

```json
{
"status":"success"
}
```

Avoid

```text
Success
```

---

### ✅ Keep business logic in OSGi services

```text
Servlet

↓

Service

↓

Repository
```

---

### ✅ Set proper response type

```java
response.setContentType(
"application/json"
);
```

---

### ✅ Use Gson or Jackson

Avoid building JSON manually.

Bad

```java
"{\"name\":\"Laptop\"}"
```

Good

```java
new Gson().toJson(product)
```

---

# Common Mistakes

### ❌ Not checking for null

Wrong

```java
String id =
request.getParameter("id");
```

Then using it without validation.

---

### ❌ Forgetting UTF-8

```java
response.setCharacterEncoding(
"UTF-8"
);
```

---

### ❌ Returning Java objects directly

Wrong

```java
response.getWriter().write(product);
```

Correct

```java
response.getWriter().write(

new Gson().toJson(product)

);
```

---

# Interview Questions

### 1. How do you read a request parameter?

```java
request.getParameter("id");
```

---

### 2. How do you return JSON?

```java
response.setContentType("application/json");

response.getWriter().write(json);
```

---

### 3. Which library is commonly used?

* **Gson**
* Jackson (also common in some projects)

---

### 4. Which HTTP status code is used for success?

```text
200 OK
```

---

### 5. Which status code indicates a bad request?

```text
400 Bad Request
```

---

### 6. Why should you validate request parameters?

To prevent:

* `NullPointerException`
* Invalid input
* Security issues
* Incorrect processing

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do you build a REST API in AEM?"**

A strong answer is:

1. Create a servlet using `@SlingServletResourceTypes` (preferred) or `@SlingServletPaths`.
2. Read request parameters using `request.getParameter()`.
3. Validate the input.
4. Call an OSGi service for business logic.
5. Convert the response object to JSON using Gson or Jackson.
6. Set `Content-Type` to `application/json`.
7. Return appropriate HTTP status codes (`200`, `400`, `404`, `500`).

This is the architecture used in most enterprise AEM projects.

---

# What You've Learned in Servlets

* ✅ Servlet Basics
* ✅ `SlingSafeMethodsServlet`
* ✅ `SlingAllMethodsServlet`
* ✅ `@SlingServletResourceTypes`
* ✅ `@SlingServletPaths`
* ✅ Selectors
* ✅ Extensions
* ✅ Request Parameters
* ✅ JSON Responses
* ✅ HTTP Status Codes

---
# Chapter 8 - Complete CRUD Operations in AEM ⭐⭐⭐⭐⭐

---

# What is CRUD?

CRUD stands for:

| Operation | HTTP Method | Purpose              |
| --------- | ----------- | -------------------- |
| Create    | POST        | Create new data      |
| Read      | GET         | Retrieve data        |
| Update    | PUT         | Update existing data |
| Delete    | DELETE      | Delete data          |

---

# Real Project Example

Suppose you're building an **E-Commerce Product API**.

The frontend (React/Angular/HTL) communicates with AEM.

```text
Frontend
      │
      ▼
Servlet
      │
      ▼
ProductService
      │
      ▼
JCR Repository / Database
      │
      ▼
JSON Response
```

---

# Project Structure

```text
com.mysite.core

├── models
│      Product.java
│
├── services
│      ProductService.java
│
├── services.impl
│      ProductServiceImpl.java
│
└── servlets
       ProductServlet.java
```

---

# Step 1: Product Model

```java
package com.mysite.core.models;

public class Product {

    private String id;
    private String name;
    private double price;

    public Product() {
    }

    public Product(String id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }
}
```

---

# Step 2: Product Service Interface

```java
package com.mysite.core.services;

import java.util.List;
import com.mysite.core.models.Product;

public interface ProductService {

    Product getProduct(String id);

    List<Product> getAllProducts();

    Product createProduct(Product product);

    Product updateProduct(Product product);

    boolean deleteProduct(String id);

}
```

---

# Step 3: Product Service Implementation

```java
package com.mysite.core.services.impl;

@Component(service = ProductService.class)

public class ProductServiceImpl
implements ProductService {

    @Override
    public Product getProduct(String id){

        return new Product(
                id,
                "Laptop",
                65000
        );

    }

    @Override
    public List<Product> getAllProducts(){

        return List.of(

                new Product("1","Laptop",65000),

                new Product("2","Phone",35000)

        );

    }

    @Override
    public Product createProduct(Product product){

        return product;

    }

    @Override
    public Product updateProduct(Product product){

        return product;

    }

    @Override
    public boolean deleteProduct(String id){

        return true;

    }

}
```

> **Note:** In a real enterprise project, these methods would interact with the JCR repository, a database, or an external API instead of returning hardcoded values.

---

# Step 4: Product Servlet

```java
@Component(service = Servlet.class)

@SlingServletPaths("/bin/product")

public class ProductServlet
extends SlingAllMethodsServlet {

    @Reference
    private ProductService productService;

    private final Gson gson = new Gson();

    // GET

    @Override
    protected void doGet(
            SlingHttpServletRequest request,
            SlingHttpServletResponse response)
            throws IOException {

        String id =
                request.getParameter("id");

        Product product =
                productService.getProduct(id);

        response.setContentType("application/json");

        response.getWriter().write(
                gson.toJson(product)
        );

    }

    // POST

    @Override
    protected void doPost(
            SlingHttpServletRequest request,
            SlingHttpServletResponse response)
            throws IOException {

        Product product =
                gson.fromJson(
                        request.getReader(),
                        Product.class
                );

        Product created =
                productService.createProduct(product);

        response.setContentType("application/json");

        response.getWriter().write(
                gson.toJson(created)
        );

    }

    // PUT

    @Override
    protected void doPut(
            SlingHttpServletRequest request,
            SlingHttpServletResponse response)
            throws IOException {

        Product product =
                gson.fromJson(
                        request.getReader(),
                        Product.class
                );

        Product updated =
                productService.updateProduct(product);

        response.setContentType("application/json");

        response.getWriter().write(
                gson.toJson(updated)
        );

    }

    // DELETE

    @Override
    protected void doDelete(
            SlingHttpServletRequest request,
            SlingHttpServletResponse response)
            throws IOException {

        String id =
                request.getParameter("id");

        boolean deleted =
                productService.deleteProduct(id);

        response.setContentType("application/json");

        response.getWriter().write(

                "{\"deleted\":"
                        + deleted
                        + "}"

        );

    }

}
```

---

# GET Request

Request

```http
GET /bin/product?id=101
```

Response

```json
{
   "id":"101",
   "name":"Laptop",
   "price":65000
}
```

---

# POST Request

Request

```http
POST /bin/product
```

Body

```json
{
    "id":"101",
    "name":"Laptop",
    "price":65000
}
```

Response

```json
{
    "id":"101",
    "name":"Laptop",
    "price":65000
}
```

---

# PUT Request

Request

```http
PUT /bin/product
```

Body

```json
{
    "id":"101",
    "name":"Gaming Laptop",
    "price":80000
}
```

Response

```json
{
    "id":"101",
    "name":"Gaming Laptop",
    "price":80000
}
```

---

# DELETE Request

Request

```http
DELETE /bin/product?id=101
```

Response

```json
{
    "deleted": true
}
```

---

# Complete Request Flow

```text
Browser / React App

↓

Servlet

↓

Read Request

↓

Validate Input

↓

ProductService

↓

JCR Repository / Database

↓

Product Object

↓

Gson

↓

JSON Response

↓

Browser
```

---

# Enterprise Architecture

```text
React / Angular

↓

AEM Servlet

↓

OSGi Service

↓

Repository Layer

↓

JCR / Database / External API
```

Each layer has a clear responsibility:

* **Servlet** → Handles HTTP requests and responses.
* **OSGi Service** → Contains business logic.
* **Repository/API Layer** → Reads and writes data.

---

# Best Practices

✅ Keep business logic in the service layer.

✅ Validate request parameters and request bodies.

✅ Return proper HTTP status codes:

```java
response.setStatus(HttpServletResponse.SC_OK);
```

or

```java
response.sendError(
    HttpServletResponse.SC_BAD_REQUEST,
    "Invalid Product Id"
);
```

✅ Use `Gson` or `Jackson` for JSON serialization.

---

# Common Mistakes

❌ Writing repository code directly inside the servlet.

❌ Returning plain text instead of structured JSON.

❌ Ignoring exceptions.

❌ Not validating input.

❌ Not setting the correct `Content-Type`.

---

# Interview Questions

### 1. Which servlet class should be used for CRUD operations?

```java
SlingAllMethodsServlet
```

because it supports:

* GET
* POST
* PUT
* DELETE

---

### 2. Where should business logic be written?

Inside an **OSGi Service**, not inside the servlet.

---

### 3. Which library is commonly used for JSON?

* Gson
* Jackson

---

### 4. Which HTTP method is used to create a resource?

```text
POST
```

---

### 5. Which HTTP method is used to update a resource?

```text
PUT
```

---

### 6. Which HTTP method is used to delete a resource?

```text
DELETE
```

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do you implement a REST API in AEM?"**

A strong answer is:

1. Create a servlet using `SlingAllMethodsServlet`.
2. Register it with `@SlingServletResourceTypes` (preferred) or `@SlingServletPaths`.
3. Read request parameters or JSON request bodies.
4. Validate the input.
5. Delegate business logic to an OSGi service.
6. Use Gson or Jackson to convert Java objects to JSON.
7. Return appropriate HTTP status codes and JSON responses.

This is the architecture used in enterprise AEM applications.

---

# What You've Completed

By now you've covered:

* ✅ Sling Model Annotations
* ✅ OSGi Annotations
* ✅ Servlet Basics
* ✅ Resource Type Servlets
* ✅ Path-Based Servlets
* ✅ Selectors & Extensions
* ✅ Request Parameters
* ✅ JSON Responses
* ✅ Complete CRUD REST API

---



# Chapter 9: AEM Filters ⭐⭐⭐⭐⭐

# What is a Filter?

A **Filter** is a Java component that **intercepts an HTTP request before it reaches a Servlet or HTL component** and can also intercept the **response before it goes back to the browser**.

Think of a filter as a **security checkpoint**.

```text
Browser
   │
   ▼
Filter
   │
   ▼
Servlet / HTL
   │
   ▼
Filter
   │
   ▼
Browser
```

The filter can:

* Allow the request
* Block the request
* Modify the request
* Modify the response
* Log request details

---

# Why do we use Filters?

Filters are commonly used for:

* Authentication
* Authorization
* Request Logging
* Performance Monitoring
* CORS Headers
* Response Compression
* Request Validation
* Security Headers

---

# Real Project Example

User opens:

```text
/content/mysite/en/home.html
```

Flow:

```text
Browser
    │
    ▼
Authentication Filter
    │
    ▼
Logging Filter
    │
    ▼
Servlet / HTL
    │
    ▼
Response
```

---

# Filter Lifecycle

```text
AEM Starts
      │
      ▼
@Component Registered
      │
      ▼
Filter Activated
      │
      ▼
Waiting for Requests
      │
      ▼
Request Received
      │
      ▼
doFilter()
      │
      ▼
Next Filter / Servlet
      │
      ▼
Response
```

---

# Basic Filter Example

```java
package com.mysite.core.filters;

import java.io.IOException;

import javax.servlet.*;
import org.osgi.service.component.annotations.Component;

@Component(
    service = Filter.class,
    property = {
        "sling.filter.scope=REQUEST"
    }
)
public class LoggingFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request,
                         ServletResponse response,
                         FilterChain chain)
            throws IOException, ServletException {

        System.out.println("Before Request");

        chain.doFilter(request, response);

        System.out.println("After Response");
    }
}
```

---

# Important Line

```java
chain.doFilter(request, response);
```

This passes the request to:

* Next Filter
* Servlet
* HTL Component

Without this line:

```text
Browser

↓

Filter

✖ Request Stops
```

The request never reaches the servlet.

---

# Execution Flow

```text
Browser

↓

Logging Filter

↓

Authentication Filter

↓

Servlet

↓

Authentication Filter

↓

Logging Filter

↓

Browser
```

---

# Understanding `chain.doFilter()`

Example

```java
@Override
public void doFilter(
        ServletRequest request,
        ServletResponse response,
        FilterChain chain)
throws IOException, ServletException {

    System.out.println("Before");

    chain.doFilter(request,response);

    System.out.println("After");
}
```

Console

```text
Before

Servlet Executed

After
```

This demonstrates that the filter runs both **before** and **after** the servlet.

---

# Filter Scope

AEM provides different scopes.

## REQUEST ⭐⭐⭐⭐⭐

```java
property={
"sling.filter.scope=REQUEST"
}
```

Runs for every incoming HTTP request.

Example:

```text
/home.html

/products.html

/search.json
```

---

## INCLUDE

Runs when one resource includes another.

---

## FORWARD

Runs when a request is forwarded internally.

---

## ERROR

Runs when an error page is rendered.

---

# Real Project Example 1 - Logging Filter

```java
@Override
public void doFilter(

ServletRequest request,

ServletResponse response,

FilterChain chain)

throws IOException,
ServletException {

long start =
System.currentTimeMillis();

chain.doFilter(request,response);

long end =
System.currentTimeMillis();

System.out.println(

"Time = "
+(end-start)

);

}
```

Output

```text
Time = 125 ms
```

Useful for performance monitoring.

---

# Real Project Example 2 - Authentication Filter

```java
String token =
request.getParameter("token");

if(token == null){

    ((HttpServletResponse)response)
        .sendError(401);

    return;

}

chain.doFilter(request,response);
```

If token is missing:

```text
401 Unauthorized
```

---

# Real Project Example 3 - Security Header

```java
HttpServletResponse resp =
(HttpServletResponse)response;

resp.addHeader(

"X-Frame-Options",

"DENY"

);

chain.doFilter(request,response);
```

Every response now contains:

```text
X-Frame-Options: DENY
```

This helps protect against clickjacking attacks.

---

# Filter Ranking

Suppose you have:

```text
Logging Filter

Authentication Filter

Compression Filter
```

Which runs first?

Use:

```java
service.ranking=100
```

Example

```java
@Component(

service=Filter.class,

property={

"service.ranking:Integer=100",

"sling.filter.scope=REQUEST"

}

)
```

Higher ranking generally executes earlier on the request path.

---

# Complete Flow

```text
Browser

↓

Filter 1

↓

Filter 2

↓

Filter 3

↓

Servlet

↓

HTL

↓

Browser
```

---

# Best Practices

### ✅ Always call `chain.doFilter()`

Unless you intentionally want to stop the request (for example, due to failed authentication).

---

### ✅ Keep filters lightweight

Filters should perform quick operations.

Heavy business logic belongs in OSGi Services.

---

### ✅ Use filters only when every request needs the logic

Examples:

* Logging
* Security
* Authentication

Not:

* Product Search
* Payment Processing

---

# Common Mistakes

### ❌ Forgetting `chain.doFilter()`

The request stops.

---

### ❌ Writing business logic in filters

Wrong

```text
Filter

↓

Database

↓

Repository

↓

REST

↓

Business Logic
```

---

### ❌ Heavy processing

Don't load thousands of records in a filter.

Filters run on many requests, so slow filters affect the entire application.

---

# Interview Questions

### 1. What is a Filter?

A Filter intercepts HTTP requests and responses to perform cross-cutting concerns such as logging, authentication, or header manipulation.

---

### 2. When is a Filter executed?

Before the request reaches the Servlet or HTL, and again after processing when the response returns.

---

### 3. What is the purpose of `chain.doFilter()`?

It passes the request to the next filter or target resource. Without it, processing stops.

---

### 4. What is the most commonly used filter scope?

```text
REQUEST
```

---

### 5. Where should business logic be written?

Inside **OSGi Services**, not inside Filters.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"Explain the request flow in AEM with Filters."**

A strong answer is:

```text
Browser
     ↓
Request Filter(s)
     ↓
Servlet / Sling Model / HTL
     ↓
Response Filter(s)
     ↓
Browser
```

Filters are ideal for **cross-cutting concerns** such as security, logging, and request/response modification, while business logic should remain in services.

---



# Chapter 10: AEM Scheduler ⭐⭐⭐⭐⭐

---

# What is an AEM Scheduler?

An **AEM Scheduler** is an OSGi component that executes a task **automatically** based on a schedule.

Think of it like an alarm clock.

```text
Time Arrives
      │
      ▼
Scheduler Starts
      │
      ▼
Runs Java Code
      │
      ▼
Task Completed
```

Unlike a Servlet, a Scheduler **does not wait for an HTTP request**.

---

# Why do we use Schedulers?

Common enterprise use cases:

* Generate reports every night
* Clear cache every hour
* Sync products from SAP
* Fetch data from external APIs
* Send scheduled emails
* Clean temporary files
* Archive logs

---

# Real Project Example

```text
12:00 AM

↓

Scheduler

↓

Read Product Data

↓

Call SAP API

↓

Update JCR Repository

↓

Finish
```

No user action is required.

---

# Scheduler Lifecycle

```text
AEM Starts
      │
      ▼
@Component Created
      │
      ▼
@Activate
      │
      ▼
Job Scheduled
      │
      ▼
Time Reached
      │
      ▼
run()
      │
      ▼
Task Finished
      │
      ▼
Repeat
```

---

# Basic Scheduler Example

```java
package com.mysite.core.schedulers;

import org.osgi.service.component.annotations.Component;

@Component(
    service = Runnable.class,
    immediate = true,
    property = {
        "scheduler.expression=0 0/5 * * * ?",
        "scheduler.concurrent=false"
    }
)
public class ProductScheduler implements Runnable {

    @Override
    public void run() {

        System.out.println("Scheduler Executed");

    }

}
```

---

# Output

Every 5 minutes:

```text
Scheduler Executed
```

---

# Understanding `Runnable`

Every Scheduler implements:

```java
public class ProductScheduler
implements Runnable
```

The Scheduler framework automatically calls:

```java
run()
```

at the scheduled time.

---

# Cron Expression

```text
0 0/5 * * * ?
```

Meaning:

```text
Second   = 0

Minute   = Every 5 minutes

Hour     = Every hour

Day      = Every day

Month    = Every month

Week     = Any day
```

---

# Common Cron Expressions

| Expression      | Meaning              |
| --------------- | -------------------- |
| `0 * * * * ?`   | Every minute         |
| `0 0/5 * * * ?` | Every 5 minutes      |
| `0 0 * * * ?`   | Every hour           |
| `0 0 0 * * ?`   | Every midnight       |
| `0 0 12 * * ?`  | Every day at 12 PM   |
| `0 0 9 ? * MON` | Every Monday at 9 AM |

---

# Scheduler Properties

## scheduler.expression

```java
"scheduler.expression=0 0/10 * * * ?"
```

Runs every 10 minutes.

---

## scheduler.concurrent

```java
scheduler.concurrent=false
```

Meaning:

If the previous execution is still running,

❌ Don't start another one.

This prevents duplicate jobs.

---

# Real Project Example 1 – Cache Cleanup

```java
@Component(
service = Runnable.class,

property = {

"scheduler.expression=0 0 * * * ?",

"scheduler.concurrent=false"

}

)
public class CacheCleanupScheduler
implements Runnable {

@Override

public void run(){

System.out.println(
"Cleaning Cache..."
);

}

}
```

Runs every hour.

---

# Real Project Example 2 – Email Scheduler

```java
@Component(
service = Runnable.class
)
public class EmailScheduler
implements Runnable {

    @Reference
    private EmailService emailService;

    @Override
    public void run(){

        emailService.sendPendingEmails();

    }

}
```

Flow

```text
Scheduler

↓

EmailService

↓

SMTP Server

↓

Emails Sent
```

---

# Real Project Example 3 – Product Sync

```java
@Component(
service = Runnable.class
)
public class ProductSyncScheduler
implements Runnable {

    @Reference
    private ProductService productService;

    @Override
    public void run(){

        productService.syncProducts();

    }

}
```

Flow

```text
Scheduler

↓

SAP API

↓

ProductService

↓

JCR

↓

Updated Products
```

---

# Using OSGi Configuration

Instead of hardcoding:

```java
scheduler.expression=0 0 * * * ?
```

Create:

```java
@ObjectClassDefinition
public @interface SchedulerConfig{

    @AttributeDefinition(
            name="Cron Expression"
    )
    String scheduler_expression();

}
```

Service

```java
@Component(service = Runnable.class)

@Designate(
ocd=SchedulerConfig.class
)
```

Read

```java
@Activate

@Modified

protected void activate(
SchedulerConfig config){

}
```

Now administrators can change the schedule from the OSGi Configuration Manager without changing code.

---

# Internal Flow

```text
AEM Starts

↓

Scheduler Registered

↓

Cron Expression Read

↓

Waiting

↓

Time Reached

↓

run()

↓

Business Logic

↓

Complete

↓

Wait Again
```

---

# Best Practices

### ✅ Keep Scheduler Lightweight

Good

```text
Scheduler

↓

ProductService

↓

Repository
```

Avoid putting all business logic directly into the scheduler.

---

### ✅ Use `scheduler.concurrent=false`

This prevents overlapping executions.

---

### ✅ Log Execution

```java
LOG.info("Scheduler Started");
```

Useful for debugging.

---

### ✅ Handle Exceptions

```java
@Override
public void run(){

    try{

        productService.syncProducts();

    }catch(Exception e){

        LOG.error(
            "Scheduler Failed",
            e
        );

    }

}
```

A scheduler should not stop permanently because of one exception.

---

# Common Mistakes

### ❌ Heavy logic in `run()`

Move complex logic to an OSGi service.

---

### ❌ Forgetting `scheduler.concurrent=false`

Multiple executions can overlap if one run takes longer than the interval.

---

### ❌ Hardcoding cron expressions

Prefer OSGi configuration for schedules that administrators may need to change.

---

# Interview Questions

### 1. What is an AEM Scheduler?

An OSGi component that executes tasks automatically based on a configured schedule.

---

### 2. Which interface does it implement?

```java
Runnable
```

---

### 3. Which method is executed?

```java
run()
```

---

### 4. What is a cron expression?

A string that defines **when** the scheduler should execute.

Example:

```text
0 0 * * * ?
```

runs every hour.

---

### 5. Why use `scheduler.concurrent=false`?

To prevent a new execution from starting while the previous execution is still running.

---

### 6. Should business logic be inside the scheduler?

No.

The scheduler should trigger an OSGi service that contains the business logic.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do you create a Scheduler in AEM?"**

A strong answer is:

1. Create an OSGi component implementing `Runnable`.
2. Register it with `@Component(service = Runnable.class)`.
3. Configure the schedule using `scheduler.expression`.
4. Set `scheduler.concurrent=false` if overlapping runs should be avoided.
5. Place business logic in an OSGi service and call it from the `run()` method.
6. Prefer making the cron expression configurable using `@ObjectClassDefinition` and `@Designate`.

This is the pattern used in most enterprise AEM projects.

---

# What You've Completed So Far

You have now learned:

* ✅ Sling Models
* ✅ Sling Model Annotations
* ✅ OSGi Services
* ✅ OSGi Annotations
* ✅ Servlets
* ✅ CRUD APIs
* ✅ Filters
* ✅ AEM Scheduler

---

# Chapter 11: AEM Workflow ⭐⭐⭐⭐⭐

# What is an AEM Workflow?

An **AEM Workflow** is a sequence of automated steps that execute business logic on content or assets.

Think of it like a business process.

Example:

```text
Author uploads an image
        │
        ▼
Generate Thumbnail
        │
        ▼
Extract Metadata
        │
        ▼
Virus Scan
        │
        ▼
Approval
        │
        ▼
Publish Asset
```

AEM performs each step automatically.

---

# Real-Life Example

Imagine a company where a content author creates a new page.

Without Workflow:

```text
Author

↓

Manager

↓

Publisher

↓

Publish
```

Everything is manual.

With Workflow:

```text
Author Creates Page
         │
         ▼
Workflow Starts
         │
         ▼
Manager Approval
         │
         ▼
Legal Approval
         │
         ▼
Marketing Approval
         │
         ▼
Publish Automatically
```

---

# Why Do We Use Workflows?

Common enterprise use cases:

* Content Approval
* Asset Approval
* Image Processing
* PDF Processing
* Metadata Extraction
* Email Notifications
* Automatic Publishing
* Data Synchronization

---

# Workflow Components

An AEM Workflow consists of several parts:

```text
Workflow Model
      │
      ▼
Workflow Instance
      │
      ▼
Workflow Steps
      │
      ▼
Custom Process
      │
      ▼
Complete
```

---

# Workflow Terminology

## 1. Workflow Model

A **Workflow Model** is the blueprint.

Example:

```text
Upload Asset

↓

Thumbnail

↓

Approval

↓

Publish
```

It defines the sequence of steps.

---

## 2. Workflow Instance

When someone starts the workflow,

AEM creates a **Workflow Instance**.

Example

```text
Workflow Model

↓

Started on image1.jpg

↓

Workflow Instance Created
```

Every execution creates a new instance.

---

## 3. Workflow Step

Each block inside the workflow is a **Workflow Step**.

Example:

```text
Step 1

Generate Thumbnail

↓

Step 2

Approval

↓

Step 3

Publish
```

---

# Workflow Architecture

```text
Author
    │
    ▼
Workflow Model
    │
    ▼
Workflow Engine
    │
    ▼
Workflow Process
    │
    ▼
Repository
    │
    ▼
Complete
```

---

# Types of Workflow Steps

| Step Type           | Purpose                 |
| ------------------- | ----------------------- |
| Process Step        | Executes Java code      |
| Participant Step    | Human approval          |
| OR Split            | Conditional branching   |
| AND Split           | Parallel execution      |
| Dynamic Participant | Assign task dynamically |
| Dialog Step         | Collect user input      |

---

# Most Important Interface

Every custom workflow step implements:

```java
com.adobe.granite.workflow.exec.WorkflowProcess
```

This is the interface you'll use most often.

---

# WorkflowProcess Interface

```java
public interface WorkflowProcess {

    void execute(

        WorkItem workItem,

        WorkflowSession workflowSession,

        MetaDataMap metaDataMap

    ) throws WorkflowException;

}
```

The `execute()` method is called whenever the workflow reaches your custom process step.

---

# Understanding execute()

```java
@Override
public void execute(

WorkItem workItem,

WorkflowSession workflowSession,

MetaDataMap metaDataMap)

throws WorkflowException {

}
```

This method contains your custom business logic.

---

# Understanding the Parameters

## 1. WorkItem

Represents the **current workflow item**.

Example:

```java
WorkflowData data =
workItem.getWorkflowData();
```

It contains information about what is being processed.

---

## 2. WorkflowSession

Allows interaction with the workflow engine.

Example:

```java
workflowSession
```

Used to:

* Complete workflow actions
* Access workflow APIs
* Control workflow execution

---

## 3. MetaDataMap

Contains process arguments configured in the workflow model.

Example:

```java
String email =
metaDataMap.get(
"email",
String.class
);
```

If the process step is configured with:

```text
email=admin@company.com
```

then:

```java
metaDataMap.get("email", String.class)
```

returns:

```text
admin@company.com
```

---

# Complete Workflow Flow

```text
Author Uploads Asset

↓

Workflow Launcher

↓

Workflow Model Starts

↓

Custom Workflow Step

↓

execute()

↓

Business Logic

↓

Next Step

↓

Workflow Complete
```

---

# Real Project Example 1

## Image Upload

```text
Author Uploads Image

↓

Generate Thumbnail

↓

Add Watermark

↓

Store Metadata

↓

Publish
```

Each processing stage can be implemented as a custom workflow step.

---

# Real Project Example 2

## Content Approval

```text
Author

↓

Manager Approval

↓

Legal Approval

↓

Marketing Approval

↓

Publish
```

---

# Real Project Example 3

## Email Notification

```text
Page Approved

↓

Workflow

↓

Email Service

↓

Notification Sent
```

---

# Best Practices

### ✅ Keep workflow steps focused

One workflow process should do one job.

Example:

```text
Generate Thumbnail
```

Not:

```text
Thumbnail

+

Email

+

Database

+

REST

+

Publish
```

---

### ✅ Move business logic to OSGi Services

Workflow

↓

EmailService

↓

Notification

Don't write all logic inside `execute()`.

---

### ✅ Handle exceptions

```java
try{

    emailService.send();

}catch(Exception e){

    LOG.error(
        "Workflow Failed",
        e
    );

}
```

---

# Common Mistakes

### ❌ Heavy logic inside execute()

Instead:

```text
Workflow

↓

OSGi Service

↓

Repository
```

---

### ❌ Ignoring process arguments

Use:

```java
metaDataMap.get()
```

to read configurable values.

---

### ❌ Hardcoding values

Bad:

```java
String email =
"admin@gmail.com";
```

Good:

```java
metaDataMap.get(
"email",
String.class
);
```

---

# Interview Questions

### 1. What is an AEM Workflow?

An AEM Workflow automates a sequence of business steps for processing content or assets.

---

### 2. Which interface is implemented for a custom workflow process?

```java
WorkflowProcess
```

---

### 3. Which method is implemented?

```java
execute()
```

---

### 4. What are the parameters of execute()?

* `WorkItem`
* `WorkflowSession`
* `MetaDataMap`

---

### 5. What is the purpose of `MetaDataMap`?

It provides access to workflow process arguments configured in the workflow model.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain the execution flow of an AEM Workflow."**

A strong answer is:

```text
User Action (Upload/Create Page)
        ↓
Workflow Launcher (Optional)
        ↓
Workflow Model
        ↓
Workflow Engine
        ↓
Custom Workflow Process
        ↓
execute() Method
        ↓
OSGi Service
        ↓
Repository / External API
        ↓
Next Workflow Step
        ↓
Workflow Complete
```

This shows that you understand both the AEM workflow engine and how custom Java code fits into the process.


---

# Chapter 12 - Custom Workflow Process ⭐⭐⭐⭐⭐

---

# What is a Custom Workflow Process?

A **Custom Workflow Process** is a Java class that implements:

```java
com.adobe.granite.workflow.exec.WorkflowProcess
```

It allows you to execute custom Java code during workflow execution.

For example:

* Send an email
* Update JCR content
* Generate thumbnails
* Call external REST APIs
* Validate content
* Publish pages
* Generate reports

---

# Workflow Execution Flow

```text
Author Uploads Asset
        │
        ▼
Workflow Starts
        │
        ▼
Custom Workflow Process
        │
        ▼
execute()
        │
        ▼
OSGi Service
        │
        ▼
Repository / REST API
        │
        ▼
Next Workflow Step
```

---

# Step 1: Create the Workflow Process

```java
package com.mysite.core.workflow;

import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.granite.workflow.WorkflowException;

import org.osgi.service.component.annotations.Component;

@Component(
    service = WorkflowProcess.class,
    property = {
        "process.label=Product Approval Process"
    }
)
public class ProductApprovalProcess
implements WorkflowProcess {

    @Override
    public void execute(

            WorkItem workItem,

            WorkflowSession workflowSession,

            MetaDataMap metaDataMap)

            throws WorkflowException {

    }

}
```

---

# Understanding `process.label`

```java
@Component(
service = WorkflowProcess.class,

property={
"process.label=Product Approval Process"
}
)
```

This label appears in the Workflow Model editor.

Example:

```text
Process Step

↓

Product Approval Process
```

When configuring a Process Step, you'll see this label in the dropdown.

---

# Understanding execute()

```java
@Override
public void execute(

WorkItem workItem,

WorkflowSession workflowSession,

MetaDataMap metaDataMap)

throws WorkflowException{

}
```

This method is called automatically when the workflow reaches your custom process.

---

# Step 2: Get Workflow Data

```java
WorkflowData workflowData =
workItem.getWorkflowData();
```

This gives access to the workflow payload.

---

# Step 3: Read Payload

```java
String path =
workflowData.getPayload().toString();
```

Suppose an author uploads:

```text
/content/dam/mysite/image.jpg
```

Output

```text
/content/dam/mysite/image.jpg
```

The payload is usually:

* Page path
* Asset path
* Content path

depending on the workflow.

---

# Step 4: Get ResourceResolver

```java
Session session =
workflowSession.adaptTo(Session.class);

ResourceResolver resolver =
workflowSession.adaptTo(
ResourceResolver.class
);
```

Now you can access the JCR repository.

---

# Step 5: Read Resource

```java
Resource resource =
resolver.getResource(path);
```

Example

Payload

```text
/content/mysite/en/home
```

Resource

```text
Page Resource
```

---

# Step 6: Update Content

Example

```java
ModifiableValueMap map =
resource.adaptTo(
ModifiableValueMap.class
);

map.put(
"approved",
true
);

resolver.commit();
```

The page now contains:

```text
approved = true
```

---

# Complete Workflow Process

```java
@Component(
service = WorkflowProcess.class,

property={
"process.label=Approve Content"
}
)
public class ApproveContentProcess
implements WorkflowProcess {

    @Override

    public void execute(

            WorkItem workItem,

            WorkflowSession workflowSession,

            MetaDataMap metaDataMap)

            throws WorkflowException {

        WorkflowData workflowData =
                workItem.getWorkflowData();

        String path =
                workflowData
                        .getPayload()
                        .toString();

        ResourceResolver resolver =
                workflowSession
                        .adaptTo(
                                ResourceResolver.class
                        );

        Resource resource =
                resolver.getResource(path);

        if(resource != null){

            ModifiableValueMap map =
                    resource.adaptTo(
                            ModifiableValueMap.class
                    );

            map.put(
                    "approved",
                    true
            );

            resolver.commit();

        }

    }

}
```

---

# Reading Process Arguments

Suppose the Workflow Model is configured with:

```text
approvalStatus=Approved
email=admin@company.com
```

Read them:

```java
String status =
metaDataMap.get(
"approvalStatus",
String.class
);

String email =
metaDataMap.get(
"email",
String.class
);
```

Output

```text
Approved

admin@company.com
```

This allows administrators to configure the process without changing code.

---

# Calling an OSGi Service

Never put all business logic in `execute()`.

```java
@Reference
private EmailService emailService;

@Override
public void execute(...) {

    emailService.sendApprovalMail();

}
```

Good architecture:

```text
Workflow

↓

EmailService

↓

SMTP

↓

Mail Sent
```

---

# Real Project Example 1 – Page Approval

```text
Author Creates Page

↓

Workflow Starts

↓

Manager Approves

↓

Custom Workflow

↓

approved=true

↓

Publish
```

---

# Real Project Example 2 – DAM Asset Processing

```text
Image Uploaded

↓

Workflow

↓

Generate Thumbnail

↓

Extract Metadata

↓

Store Metadata

↓

Complete
```

---

# Real Project Example 3 – REST Integration

```text
Workflow

↓

ProductService

↓

REST API

↓

SAP

↓

Update Repository
```

---

# Complete Architecture

```text
Workflow Model

↓

Workflow Process

↓

execute()

↓

OSGi Service

↓

Repository / REST API

↓

Commit

↓

Next Step
```

---

# Best Practices

### ✅ Keep `execute()` Small

Only:

* Read payload
* Read arguments
* Call service

---

### ✅ Use OSGi Services

Instead of:

```text
execute()

↓

1000 lines
```

Use:

```text
execute()

↓

ProductService

↓

Repository
```

---

### ✅ Handle Exceptions

```java
try{

// business logic

}catch(Exception e){

throw new WorkflowException(e);

}
```

---

### ✅ Commit Changes Carefully

```java
resolver.commit();
```

Only commit when changes are required.

---

# Common Mistakes

### ❌ Hardcoding Paths

Bad

```java
String path =
"/content/test";
```

Good

```java
workflowData
.getPayload()
```

---

### ❌ Business Logic Inside execute()

Move business logic into reusable OSGi services.

---

### ❌ Ignoring Process Arguments

Use:

```java
metaDataMap.get()
```

instead of hardcoded values.

---

# Interview Questions

### 1. Which interface is implemented for a custom workflow process?

```java
WorkflowProcess
```

---

### 2. Which method contains the business entry point?

```java
execute()
```

---

### 3. How do you get the payload path?

```java
String path =
workItem
.getWorkflowData()
.getPayload()
.toString();
```

---

### 4. How do you read process arguments?

```java
metaDataMap.get(
"name",
String.class
);
```

---

### 5. Where should business logic be written?

In **OSGi Services**, called from the workflow process.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"Explain how you build a custom workflow process in AEM."**

A strong answer is:

1. Create an OSGi component implementing `WorkflowProcess`.
2. Register it using `@Component(service = WorkflowProcess.class)` with a `process.label`.
3. Implement the `execute()` method.
4. Read the workflow payload using `workItem.getWorkflowData().getPayload()`.
5. Read configurable process arguments from `MetaDataMap`.
6. Adapt the `WorkflowSession` to a `ResourceResolver` or `Session` if repository access is needed.
7. Delegate business logic to OSGi services.
8. Commit repository changes only when necessary and handle exceptions appropriately.

This is the workflow process pattern used in enterprise AEM projects.

 

---

# Chapter 13 - Workflow Launcher ⭐⭐⭐⭐⭐

---

# What is a Workflow Launcher?

A **Workflow Launcher** is an AEM configuration that **automatically starts a workflow** when a specific repository event occurs.

Think of it as an **automatic trigger**.

Instead of:

```text
Author Uploads Asset

↓

Click Start Workflow
```

Use:

```text
Author Uploads Asset

↓

Workflow Launcher Detects Event

↓

Workflow Starts Automatically
```

---

# Why do we use Workflow Launchers?

Workflow Launchers eliminate manual work.

Common use cases:

* Start workflow when an asset is uploaded
* Start approval when a page is modified
* Generate thumbnails automatically
* Extract metadata
* Notify reviewers
* Auto-publish content

---

# Real Project Example

Author uploads:

```text
/content/dam/mysite/logo.png
```

Workflow Launcher detects:

```text
Node Created

↓

DAM Update Asset Workflow

↓

Thumbnail Created

↓

Metadata Extracted

↓

Asset Ready
```

No user action is required.

---

# Internal Architecture

```text
Repository Event
        │
        ▼
Workflow Launcher
        │
        ▼
Check Path
        │
        ▼
Check Node Type
        │
        ▼
Check Event
        │
        ▼
Start Workflow
```

---

# Workflow Launcher Configuration

In AEM:

```text
Tools

↓

Workflow

↓

Launchers
```

You can create or edit launchers here.

---

# Main Configuration Fields

A Workflow Launcher typically contains:

| Property       | Purpose                    |
| -------------- | -------------------------- |
| Workflow Model | Which workflow to start    |
| Path           | Where to monitor           |
| Node Type      | Which node type to watch   |
| Event          | Created, Modified, Deleted |
| Condition      | Optional filtering         |
| Enabled        | Enable/Disable launcher    |

---

# Path

Example:

```text
/content/mysite
```

Meaning:

Monitor everything under:

```text
/content/mysite
```

If content changes outside this path:

```text
/content/we-retail
```

The launcher does **not** start.

---

# Node Type

Example:

```text
cq:PageContent
```

Meaning:

Only page content nodes trigger the workflow.

For assets:

```text
dam:Asset
```

---

# Event Types

### Created

Starts workflow when a node is created.

Example:

```text
New Page Created

↓

Workflow Starts
```

---

### Modified ⭐⭐⭐⭐⭐

Starts workflow whenever content changes.

Example:

```text
Author Edits Page

↓

Workflow Starts
```

---

### Deleted

Starts workflow before or during deletion events (depending on the configuration and implementation).

Example:

```text
Asset Deleted

↓

Cleanup Workflow
```

---

# Complete Example

Configuration:

```text
Workflow Model:
Content Approval

Path:
/content/mysite

Node Type:
cq:PageContent

Event:
Modified

Enabled:
Yes
```

Flow:

```text
Author Updates Page

↓

Repository Event

↓

Workflow Launcher

↓

Content Approval Workflow

↓

Manager Approval

↓

Publish
```

---

# Real Project Example 1 – DAM Asset Processing

Configuration

```text
Path:
/content/dam

Node Type:
dam:Asset

Event:
Created
```

Flow

```text
Upload Image

↓

DAM Update Asset Workflow

↓

Thumbnail

↓

Metadata

↓

Smart Tags

↓

Complete
```

---

# Real Project Example 2 – Content Approval

Configuration

```text
Path:
/content/mysite

Event:
Modified
```

Flow

```text
Author Updates Page

↓

Workflow Starts

↓

Manager Approval

↓

Legal Approval

↓

Publish
```

---

# Real Project Example 3 – Product Sync

Configuration

```text
Path:
/content/products
```

Workflow

```text
Product Updated

↓

Workflow

↓

REST API

↓

SAP

↓

Update Search Index
```

---

# Launcher Execution Flow

```text
Repository Change

↓

Workflow Launcher

↓

Workflow Model

↓

Workflow Process

↓

execute()

↓

OSGi Service

↓

Repository

↓

Complete
```

---

# Conditions

You can define conditions to control when a launcher runs.

Example:

Only trigger if:

```text
status=draft
```

Ignore:

```text
status=published
```

This prevents unnecessary workflow executions.

---

# Best Practices

### ✅ Monitor only required paths

Good:

```text
/content/mysite
```

Avoid:

```text
/
```

Monitoring the entire repository can reduce performance.

---

### ✅ Use specific node types

Good:

```text
cq:PageContent
```

Instead of monitoring every node.

---

### ✅ Use conditions

Example:

```text
Only if page template = Article
```

This reduces unnecessary workflow starts.

---

### ✅ Keep workflows efficient

Workflow Launcher

↓

Workflow

↓

OSGi Service

↓

Repository

Avoid putting heavy business logic directly in the workflow process.

---

# Common Mistakes

### ❌ Monitoring the entire repository

```text
/
```

This can trigger workflows far too often.

---

### ❌ Wrong node type

Example:

```text
dam:Asset
```

while monitoring page content.

The workflow won't start.

---

### ❌ Wrong event

Configured:

```text
Created
```

Expected:

```text
Modified
```

The workflow won't execute on edits.

---

# Interview Questions

### 1. What is a Workflow Launcher?

A configuration that automatically starts a workflow when specific repository events occur.

---

### 2. Where do you configure Workflow Launchers?

```text
Tools

↓

Workflow

↓

Launchers
```

---

### 3. Which events are commonly used?

* Created
* Modified
* Deleted

---

### 4. What is the purpose of the Path?

It defines which part of the repository the launcher monitors.

---

### 5. What is the purpose of the Node Type?

It limits workflow execution to specific node types such as:

* `cq:PageContent`
* `dam:Asset`

---

### 6. Can a Workflow Launcher start a custom workflow?

**Yes.**

It can start any workflow model, including models containing your custom `WorkflowProcess` steps.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do you automatically start a workflow when a page is modified?"**

A strong answer is:

1. Create a Workflow Model.
2. Add your custom `WorkflowProcess` step(s) if needed.
3. Create a Workflow Launcher.
4. Configure:

   * **Path:** `/content/mysite`
   * **Node Type:** `cq:PageContent`
   * **Event:** `Modified`
5. Enable the launcher.

Now, whenever a page under `/content/mysite` is modified, AEM automatically starts the workflow without any manual action.

---

# Workflow Topics Completed

You have now learned:

* ✅ What is a Workflow?
* ✅ Workflow Model
* ✅ Workflow Instance
* ✅ Workflow Steps
* ✅ `WorkflowProcess`
* ✅ `execute()`
* ✅ `WorkItem`
* ✅ `WorkflowSession`
* ✅ `MetaDataMap`
* ✅ Custom Workflow Process
* ✅ Workflow Launcher



---

# Chapter 14: JCR (Java Content Repository) ⭐⭐⭐⭐⭐

---

# What is JCR?

**JCR (Java Content Repository)** is a **hierarchical content repository** used to store and manage all content in AEM.

It is similar to a file system but much more powerful.

Think of it like this:

```text
Computer File System

C:
 ├── Documents
 ├── Images
 └── Videos
```

AEM Repository

```text
/content
    ├── mysite
    ├── we-retail
    └── experience-fragments
```

Everything in AEM is stored as **Nodes** and **Properties**.

---

# Why Does AEM Use JCR?

Instead of storing data in traditional database tables:

```text
Employee Table

ID | Name | Salary
```

AEM stores data as a tree.

Example:

```text
/content

    mysite

        en

            home

                jcr:content

                    jcr:title = Home Page

                    sling:resourceType = mysite/components/page
```

This structure is ideal for websites because pages naturally form a hierarchy.

---

# JCR Architecture

```text
Browser
      │
      ▼
Servlet / Sling Model
      │
      ▼
ResourceResolver
      │
      ▼
JCR Repository
      │
      ▼
Oak Repository
```

---

# What is Apache Jackrabbit Oak?

AEM uses **Apache Jackrabbit Oak** as its JCR implementation.

```text
AEM

↓

JCR API

↓

Apache Jackrabbit Oak

↓

Repository
```

You write JCR code using standard APIs, while Oak manages storage and indexing internally.

---

# JCR Hierarchy

Example:

```text
/

├── apps
├── libs
├── content
│      └── mysite
│            └── en
│                  └── home
│                        └── jcr:content
├── conf
├── var
├── etc
└── content/dam
```

---

# Important Repository Folders

| Path           | Purpose                             |
| -------------- | ----------------------------------- |
| `/content`     | Website pages                       |
| `/content/dam` | Assets (images, PDFs, videos)       |
| `/apps`        | Custom application code             |
| `/libs`        | Adobe product code (do not modify)  |
| `/conf`        | Editable templates & configurations |
| `/var`         | Workflow and system data            |
| `/home`        | User information                    |

---

# Example Website Structure

```text
/content

   mysite

      en

         home

         about

         contact

         products
```

Each page is a node.

---

# Node

A **Node** is the basic building block of JCR.

Example:

```text
home
```

is a node.

Another example:

```text
products
```

is another node.

---

# Property

A property stores data inside a node.

Example:

```text
home

    jcr:title = Home

    sling:resourceType = mysite/components/page

    cq:lastModified = 2026-06-27
```

Here:

* `home` → Node
* `jcr:title` → Property
* `sling:resourceType` → Property

---

# Visual Example

```text
home (Node)

├── jcr:title = Home Page

├── sling:resourceType = mysite/components/page

├── cq:lastModified = 2026-06-27

└── root (Child Node)
```

---

# Child Nodes

Nodes can contain child nodes.

Example:

```text
home

    jcr:content

        root

            responsivegrid

                text

                image

                carousel
```

Each component is itself a node.

---

# Primary Type

Every node has a **Primary Type**.

Examples:

```text
cq:Page

cq:PageContent

nt:unstructured

dam:Asset
```

Example:

```text
home

jcr:primaryType = cq:Page
```

---

# Common Node Types

| Node Type         | Purpose               |
| ----------------- | --------------------- |
| `cq:Page`         | Represents a page     |
| `cq:PageContent`  | Stores page content   |
| `nt:unstructured` | Flexible content node |
| `dam:Asset`       | Digital Asset         |
| `sling:Folder`    | Folder                |

---

# Example Page

```text
home

jcr:primaryType = cq:Page

↓

jcr:content

jcr:primaryType = cq:PageContent
```

---

# Real Project Example 1

Home Page

```text
/content/mysite/en/home

↓

jcr:content

↓

root

↓

banner

↓

text

↓

image
```

Every component on the page is a JCR node.

---

# Real Project Example 2

Image Asset

```text
/content/dam/mysite/logo.png

↓

dam:Asset

↓

jcr:content

↓

metadata
```

Metadata like title, description, and tags are stored as properties.

---

# Real Project Example 3

Experience Fragment

```text
/content/experience-fragments

↓

mysite

↓

header

↓

master
```

Experience Fragments are also stored as JCR nodes.

---

# How Does AEM Read Data?

```text
Browser

↓

Servlet / Sling Model

↓

ResourceResolver

↓

JCR

↓

Node

↓

Properties

↓

Response
```

---

# Best Practices

### ✅ Store structured content as nodes

Example:

```text
Product

↓

Name

↓

Price

↓

Description
```

---

### ✅ Use meaningful node names

Good:

```text
home

about

contact
```

Bad:

```text
node1

test123

abc
```

---

### ✅ Never modify `/libs`

Always customize under:

```text
/apps
```

or use proxy components and overlays where appropriate.

---

# Common Mistakes

### ❌ Confusing Nodes and Properties

Wrong:

```text
Title is a Node
```

Correct:

```text
Title is a Property

Page is a Node
```

---

### ❌ Editing `/libs`

Adobe updates can overwrite changes.

Always place custom code under `/apps`.

---

### ❌ Using incorrect node types

Example:

```text
dam:Asset
```

for a page.

Instead:

```text
cq:Page
```

---

# Interview Questions

### 1. What is JCR?

A **Java Content Repository** used by AEM to store all content in a hierarchical structure of nodes and properties.

---

### 2. Which JCR implementation does AEM use?

**Apache Jackrabbit Oak**.

---

### 3. What are the basic building blocks of JCR?

* Nodes
* Properties

---

### 4. Where are website pages stored?

```text
/content
```

---

### 5. Where are assets stored?

```text
/content/dam
```

---

### 6. What is the difference between a Node and a Property?

| Node                                 | Property                 |
| ------------------------------------ | ------------------------ |
| Represents an item in the repository | Stores data about a node |
| Can have child nodes                 | Cannot have child nodes  |

Example:

```text
home (Node)

jcr:title = Home (Property)
```

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain JCR in AEM."**

A strong answer is:

> "JCR (Java Content Repository) is the hierarchical repository used by AEM to store all content. It is implemented using Apache Jackrabbit Oak. Everything in AEM—pages, assets, components, workflows, and configurations—is stored as nodes with properties. Backend code accesses JCR through APIs such as `ResourceResolver`, `Resource`, `Node`, and `Session`."

This answer demonstrates both conceptual understanding and practical knowledge.

---

# Chapter 15: Resource vs Node vs ResourceResolver ⭐⭐⭐⭐⭐

This is asked in almost every AEM Backend Developer interview because almost every AEM application uses these APIs. It is also covered in your uploaded AEM notes. 

---

# Before Learning

Many beginners get confused between these three.

Think of them like this:

```text
JCR Repository
        │
        ▼
ResourceResolver
        │
        ▼
Resource
        │
        ▼
Node
```

---

# What is ResourceResolver?

A **ResourceResolver** is the entry point to access the AEM repository.

Think of it as a **gateway** or **door**.

Without it, you cannot access repository resources.

Example:

```text
Browser

↓

Servlet

↓

ResourceResolver

↓

Repository
```

---

# Creating a ResourceResolver

Usually you get it from the request.

```java
ResourceResolver resolver =
request.getResourceResolver();
```

In Sling Models

```java
@SlingObject
private ResourceResolver resourceResolver;
```

In Workflow

```java
ResourceResolver resolver =
workflowSession.adaptTo(
ResourceResolver.class
);
```

---

# What Can ResourceResolver Do?

It can:

* Read resources
* Create resources
* Update resources
* Delete resources
* Commit changes
* Search resources

---

# Example

```java
Resource resource =
resourceResolver.getResource(
"/content/mysite/en/home"
);
```

Output

```text
Home Page Resource
```

---

# What is a Resource?

A **Resource** is Sling's representation of repository content.

Every page...

Every component...

Every asset...

is a Resource.

Example

```text
/content/mysite/en/home
```

is a Resource.

Another example

```text
/content/dam/logo.png
```

is also a Resource.

---

# Resource Example

```java
Resource resource =
resourceResolver.getResource(
"/content/mysite/en/home"
);
```

Now

```java
resource
```

represents

```text
/content/mysite/en/home
```

---

# What Can Resource Do?

A Resource can:

* Read properties
* Read child resources
* Adapt to Node
* Adapt to ValueMap
* Adapt to Page

---

# Reading Properties

```java
ValueMap map =
resource.getValueMap();

String title =
map.get(
"jcr:title",
String.class
);
```

Output

```text
Home Page
```

---

# Child Resources

Repository

```text
home

↓

jcr:content

↓

root

↓

text
```

Java

```java
Resource child =
resource.getChild(
"jcr:content"
);
```

---

# What is Node?

A **Node** is the actual JCR object.

Unlike Resource,

Node belongs to

```text
javax.jcr
```

or in newer repositories:

```text
jakarta.jcr
```

Node provides low-level JCR operations.

---

# Getting Node

```java
Node node =
resource.adaptTo(
Node.class
);
```

Now you have full JCR access.

---

# What Can Node Do?

Node can:

* Add nodes
* Remove nodes
* Read properties
* Set properties
* Move nodes
* Lock nodes
* Version nodes

---

# Reading Property

```java
String title =
node.getProperty(
"jcr:title"
).getString();
```

---

# Updating Property

```java
node.setProperty(
"approved",
true
);
```

---

# Saving Changes

Using Session

```java
Session session =
resourceResolver.adaptTo(
Session.class
);

session.save();
```

Or

```java
resourceResolver.commit();
```

---

# Relationship

```text
Repository

↓

ResourceResolver

↓

Resource

↓

Node
```

ResourceResolver finds Resources.

Resource represents content.

Node provides low-level JCR operations.

---

# Complete Example

```java
ResourceResolver resolver =
request.getResourceResolver();

Resource resource =
resolver.getResource(
"/content/mysite/en/home"
);

Node node =
resource.adaptTo(Node.class);

String title =
node.getProperty(
"jcr:title"
).getString();

System.out.println(title);
```

Output

```text
Home Page
```

---

# Reading Using Resource

```java
Resource resource =
resolver.getResource(
"/content/mysite/en/home"
);

ValueMap map =
resource.getValueMap();

String title =
map.get(
"jcr:title",
String.class
);
```

Much simpler.

---

# Resource vs Node

| Resource           | Node                                  |
| ------------------ | ------------------------------------- |
| Sling API          | JCR API                               |
| Easier to use      | Low-level API                         |
| Uses ValueMap      | Uses Property                         |
| Recommended in AEM | Use only when JCR features are needed |

---

# ResourceResolver vs Resource

| ResourceResolver    | Resource                       |
| ------------------- | ------------------------------ |
| Accesses repository | Represents one repository item |
| Finds resources     | Reads content                  |
| Creates resources   | Reads child resources          |

---

# Real Project Example 1

Read Page Title

```java
Resource page =
resolver.getResource(
"/content/mysite/en/home"
);

String title =
page.getValueMap().get(
"jcr:title",
String.class
);
```

---

# Real Project Example 2

Update Approval Status

```java
Node node =
resource.adaptTo(Node.class);

node.setProperty(
"approved",
true
);

resolver.commit();
```

---

# Real Project Example 3

Read Child Components

```java
for(Resource child :
resource.getChildren()){

System.out.println(
child.getName()
);

}
```

Output

```text
banner

text

image

carousel
```

---

# Which One Should You Use?

### Use Resource

For

* Reading content
* Sling Models
* Servlets
* Components

### Use Node

Only when you need

* JCR Versioning
* Locking
* Mixins
* Low-level JCR operations

Adobe recommends using the **Resource API whenever possible** because it aligns with Sling's abstraction.

---

# Best Practices

### ✅ Prefer Resource API

Good

```java
resource.getValueMap();
```

instead of

```java
node.getProperty();
```

when simple property access is sufficient.

---

### ✅ Close Service ResourceResolvers

If you obtain a `ResourceResolver` from a service (for example, via `ResourceResolverFactory`), close it after use:

```java
try (ResourceResolver resolver = serviceResolver) {
    // use resolver
}
```

This helps prevent resource leaks.

---

### ✅ Commit Only When Needed

```java
resolver.commit();
```

Only after making changes.

---

# Common Mistakes

### ❌ Using Node Everywhere

Prefer:

```java
Resource
```

for most AEM development.

---

### ❌ Forgetting to Commit

```java
node.setProperty(
"title",
"Home"
);
```

Without:

```java
resolver.commit();
```

the changes are not persisted when using the Resource API.

---

### ❌ Null Resource

Always check:

```java
Resource resource =
resolver.getResource(path);

if(resource != null){

}
```

---

# Interview Questions

### 1. What is a ResourceResolver?

A `ResourceResolver` is the main entry point for accessing and manipulating resources in the AEM repository.

---

### 2. What is a Resource?

A Sling object representing a node or item in the repository.

---

### 3. What is a Node?

A low-level JCR object that provides direct repository operations.

---

### 4. Which API should be preferred?

**Resource API**.

Use Node only when advanced JCR functionality is required.

---

### 5. How do you convert a Resource into a Node?

```java
Node node =
resource.adaptTo(Node.class);
```

---

### 6. How do you read a property using Resource?

```java
String title =
resource.getValueMap().get(
    "jcr:title",
    String.class
);
```

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"What is the difference between Resource and Node?"**

A strong answer is:

* **Resource** is part of the Sling API and provides a simple, AEM-friendly way to work with repository content. It is the preferred API for most development.
* **Node** is part of the JCR API and provides lower-level repository operations such as versioning, locking, and node manipulation.
* You can convert a `Resource` to a `Node` using:

```java
Node node = resource.adaptTo(Node.class);
```

This answer demonstrates both practical AEM knowledge and an understanding of the underlying JCR architecture.

---

# Chapter 16: ValueMap, ModifiableValueMap & JCR CRUD Operations ⭐⭐⭐⭐⭐

This topic is used **every day** by AEM backend developers because almost every project needs to **read, create, update, and delete content** from the JCR repository. It is also covered in your uploaded AEM notes. 

---

# What is ValueMap?

A **ValueMap** is a **read-only map** used to read properties from a Resource.

Think of it like a Java `Map<String, Object>`.

```text
JCR Node
    │
    ▼
Resource
    │
    ▼
ValueMap
    │
    ▼
Read Properties
```

---

# Repository Example

```text
/content/mysite/en/home

jcr:title = Home Page

description = Welcome to AEM

views = 100

published = true
```

---

# Reading Properties

```java
Resource resource = resolver.getResource(
        "/content/mysite/en/home");

ValueMap map = resource.getValueMap();

String title = map.get(
        "jcr:title",
        String.class);

System.out.println(title);
```

Output

```text
Home Page
```

---

# Reading Different Data Types

### String

```java
String title = map.get(
    "jcr:title",
    String.class);
```

---

### Integer

```java
Integer views = map.get(
    "views",
    Integer.class);
```

---

### Boolean

```java
Boolean published = map.get(
    "published",
    Boolean.class);
```

---

### String Array

```java
String[] tags = map.get(
    "cq:tags",
    String[].class);
```

---

# Default Values

Suppose:

```text
subtitle
```

does not exist.

Instead of getting `null`:

```java
String subtitle = map.get(
        "subtitle",
        "Default Subtitle");
```

Output

```text
Default Subtitle
```

---

# What is ModifiableValueMap?

`ModifiableValueMap` is used to **update JCR properties**.

Unlike `ValueMap`:

✅ Read

✅ Write

---

# Getting ModifiableValueMap

```java
ModifiableValueMap map =
resource.adaptTo(
ModifiableValueMap.class
);
```

---

# Updating Property

```java
map.put(
    "jcr:title",
    "Updated Home Page");
```

Nothing is saved yet.

---

# Save Changes

```java
resolver.commit();
```

Now the repository is updated.

---

# Complete Update Example

```java
Resource resource =
resolver.getResource(
"/content/mysite/en/home"
);

ModifiableValueMap map =
resource.adaptTo(
ModifiableValueMap.class
);

map.put(
"approved",
true
);

map.put(
"reviewer",
"admin"
);

resolver.commit();
```

Repository

```text
approved = true

reviewer = admin
```

---

# Creating a Resource

Use `ResourceResolver.create()`.

```java
Map<String,Object> props =
new HashMap<>();

props.put(
"jcr:primaryType",
"nt:unstructured"
);

props.put(
"title",
"Product 1"
);

Resource parent =
resolver.getResource(
"/content/products"
);

Resource newResource =
resolver.create(
parent,
"product1",
props
);

resolver.commit();
```

Repository

```text
/content/products

    product1

        title = Product 1
```

---

# Deleting a Resource

```java
Resource resource =
resolver.getResource(
"/content/products/product1"
);

resolver.delete(resource);

resolver.commit();
```

The node is removed.

---

# Complete CRUD Flow

```text
CREATE

resolver.create()

↓

READ

resource.getValueMap()

↓

UPDATE

modifiableValueMap.put()

↓

DELETE

resolver.delete()
```

---

# Real Project Example 1 – Update Page Title

```java
Resource page =
resolver.getResource(
"/content/mysite/en/home/jcr:content"
);

ModifiableValueMap map =
page.adaptTo(
ModifiableValueMap.class
);

map.put(
"jcr:title",
"Home Updated"
);

resolver.commit();
```

---

# Real Project Example 2 – Create Product

```java
props.put(
"name",
"Laptop"
);

props.put(
"price",
65000
);
```

Repository

```text
product1

name = Laptop

price = 65000
```

---

# Real Project Example 3 – Delete Old Asset

```java
Resource asset =
resolver.getResource(
"/content/dam/old/logo.png"
);

resolver.delete(asset);

resolver.commit();
```

---

# Complete Enterprise Flow

```text
Servlet

↓

ResourceResolver

↓

Resource

↓

ValueMap

↓

Business Logic

↓

ModifiableValueMap

↓

resolver.commit()

↓

JCR Updated
```

---

# ValueMap vs ModifiableValueMap

| ValueMap                 | ModifiableValueMap            |
| ------------------------ | ----------------------------- |
| Read Only                | Read + Write                  |
| Cannot update properties | Can update properties         |
| No commit needed         | Must call `resolver.commit()` |

---

# Best Practices

### ✅ Use ValueMap for reading

```java
resource.getValueMap();
```

---

### ✅ Use ModifiableValueMap for updates

```java
resource.adaptTo(
ModifiableValueMap.class
);
```

---

### ✅ Commit once

Good

```java
map.put("title","Home");

map.put("status","Approved");

resolver.commit();
```

Avoid calling `commit()` after every property update.

---

### ✅ Check for null

```java
Resource resource =
resolver.getResource(path);

if(resource != null){

// process

}
```

---

# Common Mistakes

### ❌ Trying to modify a ValueMap

Wrong

```java
ValueMap map =
resource.getValueMap();

map.put(
"title",
"Home"
);
```

`ValueMap` is read-only.

---

### ❌ Forgetting commit

Wrong

```java
map.put(
"title",
"Home"
);
```

Without

```java
resolver.commit();
```

changes are not saved.

---

### ❌ Modifying a null Resource

Always check:

```java
if(resource != null){

}
```

---

# Interview Questions

### 1. What is ValueMap?

A read-only map used to access properties of a Sling Resource.

---

### 2. What is ModifiableValueMap?

A writable map used to modify resource properties.

---

### 3. How do you save changes?

```java
resolver.commit();
```

---

### 4. How do you create a resource?

```java
resolver.create(
parent,
"name",
properties
);
```

---

### 5. How do you delete a resource?

```java
resolver.delete(resource);

resolver.commit();
```

---

### 6. What is the difference between ValueMap and ModifiableValueMap?

* **ValueMap** → Read-only.
* **ModifiableValueMap** → Read and update properties.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do you update a page property in AEM?"**

A strong answer is:

```java
Resource resource = resolver.getResource(
    "/content/mysite/en/home/jcr:content");

ModifiableValueMap properties =
    resource.adaptTo(ModifiableValueMap.class);

properties.put("jcr:title", "New Home Page");

resolver.commit();
```

Then explain:

1. Get the `Resource`.
2. Adapt it to `ModifiableValueMap`.
3. Update the property using `put()`.
4. Save the changes with `resolver.commit()`.

This is the standard approach used in enterprise AEM applications.

---

# JCR Topics Completed So Far

* ✅ JCR Overview
* ✅ Nodes
* ✅ Properties
* ✅ ResourceResolver
* ✅ Resource
* ✅ Node
* ✅ ValueMap
* ✅ ModifiableValueMap
* ✅ JCR CRUD Operations

---

# Chapter 17: QueryBuilder API & JCR-SQL2 ⭐⭐⭐⭐⭐

---

# What is QueryBuilder?

**QueryBuilder** is an AEM API used to search the JCR repository using a map of predicates instead of writing SQL-like queries.

Think of it like:

```text
JCR Repository
       │
       ▼
QueryBuilder
       │
       ▼
Search Results
```

Adobe recommends QueryBuilder for most AEM searches because it integrates well with Sling and JCR.

---

# Why do we use QueryBuilder?

Common use cases:

* Find pages
* Search assets
* Search by tags
* Search by title
* Full-text search
* Search by template
* Pagination
* Search components

---

# QueryBuilder Architecture

```text
Servlet

↓

OSGi Service

↓

QueryBuilder

↓

JCR Repository

↓

Search Results
```

---

# Step 1: Inject QueryBuilder

```java
@Reference
private QueryBuilder queryBuilder;
```

---

# Step 2: Get Session

```java
Session session =
resourceResolver.adaptTo(Session.class);
```

---

# Step 3: Create Predicate Map

Example: Search all pages.

```java
Map<String, String> map = new HashMap<>();

map.put("path", "/content/mysite");
map.put("type", "cq:Page");
```

Meaning:

* Search under `/content/mysite`
* Only return `cq:Page` nodes

---

# Step 4: Execute Query

```java
Query query = queryBuilder.createQuery(
        PredicateGroup.create(map),
        session);

SearchResult result = query.getResult();
```

---

# Step 5: Iterate Results

```java
for(Hit hit : result.getHits()){

    System.out.println(hit.getPath());

}
```

Output:

```text
/content/mysite/en/home

/content/mysite/en/about

/content/mysite/en/contact
```

---

# Complete Example

```java
@Reference
private QueryBuilder queryBuilder;

public void searchPages(ResourceResolver resolver)
        throws RepositoryException {

    Session session =
            resolver.adaptTo(Session.class);

    Map<String,String> map =
            new HashMap<>();

    map.put("path","/content/mysite");
    map.put("type","cq:Page");

    Query query =
            queryBuilder.createQuery(
                    PredicateGroup.create(map),
                    session);

    SearchResult result =
            query.getResult();

    for(Hit hit : result.getHits()){

        System.out.println(hit.getPath());

    }

}
```

---

# Common Predicates

## Path Predicate

```java
map.put("path",
"/content/mysite");
```

Search only inside:

```text
/content/mysite
```

---

## Type Predicate

```java
map.put(
"type",
"cq:Page"
);
```

Only pages.

Other examples:

```text
dam:Asset

nt:unstructured

cq:PageContent
```

---

## Property Predicate

Find pages where:

```text
jcr:title = Home
```

```java
map.put(
"property",
"jcr:content/jcr:title"
);

map.put(
"property.value",
"Home"
);
```

---

## Full-text Search

Search word:

```text
Laptop
```

```java
map.put(
"fulltext",
"Laptop"
);
```

This searches page content, titles, and indexed text.

---

## Limit Results

```java
map.put(
"p.limit",
"10"
);
```

Only return:

```text
10 Results
```

---

## Pagination

```java
map.put(
"p.offset",
"20"
);

map.put(
"p.limit",
"10"
);
```

Meaning:

Skip first 20 results and return the next 10.

---

# Real Project Example 1 - Search Pages

```java
map.put(
"path",
"/content/mysite"
);

map.put(
"type",
"cq:Page"
);
```

Result

```text
Home

About

Products

Contact
```

---

# Real Project Example 2 - Search Assets

```java
map.put(
"path",
"/content/dam"
);

map.put(
"type",
"dam:Asset"
);
```

Output

```text
logo.png

banner.jpg

video.mp4
```

---

# Real Project Example 3 - Search by Tag

```java
map.put(
"property",
"jcr:content/cq:tags"
);

map.put(
"property.value",
"mysite:news"
);
```

Output

```text
Latest News

Press Release
```

---

# What is JCR-SQL2?

JCR-SQL2 is the **SQL-like query language** defined by the JCR specification.

Example:

```sql
SELECT *
FROM [cq:Page]
WHERE ISDESCENDANTNODE('/content/mysite')
```

It returns all pages under:

```text
/content/mysite
```

---

# Executing JCR-SQL2

```java
Session session =
resolver.adaptTo(Session.class);

QueryManager qm =
session.getWorkspace()
.getQueryManager();

Query query =
qm.createQuery(

"SELECT * FROM [cq:Page]",

Query.JCR_SQL2

);

QueryResult result =
query.execute();
```

---

# QueryBuilder vs JCR-SQL2

| QueryBuilder                       | JCR-SQL2                             |
| ---------------------------------- | ------------------------------------ |
| AEM-specific API                   | Standard JCR query language          |
| Predicate-based                    | SQL-like syntax                      |
| Easier for common searches         | More flexible for complex queries    |
| Preferred for most AEM development | Used when SQL2 features are required |

---

# Performance Best Practices

## ✅ Always Search Under a Path

Good

```java
map.put(
"path",
"/content/mysite"
);
```

Avoid searching the entire repository.

---

## ✅ Limit Results

```java
map.put(
"p.limit",
"20"
);
```

Never return thousands of results unnecessarily.

---

## ✅ Use Indexed Properties

Search on indexed properties whenever possible for better performance.

---

## ✅ Use Pagination

Large result sets should always use pagination.

---

# Common Mistakes

### ❌ No Path Predicate

Wrong

```java
map.put(
"type",
"cq:Page"
);
```

This searches across the entire repository.

---

### ❌ Unlimited Results

Wrong

```java
No p.limit
```

This can be expensive on large repositories.

---

### ❌ Full-text Everywhere

Use full-text search only when necessary. Exact property searches are often more efficient.

---

# Interview Questions

### 1. What is QueryBuilder?

An AEM API used to search the JCR repository using predicates.

---

### 2. How do you inject QueryBuilder?

```java
@Reference
private QueryBuilder queryBuilder;
```

---

### 3. Which object executes the query?

```java
Query
```

created by `QueryBuilder`.

---

### 4. How do you limit results?

```java
map.put(
"p.limit",
"10"
);
```

---

### 5. What is JCR-SQL2?

The standard SQL-like query language for JCR repositories.

---

### 6. Which is generally preferred in AEM?

**QueryBuilder** for most application development because it is simpler and integrates well with AEM.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"How do you search pages in AEM?"**

A strong answer is:

1. Inject `QueryBuilder`.
2. Get the `Session` from the `ResourceResolver`.
3. Create a predicate map (`path`, `type`, etc.).
4. Execute the query using `queryBuilder.createQuery(...)`.
5. Iterate through the `SearchResult` and process each `Hit`.

Also mention that you always:

* Restrict searches with a **path**.
* Use **`p.limit`** for pagination.
* Prefer indexed property searches for better performance.

This demonstrates both correctness and performance awareness, which interviewers value.

---

# JCR Topics Completed

* ✅ JCR Overview
* ✅ ResourceResolver
* ✅ Resource
* ✅ Node
* ✅ ValueMap
* ✅ ModifiableValueMap
* ✅ CRUD Operations
* ✅ QueryBuilder API
* ✅ JCR-SQL2

---



# Chapter 18 - AEM Event Handling ⭐⭐⭐⭐⭐

---

# What is Event Handling?

Event Handling is a mechanism where one component **publishes an event**, and another component **listens to that event** and performs an action.

Think of it like WhatsApp notifications.

```text
Person Sends Message
        │
        ▼
WhatsApp Server
        │
        ▼
Notification Sent
        │
        ▼
Mobile Receives Notification
```

Similarly in AEM:

```text
Page Published
      │
      ▼
Event Generated
      │
      ▼
Event Handler
      │
      ▼
Send Email
```

---

# Why Do We Use Events?

Events help us:

* Decouple components
* Execute background tasks
* Improve scalability
* Notify multiple services
* Trigger asynchronous processing

---

# Real Project Example

```text
Author Publishes Page

↓

AEM Event

↓

Search Index Update

↓

Cache Clear

↓

Email Notification

↓

Analytics Update
```

One action triggers multiple independent processes.

---

# Event Architecture

```text
Publisher

↓

EventAdmin

↓

OSGi Event

↓

EventHandler

↓

Business Logic
```

---

# Main Components

| Component    | Purpose                        |
| ------------ | ------------------------------ |
| EventAdmin   | Publishes events               |
| Event        | Contains event data            |
| EventHandler | Receives events                |
| Sling Jobs   | Reliable background processing |

---

# What is EventAdmin?

`EventAdmin` is an OSGi service used to publish events.

Inject it:

```java
@Reference
private EventAdmin eventAdmin;
```

---

# Publishing an Event

```java
Dictionary<String, Object> properties = new Hashtable<>();

properties.put("pagePath", "/content/mysite/en/home");

Event event = new Event(
    "mysite/page/published",
    properties
);

eventAdmin.postEvent(event);
```

### Explanation

* Topic: `"mysite/page/published"`
* Data: `pagePath`
* Method: `postEvent()` (asynchronous)

---

# postEvent() vs sendEvent()

### postEvent()

```java
eventAdmin.postEvent(event);
```

* Asynchronous
* Returns immediately
* Recommended for most use cases

---

### sendEvent()

```java
eventAdmin.sendEvent(event);
```

* Synchronous
* Waits until all handlers complete
* Used only when immediate processing is required

---

# Creating an EventHandler

```java
@Component(
service = EventHandler.class,
property = {
EventConstants.EVENT_TOPIC + "=mysite/page/published"
}
)

public class PagePublishHandler
implements EventHandler {

@Override

public void handleEvent(Event event){

}

}
```

---

# Reading Event Data

```java
@Override
public void handleEvent(Event event){

String path =
(String)event.getProperty("pagePath");

System.out.println(path);

}
```

Output

```text
/content/mysite/en/home
```

---

# Complete Example

Publisher

```java
Dictionary<String,Object> props =
new Hashtable<>();

props.put(
"title",
"Home Page"
);

Event event =
new Event(
"mysite/page/create",
props
);

eventAdmin.postEvent(event);
```

Handler

```java
@Component(

service=EventHandler.class,

property={

EventConstants.EVENT_TOPIC
+"=mysite/page/create"

}

)

public class CreateHandler
implements EventHandler {

@Override

public void handleEvent(Event event){

String title=
(String)event.getProperty(
"title"
);

System.out.println(title);

}

}
```

Output

```text
Home Page
```

---

# Real Project Example 1

## Email Notification

```text
Workflow Completed

↓

Event Published

↓

Email Handler

↓

SMTP

↓

Mail Sent
```

---

# Real Project Example 2

## Search Index

```text
Page Published

↓

Event

↓

Search Service

↓

Update Solr Index
```

---

# Real Project Example 3

## Analytics

```text
Page Viewed

↓

Event

↓

Analytics Service

↓

Adobe Analytics
```

---

# What are Sling Jobs?

Sometimes events are **too lightweight**.

If processing is:

* Long-running
* Resource intensive
* Must survive server restarts

Use **Sling Jobs**.

---

# Sling Job Architecture

```text
Servlet

↓

Create Job

↓

Job Queue

↓

JobConsumer

↓

Business Logic
```

Jobs are queued and retried if necessary.

---

# Creating a Job

```java
@Reference
private JobManager jobManager;

Map<String,Object> props =
new HashMap<>();

props.put(
"id",
100
);

jobManager.addJob(

"mysite/product/import",

props

);
```

---

# JobConsumer

```java
@Component(

service=JobConsumer.class,

property={

JobConsumer.PROPERTY_TOPICS
+"=mysite/product/import"

}

)

public class ProductImportJob
implements JobConsumer {

@Override

public JobResult process(
Job job){

return JobResult.OK;

}

}
```

---

# Reading Job Properties

```java
Integer id =
(Integer)job.getProperty(
"id"
);
```

---

# Complete Flow

```text
Servlet

↓

JobManager

↓

Queue

↓

JobConsumer

↓

ProductService

↓

Repository
```

---

# Event vs Sling Job

| Event                    | Sling Job               |
| ------------------------ | ----------------------- |
| Lightweight notification | Background task         |
| No retry guarantee       | Retry support           |
| Fire-and-forget          | Reliable queue          |
| Fast execution           | Long-running processing |

---

# Best Practices

### ✅ Use Events

For:

* Notifications
* Cache clearing
* Logging
* UI updates

---

### ✅ Use Sling Jobs

For:

* Import thousands of products
* Generate reports
* Video processing
* Image processing
* External API synchronization

---

### ✅ Keep EventHandlers lightweight

```text
Event

↓

OSGi Service

↓

Repository
```

Avoid heavy business logic inside `handleEvent()`.

---

### ✅ Use meaningful event topics

Good

```text
mysite/page/published
```

Avoid

```text
test/event
```

---

# Common Mistakes

### ❌ Heavy processing in EventHandler

Move long-running work to a Sling Job.

---

### ❌ Using sendEvent() unnecessarily

Prefer:

```java
eventAdmin.postEvent(event);
```

for most scenarios.

---

### ❌ Putting all logic inside process()

Keep `JobConsumer` focused and delegate business logic to services.

---

# Interview Questions

### 1. What is EventAdmin?

An OSGi service used to publish events.

---

### 2. Difference between postEvent() and sendEvent()?

* `postEvent()` → Asynchronous
* `sendEvent()` → Synchronous

---

### 3. Which interface receives events?

```java
EventHandler
```

---

### 4. When should you use Sling Jobs?

When tasks are:

* Long-running
* Resource intensive
* Need retries
* Must survive failures

---

### 5. Which interface processes Sling Jobs?

```java
JobConsumer
```

---

### 6. Can an EventHandler create a Sling Job?

**Yes.** This is a common enterprise pattern:

```text
Event

↓

EventHandler

↓

JobManager

↓

JobConsumer

↓

Business Logic
```

This keeps event handling responsive while moving expensive work into a reliable background queue.

---

# Enterprise Architecture

```text
Servlet

↓

OSGi Service

↓

EventAdmin

↓

EventHandler

↓

JobManager

↓

JobConsumer

↓

Repository / REST API

↓

Complete
```

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"When would you use an Event instead of a Sling Job?"**

A strong answer is:

* I use **OSGi Events** for lightweight notifications and decoupled communication between components, such as clearing caches or notifying services.
* I use **Sling Jobs** for long-running or critical background tasks, such as importing data, processing assets, or synchronizing with external systems, because Sling Jobs provide queuing and retry capabilities.

---

# Topics Completed

You have now covered:

* ✅ Sling Models
* ✅ OSGi Services
* ✅ Servlets
* ✅ Filters
* ✅ Scheduler
* ✅ Workflow
* ✅ JCR
* ✅ QueryBuilder
* ✅ Event Handling
* ✅ Sling Jobs


# Chapter 19: AEM Dispatcher ⭐⭐⭐⭐⭐

---

# What is Dispatcher?

**Dispatcher** is Adobe's **caching and load-balancing tool** that sits between the client (browser) and AEM Publish instances.

It performs three major functions:

* Caching
* Load Balancing
* Security Filtering

---

# Why is Dispatcher Needed?

Imagine 10,000 users opening your homepage.

Without Dispatcher:

```text
10000 Users
      │
      ▼
AEM Publish
```

Every request goes to AEM.

Problems:

* Slow performance
* High CPU usage
* High memory usage
* Server overload

---

With Dispatcher:

```text
10000 Users
      │
      ▼
Dispatcher
      │
 ┌────┴────┐
 │         │
Cache?     No Cache
 │           │
 ▼           ▼
Return      AEM Publish
Cached      │
Page        ▼
        Generate Page
             │
             ▼
      Save to Cache
```

Most requests are served directly from the cache, making the site much faster.

---

# AEM Architecture

```text
Internet Users
       │
       ▼
Apache / IIS Web Server
       │
       ▼
Dispatcher Module
       │
 ┌─────┴─────┐
 │           │
Publish 1   Publish 2
       │
       ▼
Author
```

> The **Author** instance is **not** accessed directly by end users.

---

# Dispatcher Responsibilities

## 1. Caching ⭐⭐⭐⭐⭐

Stores rendered HTML, JSON, CSS, JavaScript, and images on disk.

Example:

First request:

```text
User

↓

Dispatcher

↓

Publish

↓

HTML Generated

↓

Stored in Cache
```

Second request:

```text
User

↓

Dispatcher

↓

Cache

↓

HTML Returned
```

Publish is not contacted.

---

## 2. Load Balancing

Suppose you have:

```text
Publish 1

Publish 2

Publish 3
```

Dispatcher distributes requests across all Publish instances.

```text
User 1 → Publish 1

User 2 → Publish 2

User 3 → Publish 3
```

This improves scalability and availability.

---

## 3. Security

Dispatcher blocks unauthorized requests.

Example:

Allowed:

```text
/content/mysite/en/home.html
```

Blocked:

```text
/system/console

/crx/de

/bin/querybuilder.json
```

These endpoints should not be publicly accessible.

---

# Dispatcher Cache

Example cache directory:

```text
/opt/dispatcher/cache

/content

    mysite

        en

            home.html
```

If a user requests:

```text
/content/mysite/en/home.html
```

Dispatcher first checks:

```text
Cache Exists?

YES

↓

Return Cached File
```

---

# Cache Miss

If the page is not cached:

```text
Browser

↓

Dispatcher

↓

Publish

↓

Render Page

↓

Save Cache

↓

Return Response
```

---

# Cache Hit

```text
Browser

↓

Dispatcher

↓

Cache

↓

Return File
```

Publish is skipped.

---

# Dispatcher Configuration

Main configuration file:

```text
dispatcher.any
```

It contains rules for:

* Farms
* Filters
* Cache
* Renderers
* Statistics
* Virtual Hosts

---

# Farms

A farm groups related Publish instances.

Example:

```text
Farm

↓

Publish 1

Publish 2
```

---

Example:

```text
/farms {

    /publish {

    }

}
```

---

# Render Section

Defines Publish instances.

Example:

```text
/renders {

    /publish1 {

        /hostname "localhost"

        /port "4503"

    }

}
```

---

# Cache Section

```text
/cache {

    /docroot "/opt/cache"

}
```

Dispatcher stores cached pages here.

---

# Filter Rules

Filters control which URLs are allowed.

Example:

```text
/filter {

    /0001 {

        /type "allow"

        /url "/content/*"

    }

}
```

Allow:

```text
/content/*
```

---

Block:

```text
/filter {

    /0002 {

        /type "deny"

        /url "/system/*"

    }

}
```

Requests to `/system/*` are denied.

---

# Cache Invalidation (Flush)

Suppose a page is updated.

Current flow:

```text
Old Cache

↓

User Still Gets Old Page
```

To avoid this:

```text
Author

↓

Replication

↓

Dispatcher Flush

↓

Delete Cached File

↓

Next Request

↓

Fresh Page
```

This process is called **Cache Invalidation** or **Dispatcher Flush**.

---

# Dispatcher Flush Flow

```text
Author

↓

Publish

↓

Dispatcher Flush Agent

↓

Delete Cache

↓

User Gets Latest Content
```

---

# Real Project Example

A user requests:

```text
/content/mysite/en/products.html
```

Flow:

```text
Browser

↓

Dispatcher

↓

Cache Exists?

↓

Yes

↓

Return Cached Page
```

If not:

```text
Dispatcher

↓

Publish

↓

HTML

↓

Cache

↓

Browser
```

---

# Best Practices

### ✅ Cache public pages

Examples:

```text
Home

Products

About

Contact
```

---

### ✅ Don't cache personalized pages

Examples:

```text
/profile

/cart

/checkout
```

These contain user-specific information.

---

### ✅ Block administrative URLs

Always deny:

```text
/system/*

/crx/*

/libs/*
```

from public access.

---

### ✅ Use Dispatcher Flush

Always invalidate the cache when content changes.

---

# Common Mistakes

### ❌ No cache invalidation

Users continue to see stale content.

---

### ❌ Caching personalized pages

Different users may receive another user's data.

---

### ❌ Allowing `/system/console`

This creates a major security risk.

---

### ❌ Sending all traffic directly to Publish

This defeats the purpose of Dispatcher and reduces scalability.

---

# Interview Questions

### 1. What is Dispatcher?

Dispatcher is Adobe's caching, load-balancing, and security layer that sits in front of AEM Publish instances.

---

### 2. Why do we use Dispatcher?

* Improve performance
* Reduce Publish server load
* Load balancing
* Security filtering

---

### 3. What is a Cache Hit?

The requested content is already cached, so Dispatcher serves it without contacting Publish.

---

### 4. What is a Cache Miss?

The content is not cached. Dispatcher requests it from Publish, caches it, and returns it to the user.

---

### 5. What is Dispatcher Flush?

The process of invalidating cached content after changes are published, ensuring users receive updated content.

---

### 6. Which file configures Dispatcher?

```text
dispatcher.any
```

---

### 7. Should `/system/console` be publicly accessible?

**No.** It should be blocked by Dispatcher filters.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain the request flow in AEM with Dispatcher."**

A strong answer is:

```text
Browser
    │
    ▼
Web Server (Apache/IIS)
    │
    ▼
Dispatcher
    │
    ├── Cache Hit
    │      ▼
    │   Cached Response
    │
    └── Cache Miss
           ▼
      AEM Publish
           ▼
     Render Response
           ▼
     Store in Cache
           ▼
        Browser
```

Then add:

* Dispatcher improves performance by caching responses.
* It distributes traffic across Publish instances.
* It protects Publish by filtering requests.
* Cache is invalidated using Dispatcher Flush when content changes.

This is the level of explanation expected in enterprise AEM interviews.

---

# Topics Completed So Far

You have now covered:

* ✅ Sling Models
* ✅ OSGi
* ✅ Servlets
* ✅ Filters
* ✅ Scheduler
* ✅ Workflow
* ✅ JCR
* ✅ QueryBuilder
* ✅ Event Handling
* ✅ Sling Jobs
* ✅ Dispatcher

---

# Chapter 20: AEM MSM (Multi Site Manager) ⭐⭐⭐⭐⭐

---

# What is MSM?

**MSM (Multi Site Manager)** is an AEM feature that allows you to **manage multiple websites using a single master website (Blueprint)**.

Instead of creating the same content multiple times, you create it once and synchronize it across different sites.

---

# Example Without MSM

Suppose your company has websites for:

* USA
* UK
* India
* Australia

Without MSM:

```text
USA Website

Home
About
Products

UK Website

Home
About
Products

India Website

Home
About
Products
```

If you update the Home page, you must update it in every website manually.

---

# Example With MSM

```text
               Blueprint
          /content/global

                 │
        ┌────────┼────────┐
        │        │        │
        ▼        ▼        ▼

      USA       UK      India

   Live Copy  Live Copy Live Copy
```

Update the Blueprint once, then roll out the changes to all Live Copies.

---

# Why Do We Use MSM?

Enterprise companies use MSM for:

* Global websites
* Multi-country websites
* Multi-language websites
* Brand consistency
* Faster content updates
* Reduced maintenance

---

# MSM Architecture

```text
Blueprint

↓

Live Copy

↓

Rollout

↓

Country Sites
```

---

# Important MSM Terms

## 1. Blueprint ⭐⭐⭐⭐⭐

A **Blueprint** is the master website.

Example:

```text
/content/global
```

Contains:

```text
Home

About

Products

Contact
```

---

## 2. Live Copy ⭐⭐⭐⭐⭐

A **Live Copy** is a copy of the Blueprint.

Example:

```text
/content/us

/content/uk

/content/in
```

Each Live Copy inherits content from the Blueprint.

---

# Example

Blueprint

```text
/content/global

Home

About

Products
```

Live Copy

```text
/content/us

Home

About

Products
```

Initially, both are synchronized.

---

## 3. Rollout ⭐⭐⭐⭐⭐

A **Rollout** synchronizes changes from the Blueprint to the Live Copies.

Example:

```text
Blueprint

Home Updated

↓

Rollout

↓

USA Updated

↓

UK Updated

↓

India Updated
```

---

## 4. Rollout Configuration

Defines **when and how** content is synchronized.

Examples:

* On Activation
* On Modification
* Manual Rollout
* Scheduled Rollout

---

# MSM Flow

```text
Author

↓

Blueprint

↓

Rollout

↓

Live Copies

↓

Publish
```

---

# Real Project Example 1

Company:

Nike

Websites:

```text
nike.com

nike.co.uk

nike.in

nike.au
```

Blueprint

```text
/content/nike/global
```

Live Copies

```text
/content/nike/us

/content/nike/uk

/content/nike/in

/content/nike/au
```

Update:

```text
New Product Banner
```

Rollout

↓

All country sites updated.

---

# Real Project Example 2

Company:

Bank

Blueprint

```text
/content/bank/global
```

Countries

```text
USA

Canada

UK
```

Privacy Policy updated once.

Rollout updates all country websites.

---

# Real Project Example 3

Company:

Car Manufacturer

Blueprint

```text
Cars

SUV

Electric Cars
```

Live Copies

```text
Japan

Germany

India

Australia
```

Global content is shared, while local teams can customize market-specific content.

---

# Live Relationship

```text
Blueprint

↓

Live Relationship

↓

Live Copy
```

This relationship allows AEM to know where content originated.

---

# Breaking Inheritance

Sometimes a country wants different content.

Example:

Blueprint

```text
Title

Welcome
```

India wants:

```text
Welcome to India
```

Break inheritance.

Now:

```text
India

↓

Independent Content
```

Future rollouts won't overwrite that customized field unless inheritance is re-enabled.

---

# Language Copies

MSM is often combined with **Language Copies**.

Example

```text
Global

↓

English

↓

French

↓

German

↓

Spanish
```

Each language can be a Live Copy with translated content.

---

# MSM Structure

```text
/content

    global

    us

    uk

    india

    germany

    france
```

---

# Rollout Process

```text
Blueprint Updated

↓

Rollout Triggered

↓

Live Relationship Checked

↓

Live Copies Updated

↓

Replication

↓

Publish
```

---

# Advantages

✅ Single source of truth

✅ Easy maintenance

✅ Global consistency

✅ Faster updates

✅ Supports localization

---

# Best Practices

### ✅ Keep Blueprint Generic

Avoid country-specific content in the Blueprint.

---

### ✅ Customize Only When Needed

Break inheritance only for content that truly differs by region.

---

### ✅ Use Rollout Configurations

Choose the appropriate rollout strategy (manual, on activation, etc.) based on business requirements.

---

### ✅ Test Rollouts

Always verify changes in a lower environment before rolling out to production.

---

# Common Mistakes

### ❌ Editing Every Live Copy

Update the Blueprint instead whenever possible.

---

### ❌ Breaking Inheritance Everywhere

Too many inheritance breaks make synchronization difficult.

---

### ❌ No Rollout Strategy

Without a rollout plan, Live Copies become inconsistent.

---

# Interview Questions

### 1. What is MSM?

MSM (Multi Site Manager) is an AEM feature for managing multiple websites from a single Blueprint.

---

### 2. What is a Blueprint?

The master website from which Live Copies are created.

---

### 3. What is a Live Copy?

A site that inherits content from a Blueprint.

---

### 4. What is Rollout?

The process of synchronizing changes from the Blueprint to Live Copies.

---

### 5. Why would you break inheritance?

To allow a Live Copy to have customized content that should not be overwritten by future rollouts.

---

### 6. Can MSM be used with multilingual sites?

**Yes.** MSM is commonly used together with Language Copies to manage multilingual websites efficiently.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain MSM with a real example."**

A strong answer is:

> "Suppose a company has websites for the US, UK, India, and Germany. I create a Blueprint under `/content/global` and generate Live Copies for each country. When global content such as the homepage banner or privacy policy changes, I update the Blueprint and perform a Rollout. All Live Copies receive the updates automatically. If a country requires local customization, I can break inheritance for that specific content."

This demonstrates practical enterprise knowledge rather than just definitions.

---

# Topics Completed

You have now learned:

* ✅ Sling Models
* ✅ OSGi Services
* ✅ Servlets
* ✅ Filters
* ✅ Scheduler
* ✅ Workflow
* ✅ JCR
* ✅ QueryBuilder
* ✅ Event Handling
* ✅ Sling Jobs
* ✅ Dispatcher
* ✅ MSM (Multi Site Manager)

---

# Chapter 21: Content Fragments (CF) & Experience Fragments (XF) ⭐⭐⭐⭐⭐

This topic is **very important for AEM 6.5 and AEM as a Cloud Service**, especially in **Headless CMS**, **GraphQL**, and **SPA (React/Angular)** projects. It is also covered in your uploaded AEM notes. 

---

# Before Learning

Most beginners confuse **Content Fragments** and **Experience Fragments**.

Remember this simple rule:

> **Content Fragment = Content only**
>
> **Experience Fragment = Content + Layout + Components**

---

# What is a Content Fragment (CF)?

A **Content Fragment** is a **structured content object** that contains only **content**, not presentation (layout).

Think of it as content that can be reused everywhere.

Example:

```text
Title:
AEM Tutorial

Description:
AEM is a CMS developed by Adobe.

Author:
Vijay
```

There is **no HTML**, **no layout**, **no component design**.

---

# Content Fragment Architecture

```text
Author

↓

Content Fragment

↓

GraphQL / REST API

↓

React App

↓

Mobile App

↓

Website
```

The same content can be used by many applications.

---

# Where are Content Fragments Stored?

```text
/content/dam
```

Example:

```text
/content/dam/mysite/content-fragments/articles/aem-guide
```

---

# What is a Content Fragment Model?

A **Content Fragment Model (CFM)** defines the structure of the content.

Think of it like a Java class.

Example:

```
Article Model

↓

Title

↓

Description

↓

Author

↓

Publish Date
```

Every Article Content Fragment follows this structure.

---

# Creating a Content Fragment Model

Go to:

```text
Tools

↓

Assets

↓

Content Fragment Models
```

Create:

```
Article
```

Fields:

| Field        | Type             |
| ------------ | ---------------- |
| Title        | Single Line Text |
| Description  | Multi Line Text  |
| Author       | Single Line Text |
| Publish Date | Date             |
| Tags         | Tags             |

---

# Creating a Content Fragment

Go to:

```text
Assets

↓

Files

↓

Create

↓

Content Fragment
```

Choose:

```
Article Model
```

Fill:

```
Title:
Introduction to AEM

Description:
AEM is Adobe Experience Manager...

Author:
Vijay
```

Save.

---

# Real Project Example 1

News Website

Content Fragment

```
Title:
Adobe Summit 2026

Description:
Adobe introduced new AI features.

Author:
John
```

The same content appears on:

* Website
* Mobile App
* Smart TV
* REST API

---

# What is Headless CMS?

Traditional CMS

```text
Content

+

HTML

↓

Browser
```

Headless CMS

```text
Content

↓

API

↓

React

↓

Angular

↓

Flutter

↓

iOS

↓

Android
```

Content Fragments are the foundation of AEM Headless.

---

# GraphQL

GraphQL retrieves Content Fragments.

Example Query

```graphql
{
articleList{

items{

title

author

description

}

}

}
```

Response

```json
{
  "data": {
    "articleList": {
      "items": [
        {
          "title": "Introduction to AEM",
          "author": "Vijay",
          "description": "AEM is Adobe Experience Manager..."
        }
      ]
    }
  }
}
```

---

# Java API for Content Fragment

```java
Resource resource = resolver.getResource(
"/content/dam/mysite/content-fragments/articles/aem-guide"
);

ContentFragment fragment =
resource.adaptTo(ContentFragment.class);
```

Read Title

```java
String title =
fragment.getTitle();
```

Read Element

```java
ContentElement element =
fragment.getElement("description");

String value =
element.getContent();
```

---

# What is an Experience Fragment (XF)?

An **Experience Fragment** is a **reusable page section** containing:

* Components
* Layout
* Images
* Text
* Buttons
* Styling

Unlike Content Fragments, it contains presentation.

---

# Experience Fragment Example

Homepage Banner

```text
----------------------------------

Big Banner Image

Welcome to Adobe

[Learn More]

----------------------------------
```

Everything is stored together.

---

# XF Architecture

```text
Author

↓

Experience Fragment

↓

Website

↓

Adobe Target

↓

Adobe Campaign
```

---

# Where are Experience Fragments Stored?

```text
/content/experience-fragments
```

Example

```text
/content/experience-fragments/mysite/header/master
```

---

# Creating Experience Fragment

Go to:

```text
Experience Fragments

↓

Create

↓

Template

↓

Save
```

Add:

* Image
* Text
* Button
* Carousel

---

# Variations

Experience Fragment

↓

Master

↓

Mobile

↓

Tablet

↓

Christmas Campaign

↓

Summer Campaign

---

# Real Project Example 2

Company

Nike

Header XF

```
Logo

Menu

Search

Cart
```

Reuse on:

* Home
* Products
* Checkout
* Blog

Change once.

Entire website updates.

---

# Real Project Example 3

Marketing Campaign

Experience Fragment

↓

Adobe Target

↓

Personalization

↓

Different banners for different users.

---

# Content Fragment vs Experience Fragment

| Content Fragment            | Experience Fragment                       |
| --------------------------- | ----------------------------------------- |
| Content only                | Content + Layout                          |
| Stored in `/content/dam`    | Stored in `/content/experience-fragments` |
| Headless CMS                | Website reusable sections                 |
| Uses Content Fragment Model | Uses XF Template                          |
| Accessed via GraphQL        | Embedded into pages                       |

---

# Complete Flow

```text
Author

↓

Content Fragment

↓

GraphQL

↓

React

↓

Browser
```

Experience Fragment

```text
Author

↓

Experience Fragment

↓

Page

↓

Browser
```

---

# Best Practices

### ✅ Use Content Fragments

For:

* Headless CMS
* Mobile Apps
* GraphQL
* APIs
* Structured content

---

### ✅ Use Experience Fragments

For:

* Header
* Footer
* Banner
* Promotions
* Reusable page sections

---

### ✅ Keep Content Separate from Presentation

Content → Content Fragment

Layout → Experience Fragment

---

### ✅ Reuse Fragments

Avoid duplicating content across pages.

---

# Common Mistakes

### ❌ Using Experience Fragment for APIs

Use **Content Fragments** instead.

---

### ❌ Putting Layout into Content Fragment

Content Fragments should contain **content only**.

---

### ❌ Duplicating Headers

Create one **Experience Fragment** and reuse it.

---

# Interview Questions

### 1. What is a Content Fragment?

A structured content object without presentation, used for headless delivery through APIs like GraphQL.

---

### 2. What is an Experience Fragment?

A reusable combination of content and layout that can be embedded into multiple pages.

---

### 3. Where are Content Fragments stored?

```text
/content/dam
```

---

### 4. Where are Experience Fragments stored?

```text
/content/experience-fragments
```

---

### 5. Which feature is used with GraphQL?

**Content Fragments**.

---

### 6. Which feature is used for reusable website banners?

**Experience Fragments**.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"What is the difference between Content Fragment and Experience Fragment?"**

A strong answer is:

* **Content Fragment** contains only structured content and is primarily used for **headless CMS**, GraphQL, REST APIs, and multi-channel content delivery.
* **Experience Fragment** contains **content, layout, and AEM components** and is used to build reusable page sections such as headers, footers, banners, and marketing experiences.

A simple way to remember it is:

> **Content Fragment = Data**
>
> **Experience Fragment = Data + Presentation**

This concise explanation is exactly what interviewers often look for before diving into implementation details.

---

# What You've Completed So Far

You have now covered almost all major AEM backend topics:

* ✅ Sling Models
* ✅ OSGi Services
* ✅ Servlets
* ✅ Filters
* ✅ Scheduler
* ✅ Workflow
* ✅ JCR
* ✅ QueryBuilder
* ✅ Event Handling
* ✅ Sling Jobs
* ✅ Dispatcher
* ✅ MSM
* ✅ Content Fragments
* ✅ Experience Fragments




---

# Chapter 22: AEM GraphQL ⭐⭐⭐⭐⭐

---

# What is GraphQL?

**GraphQL** is a query language for APIs that allows the client to request **exactly the data it needs**.

Unlike REST APIs, GraphQL doesn't return unnecessary data.

---

# REST vs GraphQL

## REST

```text
Browser

↓

GET /api/article/1

↓

{
  "id":1,
  "title":"AEM",
  "author":"John",
  "description":"...",
  "createdDate":"...",
  "tags":["aem","cms"],
  "comments":[...]
}
```

Even if you only need the title, the entire object is returned.

---

## GraphQL

Request

```graphql
{
  articleByPath(
    _path:"/content/dam/mysite/articles/aem-guide"
  ){
    item{
      title
    }
  }
}
```

Response

```json
{
  "data":{
    "articleByPath":{
      "item":{
        "title":"AEM Guide"
      }
    }
  }
}
```

Only the requested field is returned.

---

# Why Use GraphQL?

Advantages:

* Fetch only required fields
* Better performance
* Smaller payload
* Single request for nested data
* Perfect for mobile apps
* Ideal for SPAs (React, Angular, Vue)

---

# GraphQL Architecture

```text
Content Fragment

↓

GraphQL Endpoint

↓

GraphQL Query

↓

JSON

↓

React / Angular / Mobile App
```

---

# Prerequisite

GraphQL works with **Content Fragments**.

Example:

Content Fragment Model

```text
Article

↓

Title

Description

Author

Publish Date
```

Content Fragment

```text
Title:
Learning AEM

Author:
Vijay

Description:
Complete AEM Guide
```

---

# GraphQL Endpoint

In AEM:

```text
Tools

↓

General

↓

GraphQL
```

Create an endpoint.

Example:

```text
/content/cq:graphql/mysite
```

---

# First GraphQL Query

```graphql
{
  articleList {
    items {
      title
      author
    }
  }
}
```

Response

```json
{
  "data": {
    "articleList": {
      "items": [
        {
          "title": "Learning AEM",
          "author": "Vijay"
        },
        {
          "title": "GraphQL Basics",
          "author": "John"
        }
      ]
    }
  }
}
```

---

# Request Flow

```text
React App

↓

GraphQL Query

↓

GraphQL Endpoint

↓

Content Fragment

↓

JSON

↓

React
```

---

# Query by Path

```graphql
{
  articleByPath(
    _path:"/content/dam/mysite/articles/aem-guide"
  ){
    item{
      title
      description
      author
    }
  }
}
```

Response

```json
{
  "data":{
    "articleByPath":{
      "item":{
        "title":"Learning AEM",
        "description":"Complete Guide",
        "author":"Vijay"
      }
    }
  }
}
```

---

# Filtering

Get articles by author:

```graphql
{
  articleList(
    filter:{
      author:{
        _expressions:[
          {
            value:"Vijay"
          }
        ]
      }
    }
  ){
    items{
      title
      author
    }
  }
}
```

---

# Pagination

```graphql
{
  articleList(
    first:5
  ){
    items{
      title
    }
  }
}
```

Returns only the first 5 articles.

---

# Sorting

```graphql
{
  articleList(
    sort:"title ASC"
  ){
    items{
      title
    }
  }
}
```

---

# Nested Models

Example:

Author Model

```text
Author

↓

Name

Email
```

Article Model

```text
Article

↓

Title

↓

Author Reference
```

Query

```graphql
{
  articleList{
    items{
      title
      author{
        name
        email
      }
    }
  }
}
```

Response

```json
{
  "data":{
    "articleList":{
      "items":[
        {
          "title":"AEM",
          "author":{
            "name":"Vijay",
            "email":"vijay@test.com"
          }
        }
      ]
    }
  }
}
```

---

# React Example

```javascript
const query = `
{
  articleList{
    items{
      title
      description
    }
  }
}
`;

fetch("/content/cq:graphql/mysite/endpoint.json", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({ query })
})
.then(response => response.json())
.then(data => console.log(data));
```

---

# Real Project Example 1

News Website

```text
React

↓

GraphQL

↓

News Content Fragment

↓

JSON

↓

React UI
```

---

# Real Project Example 2

Mobile App

```text
Android App

↓

GraphQL

↓

Product Content Fragments

↓

JSON
```

---

# Real Project Example 3

E-Commerce

Content Fragment

```text
Product

↓

Name

↓

Price

↓

Description
```

GraphQL

↓

React

↓

Product Page

---

# GraphQL vs REST

| GraphQL                      | REST                   |
| ---------------------------- | ---------------------- |
| Single endpoint              | Multiple endpoints     |
| Request only required fields | Returns fixed response |
| Better for Headless CMS      | Traditional API style  |
| Excellent for SPAs           | Good for general APIs  |

---

# Best Practices

### ✅ Use Content Fragments

GraphQL works best with structured Content Fragment Models.

---

### ✅ Request Only Needed Fields

Good

```graphql
{
  articleList{
    items{
      title
    }
  }
}
```

Avoid requesting every field if you don't need them.

---

### ✅ Use Pagination

```graphql
first:10
```

Never load thousands of records in one request.

---

### ✅ Filter Data

Use filters to reduce the amount of returned data.

---

# Common Mistakes

### ❌ Using GraphQL for Experience Fragments

GraphQL is intended for **Content Fragments**, not Experience Fragments.

---

### ❌ Returning Too Much Data

Avoid requesting every field if only one or two are needed.

---

### ❌ No Pagination

Large datasets without pagination can affect performance.

---

# Interview Questions

### 1. What is GraphQL?

A query language for APIs that allows clients to request exactly the data they need.

---

### 2. What does AEM GraphQL primarily work with?

**Content Fragments** and **Content Fragment Models**.

---

### 3. Why is GraphQL preferred in headless CMS?

Because it:

* Returns only requested fields.
* Reduces payload size.
* Improves performance.
* Supports nested data retrieval.

---

### 4. Can GraphQL retrieve nested objects?

**Yes.** It can return related Content Fragments in a single query.

---

### 5. How do you limit results?

```graphql
first:10
```

---

### 6. Which frontend frameworks commonly use AEM GraphQL?

* React
* Angular
* Vue.js
* Flutter
* iOS
* Android

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Why would you choose GraphQL over REST in AEM?"**

A strong answer is:

> "I would use GraphQL for headless AEM projects because it allows frontend applications such as React or mobile apps to request only the fields they need from Content Fragments. This reduces payload size, improves performance, and avoids multiple REST API calls for related content. For traditional backend integrations or custom business APIs, REST-based servlets are still a good choice."

This balanced answer demonstrates that you understand when each technology is appropriate.

---

# AEM Backend Roadmap Progress

You have now covered:

* ✅ Sling Models
* ✅ OSGi
* ✅ Servlets
* ✅ Filters
* ✅ Scheduler
* ✅ Workflow
* ✅ JCR
* ✅ QueryBuilder
* ✅ Event Handling
* ✅ Sling Jobs
* ✅ Dispatcher
* ✅ MSM
* ✅ Content Fragments
* ✅ Experience Fragments
* ✅ GraphQL


# Chapter 23: AEM Security (Authentication, Authorization, Service Users & ResourceResolverFactory) ⭐⭐⭐⭐⭐

This topic is asked in almost every **AEM Backend Developer interview (2–10 years)** because secure repository access is critical. It is also covered in your uploaded AEM notes. 

---

# What is AEM Security?

AEM Security ensures that:

* Only authenticated users can log in.
* Only authorized users can access content.
* Backend code securely accesses the JCR.
* Sensitive repository paths are protected.

---

# Security Architecture

```text
Browser
     │
     ▼
Authentication
     │
     ▼
Authorization
     │
     ▼
Servlet / Sling Model
     │
     ▼
Service User
     │
     ▼
ResourceResolver
     │
     ▼
JCR Repository
```

---

# Authentication vs Authorization ⭐⭐⭐⭐⭐

## Authentication

Authentication answers:

> **Who are you?**

Example

```text
Username : admin

Password : admin123
```

If credentials are correct:

✅ Login Successful

---

## Authorization

Authorization answers:

> **What are you allowed to do?**

Example

```text
User : Author

Permissions

✔ Create Page

✔ Edit Page

❌ Delete Users

❌ Modify ACLs
```

---

# Real Example

```text
Employee Logs In

↓

Authentication

↓

Role = Content Author

↓

Authorization

↓

Allowed to edit pages

↓

Cannot access /system/console
```

---

# Service User ⭐⭐⭐⭐⭐

## What is a Service User?

A **Service User** is a special repository user used by backend code.

It:

* Has no password
* Cannot log in through the UI
* Exists only for Java services
* Has limited permissions

Adobe recommends using **Service Users** instead of administrative sessions.

---

# Why Not Admin Session?

Old approach (Not Recommended)

```java
Session session =
repository.loginAdministrative(null);
```

❌ Deprecated

❌ Security Risk

---

Modern approach:

```text
Servlet

↓

ResourceResolverFactory

↓

Service User

↓

ResourceResolver

↓

Repository
```

---

# ResourceResolverFactory ⭐⭐⭐⭐⭐

Inject it:

```java
@Reference
private ResourceResolverFactory resourceResolverFactory;
```

This factory creates ResourceResolvers.

---

# Service ResourceResolver

Create a map

```java
Map<String,Object> authInfo =
new HashMap<>();

authInfo.put(
ResourceResolverFactory.SUBSERVICE,
"product-service"
);
```

Get resolver

```java
ResourceResolver resolver =
resourceResolverFactory
.getServiceResourceResolver(
authInfo
);
```

Now the resolver uses the permissions of the **product-service** service user.

---

# Complete Example

```java
@Component(service = ProductService.class)

public class ProductServiceImpl
implements ProductService {

    @Reference
    private ResourceResolverFactory resolverFactory;

    @Override
    public void updateProduct() {

        Map<String,Object> auth =
                new HashMap<>();

        auth.put(
                ResourceResolverFactory.SUBSERVICE,
                "product-service"
        );

        try(ResourceResolver resolver =
                    resolverFactory
                    .getServiceResourceResolver(auth)) {

            Resource resource =
                    resolver.getResource(
                            "/content/products"
                    );

            // Read or Update JCR

            resolver.commit();

        } catch (LoginException |
                 PersistenceException e) {

            e.printStackTrace();

        }

    }

}
```

---

# Why use try-with-resources?

```java
try(ResourceResolver resolver = ...)
```

The resolver is **automatically closed**, preventing resource leaks.

---

# Subservice Mapping

OSGi Configuration

```text
Bundle

↓

Subservice Name

↓

Service User

↓

Permissions
```

Example

```text
product-service

↓

product-service-user

↓

Read

Write

/content/products
```

---

# Repository Initialization (RepoInit)

Modern AEM projects often create service users using **RepoInit**.

Example

```text
create service user product-service-user
```

Grant permissions

```text
allow jcr:read,jcr:write
on /content/products
to product-service-user
```

---

# Access Control List (ACL)

ACL defines permissions.

Example

```text
/content

↓

Read

↓

Write

↓

Delete
```

Example

```text
Author

↓

Read

Write

No Delete
```

---

# Real Project Example 1

Product Import

```text
Scheduler

↓

Service User

↓

Repository

↓

Products Updated
```

---

# Real Project Example 2

Workflow

```text
Workflow Process

↓

Service User

↓

JCR

↓

Approval Property Updated
```

---

# Real Project Example 3

REST Integration

```text
Servlet

↓

Service User

↓

Read Products

↓

Return JSON
```

---

# ResourceResolver Types

## Request ResourceResolver

```java
ResourceResolver resolver =
request.getResourceResolver();
```

Used inside:

* Servlets
* Sling Models
* Filters

Permissions are based on the logged-in user.

---

## Service ResourceResolver

```java
resourceResolverFactory
.getServiceResourceResolver()
```

Used inside:

* OSGi Services
* Scheduler
* Workflow
* Event Handler
* Sling Jobs

Permissions are based on the service user.

---

# Request Resolver vs Service Resolver

| Request Resolver             | Service Resolver                        |
| ---------------------------- | --------------------------------------- |
| Logged-in user's permissions | Service user's permissions              |
| Used in request processing   | Used in backend/background tasks        |
| Obtained from `request`      | Obtained from `ResourceResolverFactory` |

---

# Best Practices

### ✅ Use Service Users

Never use administrative sessions.

---

### ✅ Give Minimum Permissions

Example

```text
Read

Write

/content/products
```

Not:

```text
/
```

Follow the **Principle of Least Privilege**.

---

### ✅ Close ResourceResolvers

Good

```java
try(ResourceResolver resolver = ...)
```

---

### ✅ Handle LoginException

```java
catch(LoginException e){

}
```

Always handle authentication failures.

---

# Common Mistakes

### ❌ Using admin session

Deprecated and insecure.

---

### ❌ Giving Full Repository Access

Wrong

```text
/
```

Grant only the required paths.

---

### ❌ Forgetting to Close Resolver

Can lead to memory and session leaks.

---

### ❌ Hardcoding Credentials

Never write:

```java
username = "admin";

password = "admin123";
```

in code.

---

# Interview Questions

### 1. What is a Service User?

A Service User is a non-login repository user used by backend code to securely access the JCR.

---

### 2. Why is `loginAdministrative()` deprecated?

Because it grants excessive privileges and creates security risks.

---

### 3. Which class creates a Service ResourceResolver?

```java
ResourceResolverFactory
```

---

### 4. Which method creates the resolver?

```java
getServiceResourceResolver()
```

---

### 5. What is a Subservice?

A logical name that maps a bundle to a Service User through OSGi configuration.

---

### 6. Why use try-with-resources?

To automatically close the `ResourceResolver` and avoid resource leaks.

---

# Enterprise Architecture

```text
Servlet

↓

OSGi Service

↓

ResourceResolverFactory

↓

Service User

↓

ResourceResolver

↓

JCR Repository

↓

Content Updated
```

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do you access the JCR from an OSGi service?"**

A strong answer is:

1. Inject `ResourceResolverFactory`.
2. Create an authentication map with the subservice name.
3. Call `getServiceResourceResolver()`.
4. Use the returned `ResourceResolver` to access the repository.
5. Commit changes if needed.
6. Close the resolver using try-with-resources.

Example:

```java
Map<String, Object> authInfo = new HashMap<>();
authInfo.put(ResourceResolverFactory.SUBSERVICE, "product-service");

try (ResourceResolver resolver =
         resolverFactory.getServiceResourceResolver(authInfo)) {

    Resource resource = resolver.getResource("/content/products");

    // Read or update repository

    resolver.commit();
}
```

This is the **recommended and secure approach** in modern AEM.

---

# AEM Master Roadmap Progress

You have now completed:

* ✅ Core Java for AEM
* ✅ OSGi
* ✅ Sling Models
* ✅ Servlets
* ✅ Filters
* ✅ Scheduler
* ✅ Workflow
* ✅ JCR
* ✅ QueryBuilder
* ✅ Event Handling
* ✅ Sling Jobs
* ✅ Dispatcher
* ✅ MSM
* ✅ Content Fragments
* ✅ Experience Fragments
* ✅ GraphQL
* ✅ AEM Security


---

# Chapter 24: AEM Unit Testing ⭐⭐⭐⭐⭐

---

# What is Unit Testing?

**Unit Testing** means testing a single unit of code (such as a Sling Model, Service, or Servlet) in isolation to verify that it behaves correctly.

Instead of testing the whole application, you test one class at a time.

Example:

```text
ProductService

↓

JUnit Test

↓

Pass / Fail
```

---

# Why Unit Testing?

Benefits:

* Finds bugs early.
* Prevents regressions.
* Makes refactoring safer.
* Improves code quality.
* Increases confidence before deployment.

---

# Unit Testing Architecture

```text
JUnit Test

↓

Mockito

↓

AEM Mocks

↓

Sling Model / Service / Servlet

↓

Assertions
```

---

# Tools Used

| Tool                                  | Purpose                  |
| ------------------------------------- | ------------------------ |
| JUnit 5                               | Test framework           |
| Mockito                               | Mock dependencies        |
| AEM Mocks (`io.wcm.testing.aem-mock`) | Simulate AEM environment |
| AssertJ / JUnit Assertions            | Validate results         |

---

# Maven Dependencies

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>io.wcm</groupId>
    <artifactId>io.wcm.testing.aem-mock.junit5</artifactId>
    <scope>test</scope>
</dependency>
```

---

# JUnit 5 Basics

A simple test:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @Test
    void testAddition() {
        int result = 10 + 20;
        assertEquals(30, result);
    }
}
```

If the expected and actual values match, the test passes.

---

# Common JUnit Assertions

```java
assertEquals(expected, actual);
```

```java
assertNotNull(object);
```

```java
assertNull(object);
```

```java
assertTrue(condition);
```

```java
assertFalse(condition);
```

---

# Mockito

Mockito is used to create **mock objects** for dependencies.

Example Service:

```java
public class ProductService {

    private ProductRepository repository;

    public Product getProduct() {
        return repository.findProduct();
    }
}
```

Test:

```java
@Mock
private ProductRepository repository;

@InjectMocks
private ProductService productService;
```

Configure mock:

```java
when(repository.findProduct())
    .thenReturn(new Product("Laptop"));
```

Verify:

```java
assertEquals(
    "Laptop",
    productService.getProduct().getName()
);
```

---

# AEM Mocks

AEM Mocks simulate an AEM repository without starting AEM.

Create context:

```java
private final AemContext context =
        new AemContext();
```

Create repository content:

```java
context.create().resource(
    "/content/mysite",
    "jcr:title",
    "Home Page"
);
```

Retrieve resource:

```java
Resource resource =
    context.resourceResolver()
           .getResource("/content/mysite");
```

---

# Testing a Sling Model

Sling Model:

```java
@Model(adaptables = Resource.class)
public class ArticleModel {

    @ValueMapValue
    private String title;

    public String getTitle() {
        return title;
    }
}
```

Unit Test:

```java
class ArticleModelTest {

    private final AemContext context =
            new AemContext();

    @BeforeEach
    void setup() {

        context.create().resource(
            "/content/article",
            "title",
            "Learning AEM"
        );

    }

    @Test
    void testTitle() {

        Resource resource =
            context.resourceResolver()
                   .getResource("/content/article");

        ArticleModel model =
            resource.adaptTo(ArticleModel.class);

        assertEquals(
            "Learning AEM",
            model.getTitle()
        );
    }
}
```

---

# Testing an OSGi Service

Service:

```java
public class DiscountService {

    public int discount(int price) {
        return price - 100;
    }
}
```

Test:

```java
class DiscountServiceTest {

    private DiscountService service =
            new DiscountService();

    @Test
    void testDiscount() {

        assertEquals(
            900,
            service.discount(1000)
        );
    }
}
```

---

# Testing a Servlet

Suppose a servlet returns:

```json
{
   "status":"success"
}
```

Use AEM Mock request/response objects:

```java
MockSlingHttpServletRequest request =
    context.request();

MockSlingHttpServletResponse response =
    context.response();
```

Invoke:

```java
servlet.doGet(request, response);
```

Verify:

```java
assertEquals(
    "application/json",
    response.getContentType()
);

assertTrue(
    response.getOutputAsString()
            .contains("success")
);
```

---

# Mocking ResourceResolver

```java
ResourceResolver resolver =
    context.resourceResolver();
```

Mock repository:

```java
context.create().resource(
    "/content/products",
    "name",
    "Laptop"
);
```

Retrieve:

```java
Resource resource =
    resolver.getResource("/content/products");
```

---

# Mocking PageManager

```java
PageManager pageManager =
    context.pageManager();

Page page =
    pageManager.create(
        "/content",
        "home",
        "/conf/template",
        "Home"
    );
```

---

# Real Project Example

Testing a Sling Model:

```text
JUnit

↓

AEM Context

↓

Mock Resource

↓

Adapt to Model

↓

Verify Title
```

---

# Test Lifecycle

```text
@BeforeEach

↓

Setup Repository

↓

@Test

↓

Assertions

↓

Pass / Fail

↓

@AfterEach
```

---

# Best Practices

### ✅ Test one class at a time

Each test should focus on one class and one responsibility.

---

### ✅ Mock external dependencies

Mock:

* Services
* ResourceResolver
* Repository
* External REST APIs

Do not call real systems during unit tests.

---

### ✅ Keep tests independent

Each test should run successfully regardless of the order in which tests execute.

---

### ✅ Use meaningful test names

Good:

```java
testGetTitleReturnsCorrectValue()
```

Bad:

```java
test1()
```

---

# Common Mistakes

### ❌ Depending on a running AEM instance

Unit tests should execute without starting AEM.

---

### ❌ Testing multiple features in one test

Keep each test focused.

---

### ❌ Not using AEM Mocks

AEM-specific classes should generally be tested with AEM Mocks.

---

# Interview Questions

### 1. Which framework is used for unit testing in AEM?

**JUnit 5**.

---

### 2. Why is Mockito used?

To mock dependencies and isolate the class under test.

---

### 3. Why use AEM Mocks?

To simulate the AEM repository and Sling environment without running AEM.

---

### 4. How do you test a Sling Model?

1. Create an `AemContext`.
2. Create a mock resource.
3. Adapt the resource to the Sling Model.
4. Verify values using assertions.

---

### 5. Can Servlets be unit tested?

**Yes.** By using mock request and response objects from AEM Mocks.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do you unit test a Sling Model?"**

A strong answer is:

1. Create an `AemContext`.
2. Add mock content to the repository.
3. Obtain the mock `Resource`.
4. Adapt the resource to the Sling Model.
5. Verify the model values using JUnit assertions.

This demonstrates practical AEM testing experience.

---

# 🎉 Congratulations!

You have now covered the **complete AEM Backend Developer roadmap**, including:

* ✅ Core Java for AEM
* ✅ Sling Models
* ✅ OSGi Services
* ✅ Servlets
* ✅ Filters
* ✅ Scheduler
* ✅ Workflow
* ✅ JCR
* ✅ QueryBuilder
* ✅ Event Handling
* ✅ Sling Jobs
* ✅ Dispatcher
* ✅ MSM
* ✅ Content Fragments
* ✅ Experience Fragments
* ✅ GraphQL
* ✅ AEM Security
* ✅ Unit Testing

## Recommended Next Steps

To become interview-ready, I recommend moving on to:

1. **AEM Design Patterns** (Factory, Adapter, Strategy, Builder, Singleton in AEM).
2. **Adobe Core Components** (deep dive with customization).
3. **Editable Templates** (policies, templates, initial content).
4. **AEM as a Cloud Service** (Cloud Manager, deployment pipeline, immutable repository).
5. **Real Enterprise Project Architecture** (end-to-end application design).
6. **Top 200 AEM Interview Questions** with detailed answers and coding examples.

These topics are what typically distinguish an intermediate AEM developer from a senior one.
Excellent! Now we'll move to **Advanced AEM Design Patterns**, which is one of the most important topics for **3–10 years of AEM interviews**. Design patterns are heavily used in enterprise AEM projects to build maintainable, scalable, and reusable applications.

---

# Chapter 25: AEM Design Patterns ⭐⭐⭐⭐⭐

---

# What is a Design Pattern?

A **Design Pattern** is a reusable solution to a commonly occurring software design problem.

Instead of reinventing the solution every time, developers use proven patterns.

Think of it like architectural blueprints for software.

---

# Why are Design Patterns Important in AEM?

In enterprise AEM projects, design patterns help you:

* Write reusable code.
* Reduce code duplication.
* Improve maintainability.
* Improve testability.
* Build loosely coupled components.

---

# Most Important Design Patterns in AEM

| Pattern   | AEM Usage               | Interview Importance |
| --------- | ----------------------- | -------------------- |
| Singleton | OSGi Services           | ⭐⭐⭐⭐⭐                |
| Factory   | Service creation        | ⭐⭐⭐⭐⭐                |
| Adapter   | Sling `adaptTo()`       | ⭐⭐⭐⭐⭐                |
| Strategy  | Multiple business rules | ⭐⭐⭐⭐                 |
| Builder   | Complex object creation | ⭐⭐⭐                  |
| Observer  | OSGi Events             | ⭐⭐⭐⭐                 |
| Proxy     | Dispatcher/CDN          | ⭐⭐⭐                  |
| MVC       | Sling + HTL             | ⭐⭐⭐⭐⭐                |

---

# 1. Singleton Pattern ⭐⭐⭐⭐⭐

## What is Singleton?

A Singleton ensures that **only one instance** of a class exists.

---

## Example in Java

```java
public class Database {

    private static Database instance;

    private Database() {
    }

    public static Database getInstance() {

        if (instance == null) {
            instance = new Database();
        }

        return instance;
    }
}
```

---

## How AEM Uses Singleton

Every OSGi service is generally managed as a singleton.

```java
@Component(service = ProductService.class)
public class ProductServiceImpl implements ProductService {

}
```

When multiple servlets use this service:

```text
Servlet 1
      │
Servlet 2
      │
Servlet 3
      │
      ▼
Single OSGi Service Instance
```

Only one service instance is created and managed by OSGi.

---

# 2. Factory Pattern ⭐⭐⭐⭐⭐

## What is Factory?

A Factory creates objects without exposing the creation logic.

Instead of:

```java
EmailService service = new EmailService();
```

Use:

```java
NotificationService service =
factory.getService("EMAIL");
```

---

## Example

Interface

```java
public interface NotificationService {

    void send();

}
```

Email Service

```java
@Component(service = NotificationService.class,
property="type=email")
public class EmailService
implements NotificationService {

    @Override
    public void send() {

        System.out.println("Email Sent");

    }

}
```

SMS Service

```java
@Component(service = NotificationService.class,
property="type=sms")
public class SmsService
implements NotificationService {

    @Override
    public void send() {

        System.out.println("SMS Sent");

    }

}
```

Factory

```java
public class NotificationFactory {

    public NotificationService getService(String type) {

        if ("EMAIL".equals(type)) {

            return new EmailService();

        }

        return new SmsService();

    }

}
```

> **In real AEM**, avoid creating OSGi services with `new`. Instead, inject the available services and let OSGi manage their lifecycle.

---

# 3. Adapter Pattern ⭐⭐⭐⭐⭐

This is **the most common design pattern in AEM**.

---

## What is Adapter?

Converts one object into another.

Example

```text
Resource

↓

adaptTo()

↓

Page
```

---

## Example

```java
Resource resource =
resolver.getResource("/content/mysite");

Node node =
resource.adaptTo(Node.class);
```

Or

```java
ValueMap valueMap =
resource.adaptTo(ValueMap.class);
```

Or

```java
Page page =
resource.adaptTo(Page.class);
```

The `adaptTo()` method is a classic Adapter pattern.

---

# 4. Strategy Pattern ⭐⭐⭐⭐

Different algorithms for the same task.

Example

Payment

↓

Credit Card

UPI

PayPal

Net Banking

---

Interface

```java
public interface PaymentService {

    void pay();

}
```

Implementation 1

```java
public class UpiService
implements PaymentService {

    @Override
    public void pay() {

        System.out.println("UPI");

    }

}
```

Implementation 2

```java
public class CardService
implements PaymentService {

    @Override
    public void pay() {

        System.out.println("Card");

    }

}
```

---

# 5. Builder Pattern ⭐⭐⭐

Useful for creating complex objects.

Example

```java
Product product = Product.builder()
        .name("Laptop")
        .price(60000)
        .brand("Dell")
        .build();
```

---

# 6. Observer Pattern ⭐⭐⭐⭐

Used in:

* OSGi Events
* EventAdmin
* EventHandler

Flow

```text
Event

↓

Subscribers

↓

Notification
```

Example

```text
Page Published

↓

Event

↓

Email Service

↓

Analytics

↓

Cache Service
```

---

# 7. MVC Pattern ⭐⭐⭐⭐⭐

AEM follows the MVC architecture.

```text
Browser

↓

HTL (View)

↓

Sling Model (Model)

↓

Servlet / OSGi Service (Controller)

↓

JCR
```

---

# Real Enterprise Example

```text
Browser

↓

HTL

↓

Sling Model

↓

ProductService

↓

QueryBuilder

↓

Repository

↓

JSON

↓

HTL
```

This is the architecture you'll see in many enterprise AEM projects.

---

# Which Pattern Does AEM Use Most?

| Feature                 | Pattern                    |
| ----------------------- | -------------------------- |
| `adaptTo()`             | Adapter                    |
| OSGi Services           | Singleton                  |
| EventAdmin              | Observer                   |
| Sling Models            | MVC                        |
| QueryBuilder            | Builder/Factory style APIs |
| ResourceResolverFactory | Factory                    |

---

# Interview Questions

### 1. Which design pattern is used by `adaptTo()`?

**Adapter Pattern**.

---

### 2. Which pattern is used by OSGi Services?

**Singleton Pattern** (service lifecycle managed by OSGi).

---

### 3. Which pattern is used by EventAdmin?

**Observer Pattern**.

---

### 4. Which architecture does AEM follow?

**MVC (Model-View-Controller)**.

---

### 5. Which class demonstrates the Factory pattern in AEM?

**ResourceResolverFactory** is a good example because it creates `ResourceResolver` instances.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"Which design patterns have you used in AEM?"**

A strong answer is:

* **Singleton**: OSGi Services.
* **Adapter**: `resource.adaptTo(...)`.
* **Factory**: `ResourceResolverFactory` and other factory APIs.
* **Observer**: OSGi EventAdmin and EventHandler.
* **Strategy**: Different business logic implementations (for example, payment or notification services).
* **MVC**: HTL, Sling Models, and Servlets.

---


# Chapter 26: Adobe Core Components ⭐⭐⭐⭐⭐

---

# What are Core Components?

**Core Components** are reusable, production-ready AEM components provided by Adobe.

Instead of creating a Text component, Image component, Carousel, Tabs, etc. from scratch, you use Adobe's Core Components and customize them if needed.

---

# Why Core Components?

Without Core Components:

```text
Developer

↓

Create Text Component

↓

Create Image Component

↓

Create Title Component

↓

Create Carousel Component
```

Lots of development effort.

---

With Core Components:

```text
Adobe Core Components

↓

Text

Image

Title

Button

Carousel

Accordion

Tabs

Teaser

List

Breadcrumb

Navigation

↓

Customize if Needed
```

---

# Benefits

* Faster development
* Adobe supported
* Well tested
* Responsive
* Accessible (WCAG)
* Cloud Service compatible
* Easy to extend

---

# Core Component Architecture

```text
HTL

↓

Proxy Component

↓

Core Component

↓

Sling Model

↓

JCR
```

---

# Core Components Package

Common path:

```text
/apps/core/wcm/components
```

Never modify Adobe's implementation directly.

---

# Most Used Core Components

| Component | Resource Type                                |
| --------- | -------------------------------------------- |
| Text      | `core/wcm/components/text/v2/text`           |
| Image     | `core/wcm/components/image/v3/image`         |
| Title     | `core/wcm/components/title/v3/title`         |
| Button    | `core/wcm/components/button/v2/button`       |
| Carousel  | `core/wcm/components/carousel/v1/carousel`   |
| Tabs      | `core/wcm/components/tabs/v1/tabs`           |
| Accordion | `core/wcm/components/accordion/v1/accordion` |
| List      | `core/wcm/components/list/v4/list`           |
| Teaser    | `core/wcm/components/teaser/v2/teaser`       |

---

# What is a Proxy Component? ⭐⭐⭐⭐⭐

A **Proxy Component** is a custom component that points to a Core Component using:

```text
sling:resourceSuperType
```

This is the recommended approach.

---

# Example Structure

```text
/apps/mysite/components/title

    sling:resourceSuperType

        core/wcm/components/title/v3/title
```

Now your project uses Adobe's Title component while allowing project-specific customization.

---

# sling:resourceSuperType ⭐⭐⭐⭐⭐

This property enables **inheritance**.

Example:

```text
My Title Component

↓

sling:resourceSuperType

↓

Core Title Component
```

---

# Example `.content.xml`

```xml
<jcr:root
    xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Component"
    jcr:title="My Title"
    sling:resourceSuperType="core/wcm/components/title/v3/title"/>
```

---

# HTL Inheritance

Your custom HTL:

```html
<div class="custom-title">

    <sly
        data-sly-resource="${resource @ resourceType='core/wcm/components/title/v3/title'}">
    </sly>

</div>
```

Output:

```text
Custom CSS

↓

Adobe Title Component
```

---

# Extending a Sling Model

Example:

```java
@Model(
    adaptables = Resource.class,
    adapters = MyTitle.class
)
public class MyTitleImpl {

    @Self
    private Resource resource;

    public String getCustomTitle() {

        return "Custom " +
               resource.getValueMap().get(
                   "jcr:title",
                   ""
               );

    }

}
```

---

# Editable Templates Integration

```text
Editable Template

↓

Layout Container

↓

Core Components

↓

Author Adds Components
```

---

# Style System

Core Components support multiple styles.

Example:

```
Title

↓

Default

Large

Blue

Red

Centered
```

The author selects the style without changing code.

---

# Policies

Policies define what authors can do.

Example:

Image Component

Allowed:

* JPEG
* PNG
* WEBP

Maximum Width:

```
1200 px
```

Authors cannot exceed the configured limits.

---

# Real Project Example 1

Homepage

```text
Header

↓

Core Navigation

↓

Core Image

↓

Core Carousel

↓

Core Title

↓

Core Teaser

↓

Footer
```

Very little custom code is needed.

---

# Real Project Example 2

E-Commerce

```text
Product Page

↓

Title Component

↓

Image Component

↓

Button

↓

Tabs

↓

Accordion
```

---

# Real Project Example 3

News Website

```text
Home

↓

List Component

↓

Title Component

↓

Image Component

↓

Breadcrumb

↓

Search
```

---

# Core Components vs Custom Components

| Core Components  | Custom Components         |
| ---------------- | ------------------------- |
| Adobe maintained | Project maintained        |
| Ready to use     | Built from scratch        |
| Upgrade friendly | More maintenance          |
| Responsive       | Depends on implementation |
| Accessible       | Must be implemented       |

---

# Best Practices

### ✅ Always create Proxy Components

Good

```text
/apps/mysite/components/title

↓

resourceSuperType

↓

core title
```

---

### ✅ Never modify Core Components

Do **not** edit:

```text
/apps/core
```

Always extend using Proxy Components.

---

### ✅ Reuse before building

Use an existing Core Component whenever possible.

---

### ✅ Use Editable Templates

Core Components work best with Editable Templates and Policies.

---

# Common Mistakes

### ❌ Copying Core Component code

Don't copy Adobe's implementation unless absolutely necessary.

---

### ❌ Editing Adobe components

Never modify:

```text
/apps/core
```

Your changes may be lost during upgrades.

---

### ❌ Ignoring Policies

Policies provide authoring constraints without writing code.

---

# Interview Questions

### 1. What are Core Components?

Reusable Adobe-provided AEM components that are production-ready and customizable.

---

### 2. What is a Proxy Component?

A project component that inherits from a Core Component using:

```text
sling:resourceSuperType
```

---

### 3. Why use Proxy Components?

* Easy upgrades
* No modification of Adobe code
* Customization with inheritance

---

### 4. What is `sling:resourceSuperType`?

A property that enables component inheritance by pointing to another component.

---

### 5. Can Core Components be customized?

**Yes.** By creating Proxy Components, extending Sling Models, overriding HTL where needed, and using the Style System and Policies.

---

### 6. Where should project components be created?

```text
/apps/<project-name>/components
```

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do you customize Adobe Core Components?"**

A strong answer is:

1. Create a **Proxy Component** under `/apps/<project>/components`.
2. Set the `sling:resourceSuperType` to the required Core Component.
3. Add custom HTL, CSS, or JavaScript if needed.
4. Extend or create a Sling Model for additional business logic.
5. Configure Policies and the Style System instead of hardcoding behavior whenever possible.

This is the **Adobe-recommended approach** and is used in almost every modern AEM project.

---




# Chapter 27: Editable Templates ⭐⭐⭐⭐⭐

**Editable Templates** are the standard way to create pages in **AEM 6.5** and **AEM as a Cloud Service**. Almost every modern AEM project uses them. This topic is also covered in your uploaded AEM notes. 

---

# What is a Template?

A **Template** defines the **structure, layout, and initial content** of a page.

Think of it as a blueprint for creating pages.

Example:

```text
News Page Template

↓

Author creates page

↓

Page generated automatically
```

---

# Why Do We Need Templates?

Without templates:

Every author must create:

* Header
* Footer
* Navigation
* Banner

manually.

With templates:

```text
Template

↓

Header

Footer

Navigation

Layout

↓

Author creates page

↓

Everything already exists
```

---

# Types of Templates

## 1. Static Templates (Old)

Stored in:

```text
/apps
```

Characteristics:

* Developer creates template.
* Code deployment required for changes.
* Less flexible.
* Used in older AEM projects.

---

## 2. Editable Templates (Modern) ⭐⭐⭐⭐⭐

Stored in:

```text
/conf
```

Characteristics:

* Created by template authors.
* No code deployment needed for many changes.
* Highly flexible.
* Recommended by Adobe.

---

# Static vs Editable Templates

| Static Templates                  | Editable Templates          |
| --------------------------------- | --------------------------- |
| `/apps`                           | `/conf`                     |
| Developer controlled              | Template Author controlled  |
| Less flexible                     | Highly flexible             |
| Restart/deployment often required | Mostly configuration-based  |
| Older approach                    | Modern Adobe recommendation |

---

# Editable Template Architecture

```text
Template

↓

Structure

↓

Initial Content

↓

Policies

↓

Page
```

---

# Where Are Editable Templates Stored?

```text
/conf/mysite/settings/wcm/templates
```

Example:

```text
/conf/mysite/settings/wcm/templates/article-page
```

---

# Template Folder Structure

```text
/conf

└── mysite

     └── settings

          └── wcm

               ├── templates

               └── policies
```

---

# Components of an Editable Template

## 1. Structure ⭐⭐⭐⭐⭐

Structure contains content that authors **cannot delete**.

Example:

```text
Header

↓

Navigation

↓

Footer
```

These are locked.

---

## 2. Initial Content ⭐⭐⭐⭐⭐

Initial Content is editable after page creation.

Example:

```text
Welcome to My Website

↓

Author changes

↓

Welcome to Adobe
```

---

## 3. Policies ⭐⭐⭐⭐⭐

Policies define:

* Allowed Components
* Styles
* Design configurations
* Component behavior

---

# Structure vs Initial Content

| Structure           | Initial Content |
| ------------------- | --------------- |
| Locked              | Editable        |
| Shared by all pages | Unique per page |
| Header              | Banner text     |
| Footer              | Main article    |
| Navigation          | Images          |

---

# Template Editor

Go to:

```text
Tools

↓

General

↓

Templates
```

Create:

```text
Article Template
```

---

# Template Type

Choose:

```text
Page Template
```

Based on:

```text
Core Page Component
```

---

# Layout Container

Every Editable Template contains:

```text
Responsive Grid

↓

Layout Container
```

This is where authors add components.

---

# Allowed Components

Example:

```text
Layout Container

↓

Allowed Components

✔ Title

✔ Image

✔ Text

✔ Button

✔ Carousel

✔ Accordion
```

Authors cannot add components that are not allowed by the policy.

---

# Template Flow

```text
Author

↓

Create Page

↓

Choose Template

↓

Page Created

↓

Author Edits Content

↓

Publish
```

---

# Real Project Example 1

Corporate Website

Template:

```text
Corporate Template

↓

Header

↓

Breadcrumb

↓

Responsive Grid

↓

Footer
```

Authors only edit the page content.

---

# Real Project Example 2

News Website

Template

```text
News Template

↓

Header

↓

Article Title

↓

Author

↓

Date

↓

Article Body

↓

Footer
```

Every article follows the same layout.

---

# Real Project Example 3

E-Commerce

Template

```text
Product Template

↓

Header

↓

Product Gallery

↓

Price

↓

Description

↓

Related Products

↓

Footer
```

---

# Policies

Example

Image Component

Policy

```text
Allowed Formats

JPEG

PNG

WEBP
```

Maximum Width

```text
1200 px
```

Style

```text
Rounded

Border

Shadow
```

Authors can only choose the configured options.

---

# Initial Content Example

When a page is created:

```text
Home Page

↓

Welcome to Our Website

↓

Lorem Ipsum...
```

The author can edit this content.

---

# Structure Example

```text
Header

↓

Navigation

↓

Logo

↓

Footer
```

The author cannot remove these items from pages based on the template.

---

# Responsive Design

Editable Templates use:

```text
Layout Container

↓

Responsive Grid

↓

Desktop

Tablet

Mobile
```

This enables responsive page layouts.

---

# Best Practices

### ✅ Use Editable Templates

Adobe recommends Editable Templates for all new projects.

---

### ✅ Use Core Components

Combine Editable Templates with Adobe Core Components.

---

### ✅ Configure Policies

Instead of hardcoding design decisions, configure them using Policies.

---

### ✅ Keep Structure Small

Lock only common content:

* Header
* Footer
* Navigation

Allow authors flexibility in the main content area.

---

# Common Mistakes

### ❌ Using Static Templates in New Projects

Prefer Editable Templates for modern AEM development.

---

### ❌ Locking Too Much Content

If everything is in the Structure, authors cannot customize pages effectively.

---

### ❌ Ignoring Policies

Policies provide reusable design control without additional code.

---

# Interview Questions

### 1. What is an Editable Template?

An Editable Template is a configurable page template stored under `/conf` that allows template authors to define page structure, policies, and initial content.

---

### 2. Where are Editable Templates stored?

```text
/conf/<project>/settings/wcm/templates
```

---

### 3. What is the difference between Structure and Initial Content?

* **Structure**: Shared, locked content that authors cannot remove.
* **Initial Content**: Starting content that authors can modify after page creation.

---

### 4. What are Policies?

Policies define component behavior, allowed components, styles, and design settings.

---

### 5. Which is recommended by Adobe?

**Editable Templates**.

---

### 6. What is the purpose of the Layout Container?

It provides the area where authors can add and arrange allowed components.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain the architecture of an Editable Template."**

A strong answer is:

```text
Editable Template

↓

Template Type

↓

Structure (Locked)

↓

Initial Content (Editable)

↓

Policies

↓

Layout Container

↓

Core Components

↓

Page
```

Then explain:

* The **Structure** contains reusable content like the header and footer.
* **Initial Content** provides default editable content.
* **Policies** control which components and styles are available.
* Authors create pages from the template without developers needing to change code.

This explanation demonstrates a practical understanding of how modern AEM projects are built.

---

# Chapter 28: AEM as a Cloud Service (AEMaaCS) ⭐⭐⭐⭐⭐

---

# What is AEM as a Cloud Service?

**AEM as a Cloud Service (AEMaaCS)** is Adobe's cloud-native version of AEM.

Unlike traditional AEM 6.5 installations where customers manage servers, Adobe manages the infrastructure, scaling, updates, and monitoring.

---

# Traditional AEM vs AEMaaCS

## Traditional AEM 6.5

```text
Developer

↓

Package Manager

↓

Deploy Package

↓

Restart Bundle

↓

Manual Scaling
```

Infrastructure is managed by the customer.

---

## AEM as a Cloud Service

```text
Developer

↓

Git Repository

↓

Cloud Manager

↓

CI/CD Pipeline

↓

Adobe Cloud

↓

Automatic Deployment
```

Infrastructure is managed by Adobe.

---

# AEMaaCS Architecture

```text
Developer
      │
      ▼
Git Repository
      │
      ▼
Cloud Manager
      │
      ▼
CI/CD Pipeline
      │
      ▼
Author
      │
      ▼
Publish
      │
      ▼
Dispatcher
      │
      ▼
CDN
      │
      ▼
Users
```

---

# Main Features

* Cloud-native architecture
* Automatic updates
* Auto scaling
* CI/CD deployment
* Adobe-managed infrastructure
* High availability
* Continuous monitoring

---

# Cloud Manager ⭐⭐⭐⭐⭐

Cloud Manager is Adobe's DevOps platform for:

* Source code management
* Build
* Testing
* Deployment
* Quality checks
* Security scans

---

# Cloud Manager Flow

```text
Developer

↓

Git Commit

↓

Cloud Manager

↓

Build

↓

Code Quality

↓

Security Scan

↓

Deploy

↓

Production
```

---

# CI/CD Pipeline

Pipeline Stages

```text
Git Commit

↓

Build

↓

Unit Tests

↓

Code Quality

↓

Security Tests

↓

Performance Tests

↓

Deploy
```

Every deployment passes through these automated stages.

---

# Git Repository

All code is stored in Git.

```text
Developer

↓

Git Push

↓

Cloud Manager

↓

Deployment
```

No Package Manager deployment in production.

---

# Immutable Repository ⭐⭐⭐⭐⭐

One of the biggest differences in AEMaaCS.

---

## Immutable

Cannot change at runtime.

Examples:

```text
/apps

/libs

OSGi Bundles

Java Code
```

These are deployed only through the CI/CD pipeline.

---

## Mutable

Can change after deployment.

Examples:

```text
/var

/content

/content/dam

/conf
```

Authors continue to create and edit content here.

---

# Immutable vs Mutable

| Immutable   | Mutable              |
| ----------- | -------------------- |
| `/apps`     | `/content`           |
| Java Code   | Pages                |
| Bundles     | Assets               |
| OSGi Config | Content Fragments    |
| HTL         | Experience Fragments |

---

# Autoscaling

Suppose traffic increases.

Without Cloud:

```text
100 Users

↓

Publish Server
```

Later:

```text
100000 Users

↓

Server Crash
```

---

With AEMaaCS:

```text
Traffic Increases

↓

Adobe Detects

↓

Creates More Publish Instances

↓

Traffic Balanced
```

This is automatic.

---

# Dispatcher in Cloud

```text
Browser

↓

CDN

↓

Dispatcher

↓

Publish

↓

Author
```

The CDN caches content globally before requests reach Dispatcher.

---

# CDN

CDN (Content Delivery Network) stores cached content close to users worldwide.

Example:

```text
User (India)

↓

Nearest CDN

↓

Cached HTML

↓

Fast Response
```

This reduces latency.

---

# Deployment Flow

```text
Developer

↓

Git Commit

↓

Cloud Manager

↓

Build

↓

Deploy Author

↓

Deploy Publish

↓

Dispatcher

↓

Complete
```

---

# OSGi Configurations

Stored as code.

Example

```text
ui.config

↓

config.author

↓

config.publish
```

Example structure:

```text
ui.config

    config.author

    config.publish

    config.dev

    config.stage

    config.prod
```

---

# Environment Types

```text
Development

↓

Stage

↓

Production
```

Each environment can have different OSGi configurations.

---

# Real Project Example 1

Developer changes a Sling Model.

```text
Java Code

↓

Git Commit

↓

Cloud Manager

↓

Pipeline

↓

Deploy

↓

Production
```

No manual bundle upload.

---

# Real Project Example 2

Author updates homepage.

```text
Author

↓

Edit Page

↓

Publish

↓

Dispatcher Flush

↓

CDN Updated
```

Content changes do not require code deployment.

---

# Real Project Example 3

High traffic during a sale.

```text
Black Friday

↓

Traffic x10

↓

Auto Scaling

↓

New Publish Instances

↓

No Downtime
```

---

# Best Practices

### ✅ Store code in Git

Never make production code changes directly.

---

### ✅ Follow CI/CD

All deployments should go through Cloud Manager.

---

### ✅ Keep `/apps` immutable

Do not expect to modify code directly in production.

---

### ✅ Write Unit Tests

Cloud Manager runs automated tests during the pipeline.

---

### ✅ Use Dispatcher and CDN efficiently

Optimize caching for better performance.

---

# Common Mistakes

### ❌ Uploading packages directly in Production

In AEMaaCS, production deployments should go through Cloud Manager.

---

### ❌ Modifying `/apps` directly

Changes will not persist because `/apps` is immutable.

---

### ❌ Ignoring Cloud Manager quality gates

Failing code quality or security checks blocks deployments.

---

### ❌ Hardcoding environment values

Use environment-specific OSGi configurations instead.

---

# Interview Questions

### 1. What is AEM as a Cloud Service?

A cloud-native version of AEM where Adobe manages infrastructure, updates, scaling, and deployments.

---

### 2. What is Cloud Manager?

Adobe's CI/CD and DevOps platform for building, testing, and deploying AEM applications.

---

### 3. What is an Immutable Repository?

Repository areas such as `/apps` and application code that cannot be modified directly at runtime.

---

### 4. What is a Mutable Repository?

Repository areas like `/content`, `/content/dam`, and `/conf` where authors can create and update content.

---

### 5. How is code deployed?

```text
Git

↓

Cloud Manager

↓

CI/CD Pipeline

↓

Production
```

---

### 6. Does AEMaaCS support auto scaling?

**Yes.** Publish instances scale automatically based on traffic.

---

### 7. Is Package Manager used for production deployments?

**No.** Cloud Manager pipelines are the recommended deployment mechanism.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"What are the major differences between AEM 6.5 and AEM as a Cloud Service?"**

A strong answer is:

| AEM 6.5                                                | AEMaaCS                                               |
| ------------------------------------------------------ | ----------------------------------------------------- |
| Customer manages infrastructure                        | Adobe manages infrastructure                          |
| Manual deployments are common                          | Git + Cloud Manager CI/CD                             |
| Manual scaling                                         | Automatic scaling                                     |
| Manual upgrades                                        | Continuous Adobe updates                              |
| Runtime code changes are possible in some environments | `/apps` is immutable; code changes require deployment |

Then conclude:

> "AEM as a Cloud Service emphasizes cloud-native development, immutable infrastructure, automated deployments through Cloud Manager, and scalable, highly available architecture."

This demonstrates that you understand not only the features but also the architectural mindset required for modern AEM development.

---

# 🎉 AEM Backend Master Course Progress

You have now completed:

* ✅ Core Java for AEM
* ✅ Sling
* ✅ Sling Models
* ✅ OSGi
* ✅ Servlets
* ✅ Filters
* ✅ Scheduler
* ✅ Workflow
* ✅ JCR
* ✅ QueryBuilder
* ✅ Event Handling
* ✅ Sling Jobs
* ✅ Dispatcher
* ✅ MSM
* ✅ Content Fragments
* ✅ Experience Fragments
* ✅ GraphQL
* ✅ AEM Security
* ✅ Unit Testing
* ✅ Design Patterns
* ✅ Core Components
* ✅ Editable Templates
* ✅ AEM as a Cloud Service


# Chapter 29: OSGi Configuration Deep Dive ⭐⭐⭐⭐⭐

This topic is asked in almost every **3–10 years AEM interview** because every enterprise application uses OSGi configurations for environment-specific settings.

---

# What is OSGi Configuration?

OSGi Configuration allows you to **externalize application settings** instead of hardcoding them in Java.

Instead of:

```java
String apiUrl = "https://api.company.com";
```

Use OSGi Configuration:

```text
apiUrl=https://api.company.com
```

Now the value can be changed **without modifying Java code**.

---

# Why OSGi Configuration?

Without Configuration

```text
Java Code

↓

Hardcoded URL

↓

Rebuild Project

↓

Deploy Again
```

With OSGi Configuration

```text
Java Code

↓

Configuration

↓

Change Value

↓

Restart Configuration

↓

Done
```

No code changes required.

---

# Real Enterprise Example

Development

```text
API URL

https://dev-api.company.com
```

Stage

```text
https://stage-api.company.com
```

Production

```text
https://api.company.com
```

Same Java code.

Different configurations.

---

# OSGi Configuration Architecture

```text
OSGi Configuration

↓

Configuration Admin

↓

OSGi Service

↓

Servlet

↓

Browser
```

---

# Types of OSGi Configuration

| Type                    | Purpose                          |
| ----------------------- | -------------------------------- |
| Singleton Configuration | One configuration instance       |
| Factory Configuration   | Multiple configuration instances |
| Run Mode Configuration  | Different environments           |
| Configurations in Cloud | Environment-specific settings    |

---

# Modern OSGi Configuration

Create an interface.

```java
package com.mysite.core.config;

import org.osgi.service.metatype.annotations.ObjectClassDefinition;
import org.osgi.service.metatype.annotations.AttributeDefinition;

@ObjectClassDefinition(
        name = "Product API Configuration",
        description = "Configuration for Product API"
)
public @interface ProductConfig {

    @AttributeDefinition(
            name = "API URL",
            description = "Product Service URL"
    )
    String apiUrl() default "https://dev-api.company.com";

    @AttributeDefinition(
            name = "Connection Timeout"
    )
    int timeout() default 5000;

    @AttributeDefinition(
            name = "Enable API"
    )
    boolean enabled() default true;

}
```

---

# Understanding the Annotations

## `@ObjectClassDefinition`

Defines an OSGi configuration.

```java
@ObjectClassDefinition(
name="Product API Configuration"
)
```

This appears in the OSGi Configuration Console.

---

## `@AttributeDefinition`

Defines one configuration property.

```java
@AttributeDefinition(
name="API URL"
)
```

Creates a field:

```text
API URL

____________________
```

---

# Using Configuration in Service

```java
@Component(service = ProductService.class)
@Designate(
        ocd = ProductConfig.class
)
public class ProductService {

    private String apiUrl;

    private int timeout;

    @Activate
    protected void activate(ProductConfig config) {

        apiUrl = config.apiUrl();

        timeout = config.timeout();

    }

}
```

---

# What is `@Designate`?

It connects:

```text
Configuration

↓

Java Service
```

Without it, the service won't receive the configuration.

---

# What is `@Activate`?

Called when:

* Bundle starts
* Configuration changes
* Bundle restarts

Example

```java
@Activate
protected void activate(
ProductConfig config){

}
```

---

# Reading Configuration

```java
System.out.println(apiUrl);

System.out.println(timeout);
```

Output

```text
https://api.company.com

5000
```

---

# Updating Configuration

Go to:

```text
/system/console/configMgr
```

Find

```text
Product API Configuration
```

Update

```text
API URL

https://prod-api.company.com
```

Save.

AEM automatically calls:

```java
@Activate
```

again.

---

# Configuration Lifecycle

```text
Bundle Starts

↓

Configuration Loaded

↓

@Activate

↓

Service Ready

↓

Configuration Updated

↓

@Activate Again
```

---

# Factory Configuration

Sometimes one configuration isn't enough.

Example

Email Service

```text
Email Server 1

↓

Email Server 2

↓

Email Server 3
```

Factory Configurations create multiple instances.

---

Example

```java
@Component(service=EmailService.class)

@Designate(
ocd=EmailConfig.class,
factory=true
)
```

Now multiple configurations can exist.

---

# Run Modes

Different environments use different configuration folders.

```text
config.author

config.publish

config.dev

config.stage

config.prod
```

Example

Development

```text
config.dev
```

Production

```text
config.prod
```

---

# Folder Structure

```text
ui.config

    config.author

    config.publish

    config.dev

    config.stage

    config.prod
```

---

# Real Project Example

Payment API

Development

```text
https://dev-payment.company.com
```

Production

```text
https://payment.company.com
```

Same Java code.

Different configurations.

---

# Best Practices

## ✅ Never Hardcode URLs

Bad

```java
String url="https://api";
```

Good

```java
config.apiUrl();
```

---

## ✅ Use Different Configurations

Keep separate values for:

* Dev
* QA
* Stage
* Production

---

## ✅ Keep Secrets Secure

Don't hardcode:

* Passwords
* Tokens
* API Keys

Use secure configuration mechanisms appropriate for your environment.

---

## ✅ Use Meaningful Names

Good

```text
Payment API Configuration
```

Bad

```text
Test Config
```

---

# Common Mistakes

### ❌ Hardcoded URLs

```java
String url="localhost";
```

Wrong.

---

### ❌ Forgetting `@Designate`

Configuration won't bind correctly.

---

### ❌ Not Using `@Activate`

Configuration values won't be initialized or refreshed.

---

# Interview Questions

### 1. What is OSGi Configuration?

A mechanism to externalize application settings from Java code.

---

### 2. Which annotation defines a configuration?

```java
@ObjectClassDefinition
```

---

### 3. Which annotation connects configuration to a service?

```java
@Designate
```

---

### 4. Which method receives configuration values?

```java
@Activate
```

---

### 5. What is Factory Configuration?

A configuration that allows multiple instances of the same configuration type.

---

### 6. Why use OSGi Configuration?

* Environment-specific values
* No hardcoded values
* Easier maintenance
* No code changes for configuration updates

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"How do you implement environment-specific API URLs in AEM?"**

A strong answer is:

1. Create an interface annotated with `@ObjectClassDefinition`.
2. Define properties using `@AttributeDefinition`.
3. Bind it to the service using `@Designate`.
4. Read values in an `@Activate` method.
5. Store different configuration files in `config.dev`, `config.stage`, and `config.prod` (or the corresponding Cloud Service environment configurations).

This is the standard enterprise approach.

---




# Chapter 30: Apache Sling Internals ⭐⭐⭐⭐⭐

---

# What is Apache Sling?

**Apache Sling** is the web framework on which AEM is built.

Unlike traditional Java web applications, Sling is **resource-based**, not servlet-path-based.

Traditional Java:

```text
URL
 ↓
Servlet
 ↓
Response
```

AEM Sling:

```text
URL
 ↓
Resource Resolver
 ↓
Resource
 ↓
Servlet / HTL Script
 ↓
Response
```

---

# Why Sling?

Sling provides:

* Resource-based architecture
* URL mapping
* Resource resolution
* Script resolution
* HTL rendering
* Servlet resolution
* JCR integration

Everything in AEM depends on Sling.

---

# Complete Sling Request Flow ⭐⭐⭐⭐⭐

```text
Browser
   │
   ▼
HTTP Request
   │
   ▼
Apache Web Server
   │
   ▼
Dispatcher
   │
   ▼
AEM Publish
   │
   ▼
Sling Main Servlet
   │
   ▼
Resource Resolver
   │
   ▼
Resource
   │
   ▼
Resource Type
   │
   ▼
HTL Script / Servlet
   │
   ▼
HTML Response
   │
   ▼
Browser
```

This is the complete request lifecycle in AEM.

---

# Step 1: Browser Request

Example:

```text
http://localhost:4502/content/mysite/en/home.html
```

Browser sends an HTTP GET request.

---

# Step 2: Dispatcher

Dispatcher checks:

```text
Cache Exists?

YES
 ↓
Return HTML

NO
 ↓
Forward to AEM
```

---

# Step 3: Sling Main Servlet

Every request reaches:

```text
org.apache.sling.engine.impl.SlingMainServlet
```

This is the central entry point for Sling request processing.

---

# Step 4: Resource Resolution ⭐⭐⭐⭐⭐

Example URL:

```text
/content/mysite/en/home.html
```

Sling resolves it to the JCR resource:

```text
/content/mysite/en/home
```

Repository:

```text
/content

   mysite

      en

         home
```

The URL maps to a JCR resource.

---

# Step 5: Resource

Example

```text
Resource

↓

/content/mysite/en/home
```

Resource properties

```text
jcr:title = Home

sling:resourceType =
mysite/components/page
```

---

# Step 6: Resource Type ⭐⭐⭐⭐⭐

This property tells Sling which component should render the resource.

Example

```text
sling:resourceType

↓

mysite/components/page
```

Now Sling searches for:

```text
/apps/mysite/components/page
```

---

# HTL Rendering

Inside

```text
/apps/mysite/components/page
```

Sling finds:

```text
page.html
```

HTL

```html
<h1>${properties.jcr:title}</h1>
```

Output

```html
<h1>Home</h1>
```

---

# Resource Resolution Architecture

```text
URL

↓

Resource Resolver

↓

JCR Resource

↓

Resource Type

↓

Component

↓

HTL
```

---

# What is `sling:resourceType`?

This property identifies **which component renders the resource**.

Example

```text
Page

↓

sling:resourceType

↓

mysite/components/page
```

Without it, Sling cannot determine which component to use.

---

# What is `sling:resourceSuperType`?

It enables component inheritance.

Example

```text
My Title Component

↓

resourceSuperType

↓

Core Title Component
```

If your component doesn't provide a script, Sling looks in the super type.

---

# Script Resolution ⭐⭐⭐⭐⭐

Suppose

```text
Resource Type

↓

mysite/components/title
```

Sling searches:

```text
/apps/mysite/components/title/title.html
```

If not found:

```text
resourceSuperType

↓

core/wcm/components/title

↓

title.html
```

This is how inheritance works.

---

# Servlet Resolution

Suppose a request is:

```text
/bin/product
```

Servlet

```java
@Component(service = Servlet.class)

@SlingServletPaths("/bin/product")
```

Sling matches the request path and executes the servlet.

---

# Resource Type Servlet

Instead of path:

```java
@SlingServletResourceTypes(
resourceTypes="mysite/components/page"
)
```

Whenever a resource of this type is requested, Sling invokes the servlet.

---

# Request Processing Example

User opens:

```text
/content/mysite/en/home.html
```

Flow

```text
Browser

↓

Dispatcher

↓

Sling Main Servlet

↓

Resource Resolver

↓

Page Resource

↓

resourceType

↓

page.html

↓

HTL

↓

Response
```

---

# Component Rendering

Page

```text
Header

↓

Navigation

↓

Banner

↓

Content

↓

Footer
```

Each component repeats the same process:

```text
Resource

↓

resourceType

↓

HTL

↓

HTML
```

---

# Real Project Example

Homepage

```text
Home Page

↓

Title Component

↓

Image Component

↓

Carousel

↓

Text

↓

Button
```

Each component has:

```text
Resource

↓

resourceType

↓

HTL

↓

HTML
```

---

# Resource Resolution Example

Repository

```text
/content/mysite/en/home

↓

jcr:content

↓

root

↓

title

↓

image

↓

text
```

Each node contains:

```text
sling:resourceType
```

which determines how it is rendered.

---

# Sling Adaptation

```java
Resource resource =
resolver.getResource(path);

Page page =
resource.adaptTo(Page.class);

Node node =
resource.adaptTo(Node.class);

ValueMap map =
resource.adaptTo(ValueMap.class);
```

`adaptTo()` is used throughout Sling to convert one object into another.

---

# Best Practices

### ✅ Use Resource Types

Prefer resource-type-based components over hardcoded servlet paths when building page components.

---

### ✅ Use `resourceSuperType`

Reuse and extend Adobe Core Components instead of copying them.

---

### ✅ Keep Components Small

Each component should have a single responsibility.

---

### ✅ Prefer HTL

Use HTL for presentation and Sling Models for business logic.

---

# Common Mistakes

### ❌ Hardcoding Paths

Avoid embedding repository paths directly in code unless necessary.

---

### ❌ Copying Core Components

Use inheritance with `sling:resourceSuperType`.

---

### ❌ Business Logic in HTL

Keep business logic in Sling Models or OSGi Services.

---

# Interview Questions

### 1. What is Apache Sling?

Apache Sling is the resource-oriented web framework that AEM is built on. It maps HTTP requests to JCR resources and renders them using scripts or servlets.

---

### 2. What is `sling:resourceType`?

It specifies the component responsible for rendering a resource.

---

### 3. What is `sling:resourceSuperType`?

It enables component inheritance by pointing to a parent component.

---

### 4. What is Resource Resolution?

The process of mapping a request URL to a JCR resource.

---

### 5. What is Script Resolution?

The process of locating the appropriate HTL script or servlet based on the resource type.

---

### 6. What is the role of `SlingMainServlet`?

It is the central entry point that receives requests and coordinates resource resolution, servlet/script resolution, and response generation.

---

# Real Interview Tip ⭐

If an interviewer asks:

> **"Explain the complete request lifecycle in AEM."**

A strong answer is:

```text
Browser
   ↓
Dispatcher
   ↓
AEM Publish
   ↓
Sling Main Servlet
   ↓
Resource Resolution
   ↓
JCR Resource
   ↓
sling:resourceType
   ↓
HTL Script / Servlet
   ↓
Sling Model (if used)
   ↓
OSGi Service (if needed)
   ↓
JCR / External APIs
   ↓
HTML Response
   ↓
Browser
```

Then explain:

* **Dispatcher** handles caching and filtering.
* **SlingMainServlet** receives the request.
* **ResourceResolver** maps the URL to a JCR resource.
* **`sling:resourceType`** determines the component.
* **HTL** renders the view.
* **Sling Models** provide presentation data.
* **OSGi Services** execute business logic.
* The generated HTML is returned to the browser.

This is one of the strongest answers you can give in an AEM interview because it demonstrates a complete understanding of how the platform works internally.

---

# Chapter 31: Oak Indexing & Performance Tuning ⭐⭐⭐⭐⭐

This topic is **very important for Senior AEM Developers (4–10 years)** because slow queries and indexing issues are common in production systems.

---

# What is Oak?

**Apache Jackrabbit Oak** is the **content repository (JCR) implementation** used by AEM.

Everything in AEM is stored in Oak:

* Pages
* Assets
* Content Fragments
* Experience Fragments
* User data
* OSGi configurations

Example:

```text
/content
    mysite
       en
          home

/content/dam
    images
       logo.png
```

---

# Why Do We Need Indexes?

Imagine a library with **10 million books**.

Without an index:

```text
Search Book

↓

Check Book 1

↓

Check Book 2

↓

Check Book 3

↓

...

↓

Find Book
```

Very slow.

With an index:

```text
Search Book

↓

Index

↓

Book Location

↓

Done
```

Very fast.

Oak indexes work the same way.

---

# What Happens Without an Index?

Suppose you execute:

```sql
SELECT *
FROM [cq:Page]
WHERE [jcr:title]='Home'
```

Without an index:

```text
Repository

↓

Scan Every Node

↓

Find Result

↓

Slow Query
```

This is called **Repository Traversal**.

---

# With an Index

```text
Repository

↓

Index Lookup

↓

Result

↓

Fast
```

---

# Oak Query Flow

```text
Query

↓

Query Engine

↓

Index

↓

Repository

↓

Result
```

---

# Types of Oak Indexes

| Index Type     | Purpose            |
| -------------- | ------------------ |
| Property Index | Search by property |
| Lucene Index   | Full-text search   |
| Ordered Index  | Sorting            |
| Traversal      | No index (slow)    |

---

# Property Index

Best for:

```text
jcr:title

status

category

author
```

Example:

```sql
SELECT *
FROM [cq:Page]
WHERE [status]='Published'
```

Uses:

```text
Property Index
```

---

# Lucene Index ⭐⭐⭐⭐⭐

Most commonly used in AEM.

Supports:

* Full-text search
* Multiple properties
* Complex queries
* Content search

Example:

```sql
SELECT *
FROM [dam:Asset]
WHERE CONTAINS(*,'Laptop')
```

Lucene Index returns results quickly.

---

# Repository Traversal

Worst-case scenario:

```text
Repository

↓

Read Every Node

↓

Very Slow
```

Large repositories can take several seconds or even minutes for poorly indexed queries.

---

# Explain Query

Go to:

```text
Tools

↓

Operations

↓

Diagnosis

↓

Query Performance
```

Or use the Query Performance tools available in AEM.

This shows:

```text
Query

↓

Used Index

↓

Traversal?

↓

Cost

↓

Execution Time
```

---

# Example

Query:

```sql
SELECT *
FROM [cq:Page]
WHERE [category]='News'
```

Result:

```text
Lucene Index Used

Execution Time

5 ms
```

Good.

---

Bad Example

```sql
SELECT *
FROM [nt:base]
```

Result:

```text
Traversal

Execution Time

5000 ms
```

Bad.

---

# Query Cost

Oak calculates:

```text
Query

↓

Cost Estimation

↓

Choose Best Index
```

Lower cost = Better index.

---

# Creating a Custom Index

Example:

```text
/oak:index

    productIndex
```

Definition

```text
type = lucene

async = async

includedPaths = /content/products
```

---

# Index Definition Structure

```text
/oak:index

    myIndex

        type = lucene

        async = async

        includedPaths

        indexRules

        properties
```

---

# Real Project Example

Product Search

```text
Products

↓

100000 Nodes

↓

Lucene Index

↓

Search

↓

50 ms
```

Without index:

```text
Traversal

↓

15 seconds
```

---

# QueryBuilder Performance

Good

```java
map.put("path", "/content/products");
map.put("type", "cq:Page");
map.put("p.limit", "20");
```

Bad

```java
map.put("type", "cq:Page");
```

No path means searching a much larger part of the repository.

---

# Explain Query Output

Good

```text
Index Used

Execution

20 ms
```

Bad

```text
Traversal

Execution

7000 ms
```

---

# Performance Best Practices

## ✅ Always Use Path Restrictions

Good

```java
map.put("path", "/content/mysite");
```

This limits the search scope.

---

## ✅ Limit Results

```java
map.put("p.limit", "20");
```

Avoid loading thousands of results.

---

## ✅ Use Lucene Indexes

For:

* Full-text search
* Complex queries
* DAM searches

---

## ✅ Avoid Traversal

Always ensure important queries use an appropriate index.

---

## ✅ Check Query Performance

Before deploying a new query to production, verify that it uses an index.

---

# Common Performance Problems

### ❌ No Index

```sql
SELECT *
FROM [cq:Page]
```

Can cause repository traversal.

---

### ❌ No Path Restriction

Searching the entire repository is usually unnecessary.

---

### ❌ Returning Thousands of Results

Always paginate or limit result sets.

---

### ❌ Using Full-Text Everywhere

Use exact property queries when appropriate.

---

# Performance Optimization Flow

```text
Slow Query

↓

Explain Query

↓

Traversal?

↓

Create Index

↓

Deploy

↓

Fast Query
```

---

# Interview Questions

### 1. What is Oak?

Apache Jackrabbit Oak is the JCR repository implementation used by AEM.

---

### 2. Why are indexes needed?

Indexes allow Oak to locate content quickly instead of scanning every node.

---

### 3. What is repository traversal?

A repository-wide scan that occurs when no suitable index is available for a query.

---

### 4. Which index is commonly used for full-text search?

**Lucene Index**.

---

### 5. How do you identify a slow query?

Use AEM's Query Performance tools or Explain Query to verify whether an index is used and whether traversal occurs.

---

### 6. How can you improve QueryBuilder performance?

* Restrict by path.
* Use `p.limit`.
* Search indexed properties.
* Ensure suitable Oak indexes exist.

---

# Real Interview Tip ⭐

If the interviewer asks:

> **"A QueryBuilder query is taking 10 seconds. How would you troubleshoot it?"**

A strong answer is:

1. Check the query in **Query Performance/Explain Query**.
2. Verify whether the query is using an index or falling back to repository traversal.
3. Add a **path restriction** if it's missing.
4. Limit the number of results with `p.limit`.
5. If necessary, create or update a **Lucene index** for the queried properties.
6. Re-test the query to confirm improved performance.

This shows both your understanding of Oak internals and your practical production troubleshooting skills.

---

# Senior AEM Topics Completed

You have now completed:

* ✅ Sling Internals
* ✅ OSGi Configuration
* ✅ Dispatcher
* ✅ Oak Indexing & Performance Tuning
* ✅ GraphQL
* ✅ MSM
* ✅ AEM Security
* ✅ Unit Testing
* ✅ Core Components
* ✅ Editable Templates
* ✅ AEM as a Cloud Service



---

# Chapter 32: Real Enterprise AEM Project (E-Commerce Website) ⭐⭐⭐⭐⭐

## Project Scenario

Suppose your company wants to build an online electronics store.

Website:

```text
https://electronics.company.com
```

Features:

* Home Page
* Product Listing
* Product Details
* Search
* Shopping Promotions
* Contact Page
* Admin Authoring
* Headless API
* Multi-language Support

---

# Enterprise Architecture

```text
                    Browser
                       │
                Apache/CDN
                       │
                  Dispatcher
                       │
      ┌────────────────┴────────────────┐
      │                                 │
   Publish 1                       Publish 2
      │                                 │
      └──────────────┬──────────────────┘
                     │
                 Author
                     │
              JCR (Oak Repository)
                     │
     Sling Models / OSGi Services
                     │
      External APIs (Product, Payment)
```

---

# Maven Project Structure

```text
electronics-site/

│── all/
│── core/
│── ui.apps/
│── ui.content/
│── ui.config/
│── ui.frontend/
│── dispatcher/
│── pom.xml
```

---

# Module Responsibilities

| Module      | Purpose                                     |
| ----------- | ------------------------------------------- |
| core        | Java code, Sling Models, Services, Servlets |
| ui.apps     | Components, HTL, Dialogs                    |
| ui.content  | Sample content                              |
| ui.config   | OSGi configurations                         |
| ui.frontend | CSS, JS, TypeScript                         |
| dispatcher  | Dispatcher configuration                    |
| all         | Deployment package                          |

---

# Repository Structure

```text
/content/electronics

    en

        home

        products

        contact

/content/dam/electronics

/conf/electronics

/apps/electronics
```

---

# Components

```text
Header

Navigation

Hero Banner

Product List

Product Card

Search

Footer
```

Each is built as a reusable component.

---

# Component Example

```text
/apps/electronics/components

    header

    footer

    hero

    productcard

    productlist

    search
```

---

# Product Card Component

Repository

```text
product1

name = Laptop

price = 65000

image = laptop.jpg
```

Sling Model

```java
@Model(adaptables = Resource.class)
public class ProductModel {

    @ValueMapValue
    private String name;

    @ValueMapValue
    private Integer price;

    public String getName() {
        return name;
    }

    public Integer getPrice() {
        return price;
    }
}
```

HTL

```html
<h2>${model.name}</h2>

<p>${model.price}</p>
```

Output

```html
Laptop

65000
```

---

# OSGi Service

Interface

```java
public interface ProductService {

    List<Product> getProducts();

}
```

Implementation

```java
@Component(service = ProductService.class)
public class ProductServiceImpl
implements ProductService {

    @Override
    public List<Product> getProducts(){

        return new ArrayList<>();

    }

}
```

---

# Servlet

```java
@Component(service = Servlet.class)

@SlingServletPaths("/bin/products")
```

Response

```json
{
"products":[
{
"name":"Laptop",
"price":65000
}
]
}
```

---

# QueryBuilder

Search Products

```java
map.put(
"path",
"/content/products"
);

map.put(
"type",
"cq:Page"
);

map.put(
"property",
"category"
);

map.put(
"property.value",
"Laptop"
);
```

---

# Workflow

```text
Author Creates Product

↓

Workflow Starts

↓

Manager Approval

↓

Publish
```

---

# Event Handling

```text
Product Published

↓

Event

↓

Email

↓

Search Index

↓

Analytics
```

---

# Dispatcher

```text
Browser

↓

Dispatcher

↓

Cache?

↓

Yes

↓

HTML

↓

No

↓

Publish
```

---

# GraphQL

Mobile App

↓

GraphQL

↓

Content Fragment

↓

JSON

Query

```graphql
{
productList{

items{

name

price

}

}

}
```

---

# Editable Templates

```text
Home Template

↓

Header

↓

Banner

↓

Layout Container

↓

Footer
```

---

# Core Components

```text
Navigation

Title

Image

Carousel

Accordion

Button

Teaser
```

Customized using:

```text
resourceSuperType
```

---

# Security

```text
Servlet

↓

Service User

↓

ResourceResolverFactory

↓

JCR
```

No admin sessions.

---

# Cloud Deployment

```text
Git

↓

Cloud Manager

↓

CI/CD

↓

Author

↓

Publish

↓

Dispatcher
```

---

# Complete Request Flow

```text
Browser

↓

Dispatcher

↓

Publish

↓

Sling Main Servlet

↓

Resource Resolver

↓

Sling Model

↓

OSGi Service

↓

Oak Repository

↓

HTL

↓

HTML

↓

Browser
```

---

# Project Folder Structure

```text
electronics-site

core

    models

    services

    servlets

    schedulers

    workflows

ui.apps

    components

    templates

    dialogs

dispatcher

ui.config

ui.content
```

---

# Real Production Flow

```text
Author Creates Product

↓

Workflow Approval

↓

Publish

↓

Dispatcher Flush

↓

CDN Refresh

↓

Customer Opens Website

↓

Dispatcher Cache

↓

HTML Returned
```

---

# Technologies Used

| Technology         | Purpose                      |
| ------------------ | ---------------------------- |
| Sling Models       | Business data for components |
| HTL                | Presentation layer           |
| OSGi               | Services                     |
| QueryBuilder       | Search                       |
| JCR                | Content storage              |
| Dispatcher         | Cache                        |
| GraphQL            | Headless APIs                |
| Core Components    | UI                           |
| Editable Templates | Page creation                |
| Workflow           | Approval                     |
| Cloud Manager      | Deployment                   |

---

# Enterprise Best Practices

✅ Use Sling Models for presentation logic.

✅ Keep business logic in OSGi Services.

✅ Reuse Core Components through Proxy Components.

✅ Use Editable Templates and Policies.

✅ Use Service Users for repository access.

✅ Optimize QueryBuilder queries with path restrictions and indexes.

✅ Configure Dispatcher caching and invalidation.

✅ Store environment-specific values in OSGi configurations.

✅ Write JUnit tests with AEM Mocks.

---

# Common Interview Questions

### 1. Explain your AEM project architecture.

Describe the request flow from Browser → Dispatcher → Publish → Sling → JCR → HTL and explain the role of Sling Models, OSGi Services, and Dispatcher.

---

### 2. How do you structure an AEM project?

Using Maven modules such as `core`, `ui.apps`, `ui.content`, `ui.config`, `dispatcher`, and `all`.

---

### 3. Where is business logic written?

In **OSGi Services**, while Sling Models prepare data for the view.

---

### 4. Where are components created?

Under:

```text
/apps/<project>/components
```

---

### 5. How is deployment done in AEM as a Cloud Service?

Using **Git → Cloud Manager → CI/CD Pipeline → Deployment**.

---

# Final Interview Tip ⭐

If an interviewer asks:

> **"Explain a real AEM project you worked on."**

You can structure your answer like this:

1. **Project Overview** – Explain the business domain (e-commerce, banking, media, healthcare, etc.).
2. **Architecture** – Mention Author, Publish, Dispatcher, CDN, and Cloud Manager.
3. **Frontend** – HTL, Core Components, Editable Templates.
4. **Backend** – Sling Models, OSGi Services, Servlets, QueryBuilder, Workflows.
5. **Repository** – JCR, Oak, Content Fragments, Experience Fragments.
6. **Security** – Service Users and `ResourceResolverFactory`.
7. **Deployment** – Git, Cloud Manager, CI/CD.
8. **Performance** – Dispatcher caching, Oak indexing, Query optimization.
9. **Testing** – JUnit 5, Mockito, AEM Mocks.

This gives a complete, structured answer that demonstrates real-world AEM experience.

---

# 🎉 Congratulations!

You have now completed a comprehensive AEM Backend learning path covering:

* Core Java for AEM
* Sling & Sling Models
* OSGi
* Servlets & Filters
* JCR & Oak
* QueryBuilder
* Workflows
* Dispatcher
* MSM
* Content & Experience Fragments
* GraphQL
* Security
* Unit Testing
* Core Components
* Editable Templates
* AEM as a Cloud Service
* OSGi Configuration
* Sling Internals
* Oak Performance
* Enterprise Project Architecture
