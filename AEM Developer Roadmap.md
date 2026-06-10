---
title: AEM Developer Roadmap

---


# AEM Developer Roadmap (Complete)

## Phase 0: Prerequisites (Must Learn First)

Before touching AEM, become comfortable with:

### Java Fundamentals

Topics:

* Variables and Data Types
* Operators
* Conditional Statements
* Loops
* Arrays
* Methods
* Classes and Objects
* Inheritance
* Polymorphism
* Abstraction
* Encapsulation
* Exception Handling
* Collections Framework
* Generics
* Java 8 Features

  * Lambda Expressions
  * Streams API
  * Functional Interfaces
* Multithreading Basics
* File Handling
* Design Patterns

### Maven

Topics:

* Maven Architecture
* pom.xml
* Dependencies
* Plugins
* Build Lifecycle
* Multi-module Projects

### Git

Topics:

* Repository
* Clone
* Commit
* Push
* Pull
* Branching
* Merge
* Rebase
* Pull Requests
* Conflict Resolution

### Linux Basics

Topics:

* File System
* Permissions
* SSH
* Process Management
* Shell Commands

---

# Phase 1: Web Development Foundation

## HTML

Topics:

* HTML Structure
* Forms
* Tables
* Semantic Tags
* Accessibility

## CSS

Topics:

* Selectors
* Flexbox
* Grid
* Responsive Design
* Media Queries
* Animations

## JavaScript

Topics:

* Variables
* Functions
* Objects
* Arrays
* ES6+
* Promises
* Async/Await
* DOM Manipulation
* Events

## Frontend Framework Basics

Learn at least one:

* React
* Angular
* Vue

For modern AEM:

* React is highly recommended.

Topics:

* Components
* Props
* State
* Routing
* API Calls

---

# Phase 2: Backend Concepts Required for AEM

## Servlet Fundamentals

Topics:

* HTTP Protocol
* GET
* POST
* PUT
* DELETE
* Request Lifecycle
* Session Management
* Filters

## REST APIs

Topics:

* REST Architecture
* JSON
* API Design
* Authentication
* JWT
* OAuth

---

# Phase 3: Content Management System Basics

Understand:

## CMS Concepts

Topics:

* Content Authoring
* Templates
* Components
* Publishing
* Content Lifecycle
* Digital Assets

Understand differences between:

* WordPress
* Drupal
* AEM

---

# Phase 4: Core AEM Fundamentals

## AEM Architecture

Topics:

* What is AEM
* AEM Architecture
* Author Instance
* Publish Instance
* Dispatcher
* CDN
* Repository

Architecture Flow:

User → CDN → Dispatcher → Publish → Author

### Learn:

* AEM Sites
* AEM Assets
* AEM Forms
* AEM Headless
* AEM Cloud Service

---

# Phase 5: Apache Sling (Most Important)

AEM is built on Sling.

## Sling Fundamentals

Topics:

* Sling Architecture
* Resource Resolution
* Resource Mapping
* URL Decomposition
* Sling Request Processing

### Sling Resources

Topics:

* Resource
* ResourceResolver
* Adaptable
* ValueMap

### Sling Models

Topics:

* @Model
* @Inject
* @ValueMapValue
* @OSGiService
* @Self
* @Via

Practice:

* Create Sling Models
* Inject Properties
* Create Business Logic

---

# Phase 6: JCR (Java Content Repository)

AEM stores everything in JCR.

## JCR Basics

Topics:

* Repository
* Nodes
* Properties
* Paths

Example:

```text
/content
/content/site
/content/site/en
```

### Node Types

Topics:

* nt:unstructured
* cq:Page
* cq:PageContent

### JCR Queries

Topics:

* XPath
* SQL2
* Query Builder

Practice:

* Content Search
* Asset Search

---

# Phase 7: CRXDE Lite

Topics:

* Repository Navigation
* Node Creation
* Property Management
* Package Installation
* Code Inspection

Practice:

* Create Components
* Create Templates
* Create Content Structures

---

# Phase 8: OSGi Framework

Most interview questions come from here.

## OSGi Fundamentals

Topics:

* Bundle
* Service
* Component
* Configuration

### Annotations

Topics:

* @Component
* @Activate
* @Deactivate
* @Reference

### Configuration

Topics:

* OSGi Configurations
* Factory Configurations
* Run Modes

Practice:

* Create OSGi Service
* Consume OSGi Service
* Configure Services

---

# Phase 9: HTL (Sightly)

Frontend templating language.

## HTL Basics

Topics:

* Expressions
* Conditions
* Loops
* Templates

### HTL Objects

Topics:

* properties
* currentPage
* resource
* pageManager

### Advanced HTL

Topics:

* data-sly-use
* data-sly-test
* data-sly-repeat
* data-sly-list
* data-sly-resource
* data-sly-include

Practice:

* Build Components

---

# Phase 10: AEM Components

Most daily work happens here.

## Component Development

Topics:

* Component Structure
* Dialogs
* Edit Configurations
* Design Dialogs

### Granite UI

Topics:

* Text Field
* Path Field
* Checkbox
* Multifield
* Dropdown

Practice Components:

1. Title
2. Text
3. Image
4. Carousel
5. Hero Banner
6. Navigation
7. Footer
8. Accordion
9. Tabs

---

# Phase 11: Templates

## Editable Templates

Topics:

* Template Policies
* Structure Mode
* Initial Content

Practice:

* Landing Page Template
* Article Template
* Product Template

---

# Phase 12: Client Libraries

Topics:

* CSS Clientlibs
* JS Clientlibs
* Categories
* Dependencies
* Embedding

Practice:

* Component-specific CSS
* Global JS

---

# Phase 13: AEM Workflows

Topics:

* Workflow Models
* Workflow Launcher
* Custom Workflow

Practice:

* Approval Workflow
* Asset Workflow

---

# Phase 14: AEM DAM (Digital Asset Management)

Topics:

* Asset Upload
* Metadata
* Renditions
* Asset Processing

Practice:

* Image Renditions
* Asset Metadata Updates

---

# Phase 15: Dispatcher (Very Important)

AEM Performance depends on Dispatcher.

## Topics

* Dispatcher Architecture
* Cache Rules
* Filters
* Rewrite Rules
* Flush Agents

Practice:

* Configure Cache
* Invalidate Cache
* Security Filters

---

# Phase 16: Security

Topics:

* Authentication
* Authorization
* ACL
* Permissions
* Service Users

Practice:

* Secure Components
* Service User Mapping

---

# Phase 17: MSM (Multi Site Manager)

Topics:

* Blueprint
* Live Copy
* Rollout
* Synchronization

Practice:

* Multi-country Websites

---

# Phase 18: AEM Headless CMS

Growing demand area.

Topics:

* Content Fragments
* Experience Fragments
* GraphQL
* APIs

Practice:

* React + AEM Headless Project

---

# Phase 19: AEM Cloud Service

Current industry standard.

## Topics

* Cloud Manager
* CI/CD
* Pipeline
* Environment Management
* Cloud Deployment

Practice:

* Cloud Deployment
* Pipeline Configuration

---

# Phase 20: Testing

Topics:

* JUnit
* Mockito
* Sling Mocks
* AEM Mocks

Practice:

* Unit Testing
* Service Testing
* Component Testing

---

# Phase 21: DevOps for AEM

Topics:

* Jenkins
* GitHub Actions
* Docker
* Kubernetes Basics
* SonarQube

---

# Phase 22: Advanced AEM Development

Topics:

* Custom Sling Servlets
* Sling Filters
* Event Handlers
* Scheduler Jobs
* Replication API
* Package Manager API
* Custom Indexing
* Query Optimization

---

# Phase 23: Performance Optimization

Topics:

* Dispatcher Caching
* Query Optimization
* Indexing
* Lazy Loading
* CDN Optimization

---

# Phase 24: Real Projects

Build these projects:

### Beginner

* Personal Blog Website

### Intermediate

* Corporate Website

### Advanced

* Multi-country Enterprise Website

### Expert

* Headless Commerce Website
* News Portal
* Banking Portal

---

# Phase 25: Interview Preparation

Master these topics:

### Frequently Asked

* Sling vs OSGi
* Resource vs Node
* ResourceResolver vs Session
* HTL vs JSP
* Editable Templates
* Dispatcher
* MSM
* Workflow
* Service User
* Sling Models
* Content Fragment
* Experience Fragment
* AEM Cloud Service

---

# Recommended Learning Order (Exact Sequence)

1. Java
2. Maven
3. Git
4. HTML/CSS/JS
5. Servlet
6. REST API
7. CMS Concepts
8. AEM Architecture
9. Sling
10. JCR
11. CRXDE
12. OSGi
13. HTL
14. Components
15. Templates
16. Clientlibs
17. Workflows
18. DAM
19. Dispatcher
20. Security
21. MSM
22. Headless CMS
23. Cloud Service
24. Testing
25. DevOps
26. Advanced AEM
27. Performance
28. Real Projects
29. Interview Preparation
