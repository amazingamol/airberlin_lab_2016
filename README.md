# airberlin_lab_2016

Official Support Repo with Docs, FAQs and Issues around the Air Berlin Lab 2016 powered by XapiX.io

This site is for all kind of questions and feedback around the online hackathon to be found on devpost and all other aspects of the underlying innovation program.

## (http://airberlin.devpost.com/)

Prototype your value proposition towards airberlin's network of 30 million customers worldwide. 
Use airberlin's Lab to recombine data/services into customer-centric APP's. Design your APP's to meet real needs, solve painpoints and lower friction.

## (https://app.xapix.io/airberlin)

Use the for external developers usually locked up Air Berlin API (SOAP, RPC) the most comfortable way through XapiX.io (REST, Hypermedia) with preconfigured authentication. Just fill out a one step wizard and all available resources will be imported for you to start hacking! Use Swagger UI or our very own Web Console to right away peak into data and build awesome projects.

## XapiX.io

XapiX.io is a platform to build adapters to APIs or any other web interface. We normalize every kind of data source to a RESTful hypermedia format with all common features. For your convenience, we: manage authentication, minimize complexity resulting from heterogenousity, provide easy going mockup feature, provide direct feedback channel to provider API architects.

## XapiX.io 101

When signed in, find the educational mode switch in the upper right corner. Turning this one will show all available documentation info panels in place. Just try it!

Annotated videos for most common workflows are provided on our [YouTube channel](https://www.youtube.com/channel/UC1SPLZlF6Y_BkIkvi3kVwmw)

## XapiX.io terminology

(influenced by json:api and RESTful API terminology)

"Resources" within this document refers to XapiX’ main resources:
- "Web Interfaces"
- "Resource Class"
- "Mappings"
- "Microservices"

"XapiX Platform":
- "Resource Management"
  - GUI: XapiX Web GUI
  - API: Partner Company and Developer interface
- “Data Delivery API”
  - Runs all Client APIs

"Client API":
- bound to one "Project" and associated resources
- resulting REST interface according to "Resource Classes" configuration
- content and services according to Web Interfaces and Mappings

"Project":
- manage Users, resources, plan, "Client API" access + authentication
- when a User creates a "Project" it is an "owning Project"
- every created resource belongs to one "owning Project"
- only within their "owning Project" resources can be updated, deleted
- every "Project" by default is private, but can be made publicly importable
- if an "owning Project" is not publicly importable:
  - all resources have just one "consuming Project" that is the "owning Project" 
- else if an "owning Project" is publicly importable:
  - all resources have many "consuming Projects"
  - all "consuming Projects" may consume all of the "owning Project's" resources

“Web Interfaces”:
- "Web Data Source" (formerly Input Endpoint)
  - Examples:
    - 3rd party API endpoint
    - cloud data base
    - publicly accessible file on the web
    - private file uploaded to XapiX stored on S3
  - data types: JSON, XML, CSV, SOAP service, DB table or view, etc.
  - config fields to retrieve a collection of data records / a single data record
  - fetches a "data sample" when saved with valid configuration
  - "Web Data Target" - soon to come

"Resource Class" (formerly Output Endpoint)
- has 1 to 5 "Actions" out of:
  - "index" retrieves a (filtered, paginated) collection of "Resource Objects"
  - "show" retrieves a single "Resource Object" by it's ID
  - "create" takes a single "Resource Object"
  - "update" takes a single modified "Resource Object" to replace the one with the given ID
  - "delete" a single "Resource Object" by it's ID
- has 1..n attributes of plain data types (string, integer, boolean, nil)
- has 0..n "Resource Relationships"
  - "to_one" aka "belongs_to" says one "Resource Object" of this kind is related / belongs to one other "Resource Object"
  - "to_many" says one "Resource Object" of this kind is related to many other "Resource Objects". Or many other "Resource Objects" belong to one "Resource Object" of this kind.
- has 0..n "Sub Structures"
  - nested record collections in a "Web Data Source's" response
  - treated mostly like "Resource Relationships" only they are passed through without changes, so they are not of a "Resource Class" and violate "json:api"

"Mappings":
- "Source Mapping" (formerly Endpoint Mapping)
  - has 1 "Web Data Source" as mapping source. Keys of "data sample" are mappable items
  - has 1 "Resource Class" as mapping target. Attributes are mappable items
  - 0..n "data sample" keys may be mapped into one attribute. “Mapping formula” in a domain specific language (DSL) is attached to do data transformations
- "Target Mapping"
  - has 1 "Web Data Target" as mapping target. Parameters are mappable items
  - has 1 "Resource Class" as mapping target. Attributes are mappable items
  - “Mapping formula” on the ”Web Data Target”

"Microservice”:
- Code function for side effects executing logic remotely
- Bound to 0..n “Resource Class” “Actions”
- Examples:
  - Synchronize 3rd party API
  - Send an email
