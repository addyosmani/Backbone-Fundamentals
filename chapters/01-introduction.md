# Introduction

Frank Lloyd Wright once said "You can't make an architect. You can however open the doors and windows toward the light as you see it." In this book, I hope to shed some light on how to improve the structure of your web applications, opening doors to what will hopefully be more maintainable, readable applications in your future.

The goal of all architecture is to build something well; in our case, to craft code that is enduring and delights both ourselves and the developers who will maintain our code long after we are gone. We all want our architecture to be simple, yet beautiful.

While modern web development has evolved significantly with frameworks like React, Vue, and Angular becoming popular choices for new projects, understanding Backbone.js remains valuable as it teaches fundamental concepts about application architecture and state management that are still relevant today.

### What Is MVC in Modern Web Development?

The Model-View-Controller (MVC) pattern, while evolved in modern frameworks, remains an important architectural concept. Today's frameworks often implement variations of this pattern:

* Models manage application data and business logic
* Views handle the user interface and presentation
* Controllers (or similar concepts) manage user input and application flow

Modern frameworks have evolved these concepts:
- React uses a component-based architecture with state management
- Vue combines template-based views with reactive data models
- Angular implements a more traditional MVC-like pattern with additional features

Backbone.js implements its own interpretation of MVC, which we'll explore in detail.

### What is Backbone.js?

![](img/backbonejsorg.jpg)

Backbone.js (current version 1.5.0) is a lightweight JavaScript library that adds structure to client-side code. While newer frameworks may be more popular for new projects, Backbone.js offers several advantages:

* Minimal size (only 13kb minified)
* Simple, understandable source code
* Flexible architecture that plays well with other libraries
* Strong focus on data modeling and state management
* RESTful API integration
* Excellent documentation and mature ecosystem

Backbone.js is particularly valuable for:
* Understanding fundamental concepts of structured JavaScript applications
* Maintaining or upgrading legacy applications
* Building lightweight applications where minimal framework overhead is desired
* Learning about event-driven architecture and data binding

### Modern JavaScript Application Architecture

Today's web applications often follow these architectural principles:

1. Component-Based Architecture
   - Modular, reusable pieces of UI and logic
   - Clear separation of concerns
   - Encapsulated state management

2. State Management
   - Centralized state stores (like Redux, inspired by Backbone's concepts)
   - Unidirectional data flow
   - Predictable state updates

3. API Integration
   - RESTful or GraphQL APIs
   - Real-time updates with WebSocket
   - Asynchronous data handling with Promises/async-await

4. Build and Development Tools
   - Modern build systems (Webpack, Vite)
   - ES6+ JavaScript features
   - TypeScript for type safety

Backbone.js influenced many of these modern practices, particularly in areas of:
- Event-driven architecture
- Model-View separation
- RESTful API integration
- Client-side routing

### When to Use Backbone.js Today

While new projects might benefit from modern frameworks, Backbone.js remains relevant in several scenarios:

1. Legacy Application Maintenance
   - Understanding and maintaining existing Backbone.js applications
   - Gradually migrating to newer technologies

2. Lightweight Applications
   - When minimal framework overhead is desired
   - For embedded widgets or microsites

3. Learning Purposes
   - Understanding fundamental concepts of structured JavaScript applications
   - Learning about event-driven architecture

4. Integration with Other Libraries
   - As part of a larger application using multiple technologies
   - When flexibility in architecture is required

### Setting Expectations

This book will:
1. Teach fundamental concepts of structured JavaScript applications
2. Show how to build applications using Backbone.js
3. Demonstrate modern JavaScript practices within Backbone.js
4. Explain how concepts from Backbone.js influence modern frameworks

The chapters will cover:

<i>Chapter 2, Fundamentals</i>, explores MVC pattern history and modern implementations.

<i>Chapter 3, Backbone Basics</i>, covers core Backbone.js features with modern JavaScript syntax.

<i>Chapter 4, Exercise 1: Todos</i>, builds a Todo application using current best practices.

<i>Chapter 5, Exercise 2: Book Library</i>, creates a RESTful application with modern API integration.

<i>Chapter 6, Backbone Extensions</i>, explores useful extensions and modern alternatives.

<i>Chapter 7, Common Problems and Solutions</i>, addresses current development challenges.

<i>Chapter 8, Modular Development</i>, covers modern module systems and build tools.

<i>Chapter 9, Exercise 3: Modular Todo App</i>, rebuilds the Todo app using modern tooling.

<i>Chapter 10, Pagination</i>, implements modern data handling patterns.

<i>Chapter 11, Build Tools</i>, explores current build systems and deployment.

<i>Chapter 12, Mobile Applications</i>, covers responsive design and mobile considerations.

<i>Chapter 13-15, Testing</i>, covers modern testing practices with Jasmine, QUnit, and SinonJS.

<i>Chapter 16, Resources</i>, provides updated learning resources.

<i>Chapter 17, Conclusions</i>, reflects on Backbone.js in modern web development.

<i>Chapter 18, Appendix</i>, includes additional patterns and architectural considerations.
