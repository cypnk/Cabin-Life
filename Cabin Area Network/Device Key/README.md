# Device Key

A hardware authentication method which can be used to gain access to certain sensitive areas or equipment by providing onboard values as part of the [messaging protocol](https://github.com/cypnk/Cabin-Life/tree/master/Cabin%20Area%20Network#messaging).

The implementation of this aspect of the network will depend on the desired level of security. For simple authentication, the origin and last 8 values of the 32 bit message payload may suffice. For others, the function name, and destination may be added as part of the message payload.

This example will be a portable key which can be plugged into the running network at a suitably designed entry port for both indoor and outdoor use.

Work in progress...
