The term Plain Old [..] Objects originated from the desire to simplify types. Types with complicated conventions such as mandated base classes and heavy attribute decoration. Complicated types with many concerns that couple infrastructure to behaviour represent ill-factored code. Conflicting with established software design advice like high cohesion and low coupling. 

In summary favour the explicit nature of poco types over implicit, magic behaviour. Granted from inheriting or decorating with framework or library classes.  Please. Just because you can, doesn't mean you should. No surprises. Keep it simple. The recognition and adoption of the term and concept by the industry led to the dial of complexity turning down. 

DTOs are a kind of POCO. Their purpose is to transfer data across boundaries in distributed systems. Common DTOs purposes are Messages. For queues like NServiceBus, EasyMQ, MassTransit or ViewModels for presentation patterns. The common denominator is that they have _no behaviour_ they are only for data (transfer). 

Idiomatic object-orientation favours data stored in objects with behaviour (business logic). Manipulating data in a fashion intuitive to the problem the software is solving. A common misconception is that objects must contain data _or_ behaviour. Consider a type that contains only data and no behaviour anaemic. 

Anaemic objects are an anti-pattern. They promote high coupling because data and behaviour are separate, but need coupling. They are not cohesive because they are not intuitive. One does not expect to find the behaviour for an entity extra to the entity. Discourage encapsulation. Enforcing invariants is simpler if the behaviour can manipulate the data without exposing it. Reducing side effects and bugs. A projection of a snapshot of data is applicable for presentation. 

POCOs encourage the adoption of simple and uncomplicated software. An anaemic type is the antithesis of a POCO. It encourages high coupling and low cohesion.