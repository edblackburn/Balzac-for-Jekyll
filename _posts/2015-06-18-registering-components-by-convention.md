---
layout: post-no-feature
title: "Registering components by convention"
category: articles
tags: [post, readability, test]
---
Experience has taught me that the benefits of using a container diminish if you have to maintain explicit configuration. It's is time consuming and encourages one to implement unintuitive structures. Granted implicit registration can appear magic, but if the conventions are universal and clear then the cost of adding new components and importantly maintaining old ones is lowered.

If the cost of using a container is high, why bother at all? Constructor dependency injection is so common place that poor mans dependency injection is not unusual and is often a sensible choice.

For example for simple container configuration I prefer to "bootstrap" my service and use common conventions. So common is the maxim convention over configuration it is in danger of becoming a cliche. So here's an example using Windsor.

My bootstrapper instanciates and disposes of the container instance, whilst installing all public installers with parameters constructors within the same assembly:

<script src="https://gist.github.com/blazey/b959af307923eebae028.js"></script>

Where possible I register my components by feature. This reduces the cost of maintenance because my features are less coupled than if I were sharing services. I omit cross cutting infrastructure services from feature installers. I group features by namespace because experience has taught me this is more intuitive for developers (particularly myself if I don't visit a code base often).

Here is an example of a feature installer for a services API: 

<script src="https://gist.github.com/blazey/ec6aa4dd49bb26efd68e.js"></script>

Nice and simple? The FeatureInstaller is called explicitly because it is not public and has a generic parameter. In this example we are instructing the container to install all types with [corresponding interfaces](https://github.com/castleproject/Windsor/blob/master/docs/registering-components-by-conventions.md#defaultinterfaces) and within the same namespace as IController. 

Here is the feature installer:

<script src="https://gist.github.com/blazey/74a8eaad16641417e34b.js"></script>

But what if I need to configure a type in a library, whose conventions do not match mine? Well Convention over configuration does not mean convention not configuration.

Here is a simple example whereby hangfire.io is configured alongside my conventionally configured types: 

<script src="https://gist.github.com/blazey/9153cfc81cce8f28f20a.js"></script>

In summary favour convention over configuration, structure your code to be intuitive so a developer can understand where to find things, without cognitive gymnastics. The upfront effort to factor your code around features is cheaper than the refactoring required if features are coupled. Your shopping basket should not be coupled to your product browsing. Exclude aspects and other cross cutting types and install them with their own conventions or explicitly if required.