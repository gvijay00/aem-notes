---
title: AEM Backend

---

Perfect! We'll build this as a complete **AEM Master Course** based on your notes. 

We'll proceed one topic at a time so every concept is covered in depth with code, diagrams, interview questions, and real-world examples.

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

# Chapter 2: AEM Installation & Project Setup

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
# Chapter 3: AEM Consoles

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
# Chapter 4: AEM Project Structure

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
# Chapter 5: AEM Components

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
# Chapter 6: HTL (HTML Template Language)

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
# Chapter 7: Sling Models (Complete Guide)

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
Excellent. Now let's learn **`@Inject`**, one of the most commonly used Sling Model annotations. Although modern AEM development often prefers more specific annotations like `@ValueMapValue` or `@ChildResource`, you will still see `@Inject` in many projects and interviews. This topic is also part of your uploaded AEM notes. 

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

## Next Annotation: `@ValueMapValue` ⭐⭐⭐⭐⭐

This is one of the **most important Sling Model annotations**. We'll cover:

* What is a `ValueMap`?
* How JCR properties are stored.
* How `@ValueMapValue` reads data.
* Required vs optional values.
* Complete code examples.
* Nested property handling.
* Real-world project scenarios.
* Common pitfalls.
* Interview questions.

This annotation is used in almost every AEM component, so we'll study it in even greater detail.
Excellent! Now let's study **`@ValueMapValue`**, which is arguably the **most important Sling Model annotation**. You'll use it in almost every AEM component. This topic is also covered in your uploaded AEM notes. 

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

## Next Annotation: `@ChildResource` ⭐⭐⭐⭐⭐

This is another essential annotation used with **Multifields**, **Navigation**, **Menus**, and nested content structures.

We'll cover:

* What is a child resource?
* JCR node hierarchy
* Reading Multifields
* Injecting lists of child resources
* Nested Sling Models
* Complete working examples
* Real project scenarios (Navigation Menu, Accordion, Carousel)
* Best practices
* Interview questions

`@ChildResource` is one of the most frequently used annotations in enterprise AEM projects, especially when working with complex authorable components.
Excellent! Now we'll study **`@ChildResource`**, one of the **most important annotations** for handling **Multifields**, **Navigation Menus**, **Carousels**, **Accordions**, and other nested content structures in AEM. This topic is also covered in your uploaded notes. 

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

## Next Annotation: `@Self`

We'll cover:

* What `@Self` is and when to use it.
* Difference between `@Self` and `@SlingObject`.
* Injecting the current `Resource`.
* Injecting `SlingHttpServletRequest`.
* Real project examples.
* Best practices and interview questions.

After that, we'll continue with `@SlingObject`, `@OSGiService`, `@ScriptVariable`, `@RequestAttribute`, `@ResourcePath`, `@Via`, and the remaining Sling Model annotations in the same detailed manner.
Excellent! Now let's learn **`@Self`**, another very important Sling Models annotation. It is widely used in enterprise AEM projects, especially when you need direct access to the current adaptable object. This topic is also covered in your uploaded AEM notes. 

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

## Next Lesson: `@SlingObject` ⭐⭐⭐⭐⭐

In the next lesson, we'll cover:

* What `@SlingObject` is
* `ResourceResolver`
* `Resource`
* `SlingHttpServletRequest`
* `SlingHttpServletResponse`
* Accessing the JCR repository
* Reading other resources
* Query examples
* Real enterprise use cases
* Complete code examples
* Interview questions

`@SlingObject` is one of the most frequently used annotations in enterprise AEM projects because it provides access to the core Sling APIs needed for repository operations and request processing.
Excellent! Now let's learn **`@SlingObject`**, one of the **most powerful and frequently used Sling Model annotations**. In almost every real AEM project, you'll use it to access the current resource, request, or `ResourceResolver`. This topic is also covered in your uploaded AEM notes. 

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

## Next Lesson: `@OSGiService` ⭐⭐⭐⭐⭐

This is another major interview topic. We'll cover:

* What is an OSGi Service?
* How to create an OSGi Service
* `@Component`
* `@Reference`
* `@OSGiService`
* Injecting services into Sling Models
* Real-world examples (EmailService, ProductService, SearchService)
* Complete working code
* Service lifecycle
* Best practices
* Common mistakes
* Interview questions

This is one of the most important backend concepts in AEM and is used extensively in enterprise projects.
Excellent! Now we'll learn **`@OSGiService`**, one of the **most important backend annotations** in AEM. Almost every enterprise AEM application uses OSGi services for reusable business logic. This topic is also covered in your uploaded AEM notes. 

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

## Next Lesson: `@PostConstruct` ⭐⭐⭐⭐⭐

`@PostConstruct` is another **very important** annotation because it is executed automatically **after all injections are complete**.

We'll cover:

* What `@PostConstruct` is.
* Why it is needed.
* Lifecycle.
* Data initialization.
* Validation.
* Sorting and formatting data.
* Calling OSGi services.
* Performance considerations.
* Real enterprise examples.
* Common mistakes.
* Interview questions.

`@PostConstruct` is used in most production Sling Models, so understanding it well is essential for both interviews and real-world AEM development.
