# How should a module be structured?

Each module needs to contain pom.xml and src folder. Main module (Kitodo) should have included dependencies to all other modules. They all are equal in hierarchy but the aim is to use Kitodo module as a core module.

Name of artifactId: kitodo-moduleFunction
Name of groupId: org.kitodo.moduleFunction

Name of all modules should start from big letter e.g. Kitodo → probably more appropriate name would be Core or something like that.

# What does maven specify?

Maven requires that every child module contains information about parent (parent is defined in pom.xml, which is placed on project level). Pom.xml on project level requires to have declared list of all child modules. It is advisable to avoid submodules in modules → keep only one level parent - child.

Modules which are equal to each other in hierarchy needs to have added dependencies to other modules (only used ones).

# How could an API look like?

They need to give easy access to functionalities provided by modules.
