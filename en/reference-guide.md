Preface
=======

Software development requires many different skills. This is even more
true when you have to deal with a distributed corporate application for
which you have to get expertise on :

-   Database design and performance (schema design, data access
    optimisation, data integrity, ...)

-   Gui design and binding on domain model (views, flow, actions, ...)

-   N-tier architecture design for distributed applications (frontend
    deployment, bandwidth consumption, network round trips, ...)

-   System scalability and robustness (fail over, load-balancing, ...)

-   Software architecture and best practices (design patterns, security,
    manageability, logging, low coupling, separation of concerns, ...)

-   Up-to-date technology building blocks (stay with standards, leverage
    on existing components, easy switch between equivalent components,
    ...)

Whenever one of these skills is not efficiently addressed, the software
may simply never become available or may not meet the promised quality
or exploitability required standards. It surely leads to huge delays on
the schedule and bad ROI.

Big software vendors have tried to address this situation more or less
succesfully by providing end to end CASE tools, but there are well-known
drawbacks to this approach. Some of them are :

-   High license fees for development and generally for runtime

-   End-to-end proprietary solutions locking the software and thus the
    customer into the selected technology and tools

-   The resulting software is often completely opaque and rarely
    intergrates seamlessly in the overall information infrastructure

With these ideas in mind, the Jspresso application framework was
developed. To get an idea of what a software framework is and what it is
not, please, refer to the following
[link](http://en.wikipedia.org/wiki/Software_framework). The Jspresso
framework differs from most of the other frameworks since it addresses
the complete software architecture (see the [Jspresso modules
diagram](#Jspresso-modules)) including all the key success factors
formerly described; but instead of "reinventing the wheel", Jspresso
strongly relies on production-proof open source libraries and
components. To get a complete list of the used libraries, please refer
to the Appendices.

Each of these libraries is distributed using a business-friendly licence
([LGPL](http://www.opensource.org/licenses/lgpl-license.php),
[BSD](http://www.opensource.org/licenses/bsd-license.php),
[Apache](http://www.opensource.org/licenses/apachepl.php), ...) that
enables its inclusion in closed-source software under copyright notice
conditions. Jspresso assembles them all together, in a loosely coupled
architecture so that the resulting software is not locked in any of
them. As an example, you don't have to choose whether you want to deploy
your application as a Java swing application through Java Web Start, as
an Adobe Flex application using the flash plugin or as an Ajax
application without any plug-in or all simultaneously ! Jspresso will
take care of it at runtime.

The whole objective of Jspresso is to shorten the gap (and thus avoid
the "tunnel" effect) between the business requirement analysis, the
detailed specifications, the design and the software available and
running. The development process becomes extremely agile since the
prototype progressively becomes the final application through very short
iterations.

To achieve this goal, the main paradigm of Jspresso is "whenever
describing is enough, do not code". Take a simple frontend example : you
want to provide the end user with a table listing a set of articles. Of
course, this table view has to be editable, sortable and present the
different columns based on their types (an image, the remaining stock
quantity, the date when this article was made available in the system,
and so on). Everyone is able to describe this view precisely and
everyone is able to understand what has been described. There should not
be a need for writing a single line of code (swing, flex, html, jsp,
javascript, ...) whenever this description has been captured by the
framework. This is exactly what Jspresso does by taking care of the
implementation once you have expressed the requirements. And there is no
complex code generation. Everything is just handled at runtime.

Here are some of the key features of the Jspresso framework :

**General design**

-   Develop by assembling built-in java beans descriptors through
    dependency injection. Descriptors can also be dynamically composed
    in plain java code if needed.

-   Desktop ergonomics oriented. Jspresso is not another web framework
    so just forget about page flows.

-   I18N and security (authentication and authorizations) as first
    citizens.

**Domain model**

-   Rich domain model paradigm (as opposed to thin or even anorexic
    domain models). Entities are responsible of their integrity, offer
    services and handle their relationships to others.

-   Model descriptors allow for the implementation of arbitrarily
    complex domain models :

    -   1-N, N-1, N-N, 1-1 unidirectional and bidirectional
        relationships

    -   association and composition semantics

    -   list and set collection semantics

    -   entities, inlined components and service interfaces

    -   entities inheritance

    -   more than 15 property types handled through all layers (string,
        integer, enumeration, date, duration, color, percentage, binary,
        ...)

-   Services offered by entities (and components) are objects themselves
    that are assembled in the entity (or component) through dependency
    injection. This allows for easy mock-up, logging and tracing, KPI
    implementation, inheritance between services, ... You can get all
    the advantages of AOP without its drawbacks.

-   Model descriptors offer fine-grained model description (rich
    validation constraints on properties). This is one of the most
    important feature of Jspresso since this rich semantic is then
    leveraged in all other layers without the need for repeating things.
    For instance, once you have constrained a property with a regular
    expression, views presenting this property will automagically
    enforce this constraint by allowing only matching values to be
    entered. Describe finely your domain model and building a complete
    application over it will then be an effortless process.

-   Jspresso entities (and components) support computed properties. Once
    defined, they are just usable as any primary property in the other
    layers.

-   Jspresso entities (and components) support life-cycle interceptors
    (on-create, on-persist, on-update, on-delete, on-load). Life-cycle
    interceptors are objects that are assembled in entities and
    dynamically triggered by the framework when needed.

-   Jspresso entities (and components) support property modifiers
    interceptors (before, intercept, after). Property modifiers
    interceptors are objects that are assembled in entities and
    dynamically triggered by the framework when needed.

-   Jspresso handles transparently the persistence of the domain model
    in the backend store. Everything needed to achieve this is inferred
    form the model description. Atomic backend synchronization is also
    completely handled by the framework and allows delayed updates of
    in-memory changes.

**Views**

-   Technology neutral view description. Following the assembling
    principle, views are generated at runtime through built-in factories
    depending on the chosen deployment strategy. Developing views is
    achieved by composing technology agnostic java beans view
    descriptors; this means absolutely no Swing, Flex, javascript, HTML
    or whatever specific GUI coding. Jspresso offers an extensive range
    of ready-to-use, highly configurable, view descriptors including :

    -   tree view

    -   table view

    -   list view

    -   form (component) view leveraging all supported property types
        with calendar component, filtered fields, list of values for
        relationships, ...

    -   single property view

    -   image view

    -   composite (container) views :

        -   border (north, south, east, west, center) composite view

        -   card composite view

        -   split composite view

        -   tab composite view

        -   grid composite views : evenly distributed size grids and
            constrained distributed size grids

-   Jspresso is open for extensions. You can easily implement your own
    view descriptors and extend the built-in view factories so that they
    are ready to handle them.

-   View descriptors are highly configurable but offer sensible default
    values; you can assemble rich views in minutes. General
    customizations include fonts, colors and border. Of course, each
    view descriptor allows for specialized customization; some examples
    of such customizations are :

    -   number of columns and list of displayed properties in form views

    -   split orientation in split views

    -   columns in table views

    -   many, many others...

-   Jspresso views are natively internationalized. Special care has been
    taken to nicely handle common I18N problems such as translation
    lengths differences by exclusively using layouts behind the scene;
    this means no absolute positioning of components and thus GUI resize
    friendly behaviour.

-   Jspresso avoids description repetition. Views are automatically
    configured based on their underlying model. For instance, fields (or
    table columns) preferred length are computed based on the maximum
    length constraint of the underlying model property.

**High-level application components**

-   Jspresso offers a rich set of ready-to-use high level application
    components that are ready to be assembled in application modules.
    For instance, Jspresso offers a highly configurable built-in module
    for CRUD operations on an entity family.

**Binding**

-   Jspresso transparently implements a true bidirectional MVC
    (Model-View-Controller). Views are always in sync with their
    session, in-memory, server-side model. This kind of design is a real
    challenge for distributed applications since it implies a lot of
    effort in terms of client-server communication efficiency and model
    integrity (Jspresso heavily uses the Unit-of-Work architectural
    pattern to guarantee the coherence of the backend transactional
    updates and of the in-memory model state).

-   Binding views and model doesn't require any special effort from the
    developer. It is just implicit when you describe your views. Binding
    is based on the JavaBeans' property semantics (property accessors).

**Actions**

-   Jspresso offers a rich and extensible set of built-in actions.
    Actions are implemented following a comprehensive action framework.
    There are more than 50 different built-in actions ready to be
    customized and assembled in Jspresso applications. Some example of
    such actions are :

    -   save action that transactionally updates the backend store

    -   copy, cut, paste actions that manage an entity oriented
        clipboard

    -   create and add, remove from, duplicate and add actions to handle
        "master-detail" like GUIs

    -   query action that implements "query by example" to retrieve
        entities from the backend store

    -   wizard action that chain views and populate an arbitrary context

    -   many, many others...

-   Jspresso actions are naturally split in 2 main categories :

    -   front-end actions that handle user interactions with the
        application. They offer customizable (and internationalized)
        tool tips, icons, keyboard shortcuts, ...

    -   back-end actions that are faceless and thus GUI independent.
        They are related to domain model operations.

-   Front-end actions are assembled in views so that users can trigger
    them. They are composed in a tool bar attached to the view but can
    also be triggered using a contextual pop-up menu.

-   Jspresso actions can be chained together so that you can implement
    complex application workflows by composing basic actions.

-   Jspresso actions are objects. This means that you can easily
    implement object-oriented hierarchies of actions, capitalize
    standard action sets that are reusable across your company
    applications, implement common behaviour for tracing, performance
    monitoring of services and so on.

**Security**

-   Security is everywhere in Jspresso but you won't notice it unless
    you actually need it.

-   Authentication is based on JAAS. Jspresso provides standard login
    modules that are fully JAAS compliant.

-   Authorizations are not handled by JAAS. This choice is deliberate
    since we believe that JAAS authorizations (and all the authorization
    frameworks we heard about) are too much code related, quite
    difficult to implement and lack some higher level concepts (like
    "make this field read-only for non-admin profiles"). So we
    implemented a simple yet complete and powerful authorization
    infrastructure :

    -   based on roles that are hierarchically organized and populated
        by JAAS authentication

    -   declarative so that you just have to configure the descriptors
        with a list of authorized roles (using their names). Whenever
        this list is missing means that there is no restriction on the
        underlying component.

    -   applicable in all layers (model, view, actions).

-   Each and every part of a Jspresso application is securable with
    authorization rules. Authorizations are propagated across layers so
    that if you declare a restriction in the domain model layer it is
    automatically propagated in the related views. But of course you can
    declare the restriction in the view (or part of the view) itself.
    Securable Jspresso components include :

    -   entity (or component) families

    -   single entity (or component) properties

    -   actions

    -   views (and view parts)

**I18N**

-   Jspresso has been developed to address the widest range of business.
    That is why it has been built with I18N in mind since the very
    beginning. But again, Jspresso makes internationalization easy.

-   I18N is not tied to the client desktop locale but to the user
    preferred language.

-   I18N applies to label translation and various formats (date,
    decimal, ...)

-   I18N traverses all layers with easy to apply conventions. For
    instance, whenever a form field is presented to the user, the
    framework will automatically look for a translation of the
    underlying property name. This means that once you've translated
    your entities and properties names, all your application is
    potentially internationalized. You can of course override this
    standard behaviour if you need to translate the same property
    differently in different views.

**Deployment architecture**

-   Seamless multi-channel deployment of the front-end :

    -   Swing

    -   Flex (Flash)

    -   qooxdoo (Ajax)

-   No need for a full-fledged application server unless you really need
    it. Jspresso embraced the Spring framework philosophy to keep the
    required software infrastructure as light as possible. The minimum
    requirement is a 2.5 servlet container (even not needed for a 2-tier
    swing deployment) and an Hibernate supported database.

This manual is organized around developing a sample application which is
targeted at human resources management. We will cover the complete
development process while presenting as much as possible of the Jspresso
framework. We believe that this approach will be more efficient than a
raw description of the framework features since it will show you not
only what to use but also how to use it efficiently.

The second half of the manual is Jspresso beans full reference.

So let's begin.

