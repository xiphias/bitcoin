Integration testing for bitcoin
================================

Tests that simulate multiple bitcoin users and can verify that the whole network of bitcoin clients work together
to achieve the goals of Bitcoin. Also maybe [System testing](http://en.wikipedia.org/wiki/System_testing)
would be a better name for the tests, but I'm not sure.

Goals
---------
- Make the bitcoin code easier to refactor while increasing the guarantee
 that it doesn't break the overall behaviour of the client.
- Make it easier to have multiple experimental coins (for example LightCoin or PPCoin) in the codebase, while guaranteeing that the original BitCoin protocol doesn't break
- Make it easy to test attack scenarios (like DOS,
 releasing an incompatible BitCoin client), monitoring
- Have tests without (or at least minimal number of) unreadable constants and unreadable fake data to make them easier to verify.

Proposed implementation
------------------------------------
The first implementation should use the JSON-RPC interface and build up as much verification
of BitCoin network as possible. It should be in C++, which makes it easier to move to the second implementation.
The JSON-RPC calls should be hidden by a C++ interface.

The second implementation should use the same interface that was used for JSON-RPC,
but using the BitCoin code directly (while not breaking the JSON-RPC tests).
For this the BitCoin client has to be refactored as a library,
getting rid of all global variables (and having them in a data structure),
so that multiple BitCoin clients can be run in the same process.

The improvement of the second implementation should have dependency injection
for the time and for finding/verifying a mined block,
so that the tests don't need to use real CPU power for mining,
and they can run faster and test more complex scenarios.






