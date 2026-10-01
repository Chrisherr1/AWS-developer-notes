**High-Availability vs Fault-Tolerance vs Disaster Recovery**
---
    Most people mix these up.

**High Availability**
---

    - Aims to entire a agreed level of operational preformeance, usually uptime, for a higher than normal period.

    -HA is NOT aiming to stop FAILURE, and it definetly doesn't mean customers WONT experience outages.

    A HA is one designed to be online and providing services as often as possible. It designed so that the components can be replaced as quickly as possible.

    Often using automation to bring systems back into service.

    HA is NOT ABOUT user experience.
        -If a component fails and it gets replaced and disrupts service for a few secs thats okay, its still HA.

    It's only about maximizing online time, thats it.

    Often represented by 99.9%,99.99%,99.9999%

    May require redundant infrastructure.

Key idea : It's only really about minimizing outages, not user experience.

**Fault Tolerance**
---

    - is the property that enables a system to continue operating properly in the event of the failure of some(one or more faults within) of its components.

    - means if something fails, it should be able to continue operating properly even while those faults are present and are 
    being fixed.

    - Should be able to work, with faults without effecting customers.

    - MORE EXPENSIVE,MORE COMPLEX to implement

    - First need to minimize outages, which is the same as HA, but
    also need to design the system to tolerate failure.
    - Which means levels of redundancy and system components, which can route any traffic around any failed components.

Key idea: It's a step up from high availability. It's about
    in case of failure the system DOES NOT GO DOWN at any point, and it can continue with the faulty components.
    Implemented usually by having duplicate components in the system not just on standby but actually in the system already.

*YOU NEED TO KNOW WHICH YOUR CUSTOMER NEEDS*


**Disaster Recovery**

    - A set of policies,tools, and procedures to enable the recovery or continuation of vital technology infrastructure and systems following a natural or human-induced disaster.

    Key Idea: Is more about what to do if a disaster actually knocks out a system.
    




