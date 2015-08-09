# Proposal: Implement core web services for notebook functionality

## Goals

* Implement *private* (at least for now) APIs
* Support isolating notebook biz logic from the main website, so it can focus on interactions.
* Expose it with a uniform interface
* Adhere to REST principals to enable clean evolution of workflows

## General concerns

### API Design

#### REST / Hypermedia

* Design using these principles and elements: https://github.com/estebistec/hypermedia-notes
* Research others and look for any natural matches of existing media types
  * Any learning/education formats?

#### Security

* Private auth for now, but OAuth-like for smooth future evolution
 * Bearer tokens
 * Signatures?
* Tokens will be associated to specific data owners (e.g., users)
 * Time based for further security?

### API Implementation

#### Uniform server patterns

Reduce code and establish patterns

* Resources
* Linking
* Conditional requests
* Health checks
* Profile and relation docs

#### Infrastructure

##### Instrumentation

* timing
* counting

##### Monitoring

* logging
* error handling
* alerting

#### Client / consumer support

We should have good client libraries that make the Django view code as thin as possible. This
includes such concerns as:

* loading resources and identifying their types (content-types, profiles, etc.)
* following related links without coupling to specific URLs
* taking actions (e.g., POSTing new data) described in the API
* caching representations of resources until they change
 * probably very locally, e.g., per web server process
* translating form inputs into API actions
* translating API errors into form error displays
 * this should be rare as forms themselves will implementation input validation
 * maybe what is needed here is a way to derive the validation parameters from the current
   resource.

## Concepts

### Overview

Each should have:

* Clear capabilities (data, workflows, ownership, security, etc.) to expose in services
* Proposed list of service resources
* Dependencies and relationships with other service concepts

### Index

1. Users
2. Notes
3. Tags
4. Snippets
5. Bookmarks
6. Scraps
7. Areas of Learning
