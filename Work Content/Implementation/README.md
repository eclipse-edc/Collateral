# Implementation Viewpoint

The implmentation of the usage control concepts and their enforcements happens in the EDC in the form of the Policy Engine and its instantiations as well as in connected systems through accessible PEPs.


## The Policy Engine

Each implementation of an EDC usage enforcement engine must implement the `PolicyEngine` interface from the core Service Provider Interface (spi/core-spi) module. The `PolicyEngine` ensures that the basic funtions are provided:
- tbc.