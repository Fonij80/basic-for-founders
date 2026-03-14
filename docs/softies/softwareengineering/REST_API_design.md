# REST API Design Rules

- Representational State Transfer (REST): technical description of how the world Wide Web works,

- if web is an OS, REST is its architectural style

- REST API: type of web server that enables a client to access resources

- Tim Berners-Lee started a non-profit software project "WorldWideWeb" in 1990 to facilitate knowledge sharing in CERN. He had invented and implemetned:

- The Uniform Resource Identifier (URI), a syntax that assigns each web document a unique address

- The HyperText Transfer Protocol (HTTP), a message-based language that computers could use to communicate over the Internet.

- The HyperText Mark-up Language (HTML), to represent informative documents that contain links to related documents.

- The first web server. (http://info.cern.ch)

- The first web browser, which Berners-Lee also named “WorldWideWeb” and later renamed “Nexus” to avoid confusion with the Web itself.

- The first WYSIWYG HTML editor, which was built right into the browser. (What You See Is What You Get)

- First published web page on 1991

## Web Architecture

- In 1993, Roy Fielding, co-founder of Apache HTTP Server, became concerned by the Web's scalibility problem. His solution was to satisfy all below web constraints (referred to as the Web's architectural style):

1. Client-server: web is a client-server based system with the core of separation of concerns. Both client and server must conform to the Web's _uniform itnerface_.

- Web components: client, server, network-based intermediaries

2. Uniform interface: The interactions between the Web’s components depend on the uniformity of their interfaces. If any of the components stray from the established standards, then the Web’s communication system breaks down.

- uniform interface's constraints:
  1. Identification of resources: each distinct Web-based concept is known as a resource and may be addressed by a unique identifier

  2. Manipulation of resources through representations: the representation is a way to interact with the resource but it is not the resource itself. This conceptual distinction allows the resource to be represented in different ways and formats without ever changing its identifier.

  3. Self-descriptive messages: A resource’s desired state can be represented within a client’s request message. A resource’s current state may be represented within the response message that comes back from a server. The self-descriptive messages may include metadata to convey additional details regarding the resource state, the representation format and size, and the message itself.

  4. Hypermedia as the engine of application state (HATEOAS): A resource’s state representation includes links to related resources. The presence, or absence, of a link on a page is an important part of the resource’s current state.
  - Links: the threads that weave the Web together by allowing users to traverse information and applications in a meaningful and directed manner.

3. Layered system: enable network-based intermediaries such as proxies and gateways to be transparently deployed between a client and server using the Web’s uniform interface

- Network-based intermediaries are used for enforcement of security, response caching, and load balancing.

4. Cache: Caching response data can help to reduce client-perceived latency, increase the overall availability and reliability of an application, and control a web server’s load (reduce the overall web's cost)

5. Stateless: web server is not required to memorize the state of its client applications and the client must include all of the contextual info, a key contributor to the web's scalibility

6. Code-on-demand: enables web servers to temporarily transfer executable programs, such as scripts or plug-ins, to clients, the only optional constraint

- Web browser hosted technologies like Java applets, JavaScript, and Flash exemplify the code-on-demand constraint.

- Web API: the face of a web service, directly listening and responding to client requests.

- A Web API conforming to the REST architectural style is a REST API.

- Having a REST API makes a web service “RESTful.”

- A REST API consists of an assembly of interlinked resources. This set of resources is known as the REST API’s resource model.

- WRML: Web Resource Modeling Language to assist with the design and implementation of REST APIs.

## Identifier Design with URI

- REST APIs use Uniform Resource Identifiers (URIs) to address resources

- Tim Berners-Lee on URL: The only thing you can use an identifier for is to refer to an object. When you are not dereferencing, you should not look at the contents of the URI string to gain other information. (dereference sth: to use a piece of data to discover where another piece of data is held)

- URI Format Rules:
  URI = scheme "://" authority "/" path [ "?" query ] [ "#" fragment ]

1. Rule: Forward slash separator (/) must be used to indicate a hierarchical relationship

2. Rule: A trailing forward slash (/) should not be included in URIs. As the last character in the URL, / adds no semantic value.

3. Rule: Hyphens (-) should be used to improve the readability of URIs. Anywhere you would use a space or hyphen in English, you should use a hyphen in a URI.

4. Rule: Underscores (_) should not be used in URIs. Text viewer applications (browsers, editors, etc.) often underline URIs to provide a visual cue that they are clickable, so _ became hidden.

5. Rule: Lowercase letters should be preferred in URI paths. URI is case-sensitive except for the scheme and host component.

- same URIs:
  http://api.example.restapi.org/my-folder/my-doc
  HTTP://API.EXAMPLE.RESTAPI.ORG/my-folder/my-doc

6. Rule: File extensions should not be included in URIs. Instead, they should rely on the media type, as communicated through the Content-Type header, to determine how to process the body’s content.

- URI Authority Design Rules:

7. Rule: Consistent subdomain names should be used for your APIs. The full domain name of an API should add a sub-domain named api.

8. Rule: Consistent subdomain names should be used for your client developer portal. If an API provides a developer portal, by convention it should have a subdomain labeled developer.

### Resource Modeling

- The URI path conveys a REST API’s resource model, with each forward slash separated path segment corresponding to a unique resource within the model’s hierarchy. For example, this URI design:

http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet

- indicates that each of these URIs should also identify an addressable resource:

http://api.soccer.restapi.org/leagues/seattle/teams

http://api.soccer.restapi.org/leagues/seattle

http://api.soccer.restapi.org/leagues

http://api.soccer.restapi.org

- resource modeling == data modeling for a relational DB schema == classical modeling of object-oriented system

### Resource Archetypes

- When modeling an API’s resources, we can start with the some basic resource archetypes. A REST API is composed of four distinct resource archetypes:

1. Document: A document resource is a singular concept that is akin to an object instance or database record. A document’s state representation typically includes both fields with values and links to other related resources. With its fundamental field and link-based structure, the document type is the conceptual base archetype of the other resource archetypes. In other words, the three other resource archetypes can be viewed as specializations of the document archetype. Each URI below identifies a document resource:

http://api.soccer.restapi.org/leagues/seattle
http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet
http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/mike

- A document may have child resources that represent its specific subordinate concepts. With its ability to bring many different resource types together under a single parent, a document is a logical candidate for a REST API’s root resource, which is also known as the docroot. The example URI below identifies the docroot, which is the Soccer
  REST API’s advertised entry point:
  http://api.soccer.restapi.org

2. Collection: A collection resource is a server-managed directory of resources. Clients may propose new resources to be added to a collection. However, it is up to the collection to choose to create a new resource, or not. A collection resource chooses what it wants to contain and also decides the URIs of each contained resource.

- Each URI below identifies a collection resource:
  http://api.soccer.restapi.org/leagues
  http://api.soccer.restapi.org/leagues/seattle/teams
  http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players

3. Store: A store is a client-managed resource repository. A store resource lets an API client put resources in, get them back out, and decide when to delete them. On their own, stores do not create new resources; therefore a store never generates new URIs. Instead, each stored resource has a URI that was chosen by a client when it was initially put into the store. The example interaction below shows a user (with ID 1234) of a client program using a fictional Soccer REST API to insert a document resource named alonso in his or her store of favorites:
   PUT /users/1234/favorites/alonso

4. Controller: A controller resource models a procedural concept. Controller resources are like executable functions, with parameters and return values; inputs and outputs. Like a traditional web application’s use of HTML forms, a REST API relies on controller resources to perform application-specific actions that cannot be logically mapped to one of the standard methods (create, retrieve, update, and delete, also known as CRUD). Controller names typically appear as the last segment in a URI path, with no child resources to follow them in the hierarchy. The example below shows a controller resource that allows a client to resend an alert to a user:
   POST /alerts/245743/resend

### URI Path Design Rules

{collection-c}/{store-s}/{document-d}

1. Rule: A singular noun should be used for document names.

2. Rule: A plural noun should be used for collection names.

3. Rule: A plural noun should be used for store names.

4. Rule: A verb or verb phrase should be used for controller names.

5. Rule: Variable path segments may be substituted with identity-based values. A URI template includes variables that must be substituted before resolution. The URI template example below has three variables (leagueId, teamId, and playerId):
   http://api.soccer.restapi.org/leagues/{leagueId}/teams/{teamId}/players/{playerId}

- The substitution of a URI template’s variables may be done by a REST API or its clients. Each substitution may use a numeric or alphanumeric identifier, as shown in the examples below:
  http://api.soccer.restapi.org/leagues/seattle/teams/trebuchet/players/21
  http://api.soccer.restapi.org/games/3fd65a60-cb8b-11e0-9572-0800200c9a66

6. Rule: CRUD function names should not be used in URIs. HTTP request methods should be used to indicate which CRUD function is performed.

- Incorrect URIs:
  GET /deleteUser?id=1234
  GET /deleteUser/1234
  DELETE /deleteUser/1234
  POST /users/1234/delete

### URI Query Design

- URI’s optional query comes after the path and before the optional fragment:
  URI = scheme "://" authority "/" path [ "?" query ] [ "#" fragment ]

http://api.college.restapi.org/students/morgan/send-sms
http://api.college.restapi.org/students/morgan/send-sms?text=hello

- The URI of a controller resource that sends an sms message.
- The URI of a controller resource that sends an sms message with a text value of hello.

The query component of a URI contains a set of parameters to be interpreted as a
variation or derivative of the resource that is hierarchically identified by the path component. So, while these two resources are not the same, they are very closely related.
The query component can provide clients with additional interaction capabilities such as ad hoc searching and filtering. Therefore, unlike the other elements of a URI, the query part may be transparent to a REST API’s client.
The entirety of a resource’s URI should be treated opaquely by basic network-based intermediaries such as HTTP caches. Caches must not vary their behavior based on the presence or absence of a query in a given URI. Specifically, response messages must not be excluded from caches based solely upon the presence of a query in the requested URI.

1. Rule: The query component of a URI may be used to filter collections or stores

2. Rule: The query component of a URI should be used to paginate collection or store results

A REST API client should use the query component to paginate collection and store results with the pageSize and pageStartIndex parameters. The pageSize parameter specifies the maximum number of contained elements to return in the response. The pageStartIndex parameter specifies the zero-based index of the first element to return in the response. For example:
GET /users?pageSize=25&pageStartIndex=50
When the complexity of a client’s pagination (or filtering) requirements exceeds the simple formatting capabilities of the query part, consider designing a special controller resource that partners with a collection or store. For example, the following controller may accept more complex inputs via a request’s entity body instead of the URI’s query
part:
POST /users/search
This design allows for custom range types and special sort orders to be easily specified in the client request message body.
