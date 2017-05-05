# Logging Guidelines

Most languages and runtime environments provide facilities for recording log
messages at runtime. The following are some language-neutral guidelines for
performing logging within our applications.

###### Use standard logging facilities

Applications **must** use standard logging facilities available for their
language or runtime environment. These facilities **should**, to the extent
possible, support the following features:

- Output at different levels/priorities (along w/ runtime configuration of such)
- Multiple output targets (i.e. console, file, email, etc.)
- Custom output formats
- [Diagnostic contexts](https://logback.qos.ch/manual/mdc.html)

If logging facilities are an "add-on", then a common, mature, and well-supported
library **must** be used. Add-ons **should** also be used where the built-in
facilities are recognized to be cumbersome, rudimentary, or otherwise inferior
to 3rd party solutions (for instance, JDK's `java.util.logging`). See each
language's standards for specific recommendations.

Bare "print" statements to standard out/err **must not** be used. Even though
setting up a logging framework and configuration might take a little extra time,
the benefits in the long run outweigh the small short-term costs.

_Rationale:_ Logging frameworks are superior to simple "print" statements.
First, the amount of logging output can be controlled via configuration &mdash;
sometimes without even restarting the application &mdash; rather than with code
changes. Second, the output can be better controlled to be both available and
readable to interested parties and automated tools.

###### Don't be shy about logging...

Applications **should** log their behavior and state frequently. A reader of the
logs should be able to follow what the application is doing. The amount of
detail that is contained in the logs may vary, depending on the configured
level. However, the "story" should be clear regardless of the level.

_Rationale:_ Logging statements can be very useful in troubleshooting, both
during development and in production. They also can take the place of code
comments in some cases.

###### ...But don't over-log

Applications **must not** log more detail than is necessary to create the
narrative. For instance, a developer should not use a logging statement before
and after each line of application code, or to "dump" the state of variables
(while such a technique can be useful for debugging, it should be used as a last
resort, and any excessive logging statements created must be removed before
committing to the source repository).

_Rationale:_ If an application generates too much logging output, then it
becomes almost meaningless. It's so difficult to wade through the log to find
the relevant information, that the log loses its value (needle in a haystack).

###### Use appropriate levels for log statements

Applications **must** use appropriate logging levels for each log statement. The
correct level of each statement will depend on the context and the importance or
severity of the information in the statement. Use common sense, and consider the
way that a log configured for any given level will look.

_Example:_ As an example, imagine a web application that wants to log requests
to `GET /customer/{id}`. The following are some possible logging statements, and a
sensible level for each of them:

```
[TRACE] Headers {'Authorization':'XYZ', 'X-Blah':'Blah blah blah',...}
[INFO ] Received GET request for customer 123
[WARN ] Unrecognized header: X-Blah
[ERROR] User 'ABC' is not authorized to view customer 123, IP address: 12.34.56.78
[FATAL] Cannot connect to database
```

The first statement is purely debugging information, and will only be relevant
to a small audience, probably during development or testing. The second & third
might be relevant in production, depending on the audience of the log. The last
2 are probably going to be something that _everyone_ needs to see. The
difference between them is that the first is not under the control of the
application, and could be fixable by the client, whereas the second indicates a
problem with the application itself that will need intervention to correct.

_This is a close cousin of the previous item, "... But don't over-log"._

_Rationale:_ Because logs are designed to be configurable, it's important that
the information logged to a destination matches the importance expected.

For instance, an operator might have configured an applcation to log all `FATAL`
and `ERROR` logs to an SNMP trap, which are then displayed in a dashboard. But
if the application also logs each web request at the `ERROR` level, the
operator's dashboard will quickly become inundated with mundane messages. The
operator will then either learn to ignore that application's error messages, or
will turn off `ERROR` logging altogether. Either way, actual application errors
are likely to be missed.

###### Be careful of logging sensitive information

Applications **must not** log very sensitive information such as passwords,
national identification numbers, etc. Some PII **might** be acceptable, such as
names and email addresses. However, care must be taken that logging, especially
in production, does not create a security hole. Logs should only be viewable by
authorized parties, and the information in those logs should not reveal
excessive data about the users of the application.

Some information can be logged if it is first scrubbed. For instance, a
trace-level logging statement that dumps the state of a customer should scrub
the sensitive data when it is logged:

```
[TRACE] Customer 123: { email = mr.ed@elmersglue.com, ssn = XXX-XX-XX32, firstName = Mister, lastName = Ed}
```

_Rationale:_ Logs are not always as secure as the other parts of the
application. Even if they are only readable by legitimate parties, such persons
or systems may not be authorized to view the personal information of the
application's users.
