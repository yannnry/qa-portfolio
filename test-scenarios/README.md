# Test Scenarios

This folder contains high-level scenarios that map out what needs validation before test cases are written against them. A scenario states the condition to be tested; the test case states exactly how.

Examples may cover:

* Authentication and session handling
* Form validation and required-field behavior
* Data persistence across navigation or refresh
* Error handling and recovery paths
* Boundary conditions (input length, numeric ranges, empty states)
* Cross-feature interactions, such as a change in one module affecting another

Scenarios here are written the way I write them during an actual audit: broad enough to catch what matters, specific enough that two testers would derive the same test cases from them.
