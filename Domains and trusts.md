
# Forest topology

> All child domains within a forest have a 2-way transitive trust to the root domain.

> Domain admins have control over their own domain resources!

>the domain admin can add global groups of other domains to the local groups of his domain, but not the other way around.

a domain admin of a child domain can only SEE GLOBAL GROUPS of the other domains in the forest.

The domain admin of the root forest is most likely also the 

Local groups are only visible inside the domain, 

1. **Domain Local Groups**:
    
    - Domain local groups are primarily used to assign permissions within a specific domain.
    - They can contain users, global groups, and universal groups from any domain within the same forest.
    - Domain local groups are commonly used to assign permissions to resources such as folders, files, and printers within a specific domain.
    - They provide flexibility in assigning permissions and can be nested within other groups.
2. **Global Groups**:
    
    - Global groups are used to organize users with similar roles or permissions across multiple domains.
    - They can contain user accounts from the same domain where the group is created.
    - Global groups are often used for assigning permissions across different domains within the same forest.
    - They are not typically used directly for assigning NTFS permissions, but rather for organizing users into logical groups.