<!-- markdownlint-disable MD012 MD014 -->

# TeamCity

## Build project as code


![Chef Giphy](https://media.giphy.com/media/xznyPebL28X5u/giphy.gif)



## Infrastructure as Code

> Infrastructure as code is the approach to defining computing and network infrastructure through source code that can then be treated just like any software system

[Martin Fowler](https://martinfowler.com/bliki/InfrastructureAsCode.html)


- Can be kept in version control <!-- .element: class="fragment" -->
- Allows reproducible builds and testing <!-- .element: class="fragment" -->
- Allows auditing <!-- .element: class="fragment" -->


Benefits are 
- less stress when rolling out changes as well as 
- reduced mean time to recovery when disaster strikes.



### Build Project as Code


#### Lessons from the Travis model were as follows:

- Keep the build configuration alongside the code in the same VCS
- Pick an external form for the build configuration that is 
   - plain text and 
   - is human readable 
--> the changes could be tracked and diffed much like the changes to any other part of the code.
  
- Travis CI mainstreamed build as code using a YAML file.

TODO: Example yaml

### Build Project as Code

# TeamCity 


## Current situation
- Project is configured via UI

- Versioned settings

- Enabling/ disabling versioned settings is a specific permission
- Not attached to Project developers (plus) roles 

- If enabled TeamCity commits the initial project configuration to the VCS


# Sources



- https://www.gocd.org/2017/05/02/what-does-pipelines-as-code-really-mean/


- https://martinfowler.com/bliki/InfrastructureAsCode.html: Infrastructure as code is the approach to defining computing and network infrastructure through source code that can then be treated just like any software system. Such code can be kept in source control to allow auditability and ReproducibleBuilds, subject to testing practices, and the full discipline of ContinuousDelivery. It's an approach that's been used over the last decade to deal with growing CloudComputing platforms and will become the dominant way to handle computing infrastructure in the next.