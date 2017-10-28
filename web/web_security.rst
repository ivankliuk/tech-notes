Web Security
============

General
=======

A web session is a sequence of network HTTP request and response transactions associated to the same user.
HTTP is a stateless protocol where each request and response pair is independent of other web interactions. Therefore, in order to introduce the concept of a session, it is required to implement session management capabilities that link both the authentication and access control (or authorization) modules commonly available in web applications:
https://www.owasp.org/index.php/File:Session-Management-Diagram_Cheat-Sheet.png

The session ID or token binds the user authentication credentials (in the form of a user session) to the user HTTP traffic and the appropriate access controls enforced by the web application

In order to keep the authenticated state and track the users progress within the web application, applications provide users with a session identifier (session ID or token) that is assigned at session creation time, and is shared and exchanged by the user and the web application for the duration of the session (it is sent on every HTTP request). The session ID is a “name=value” pair.


Session ID Properties
=====================

*Session ID Name Fingerprinting*
The name used by the session ID should not be extremely descriptive nor offer unnecessary details about the purpose and meaning of the ID.
Therefore, the session ID name can disclose the technologies and programming languages used by the web application.
It is recommended to change the default session ID name of the web development framework to a generic name, such as “id”.

*Session ID Length*
The session ID must be long enough to prevent brute force attacks, where an attacker can go through the whole range of ID values and verify the existence of valid sessions.
The session ID length must be at least 128 bits (16 bytes).

*Session ID Entropy*
The session ID must be unpredictable (random enough) to prevent guessing attacks, where an attacker is able to guess or predict the ID of a valid session through statistical analysis techniques. For this purpose, a good PRNG (Pseudo Random Number Generator) must be used.
The session ID value must provide at least 64 bits of entropy (if a good PRNG is used, this value is estimated to be half the length of the session ID).

*Session ID Content (or Value)*
The session ID content (or value) must be meaningless to prevent information disclosure attacks, where an attacker is able to decode the contents of the ID and extract details of the user, the session, or the inner workings of the web application.

# Continue here: https://www.owasp.org/index.php/Session_Management_Cheat_Sheet

TODO
