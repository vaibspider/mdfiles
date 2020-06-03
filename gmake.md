# Compiling FreeBSD kernel - GNU make vs BSD make

Compiling FreeBSD kernel using GNU make gives following error:
```Makefile:111: *** missing separator.  Stop.```                                                                                                     
The error line no. corresponds to the \.if condition:
```
.if ${MAKE_VERSION} >= 20140620 && defined(.PARSEDIR)
.sinclude <bsd.compiler.mk>
.endif
```
The error above is misleading; it is not due to some popular whitespace issues with the Makefile. It's because GNU make couldn't parse the Makefile. FreeBSD kernel comes with a Makefile, which uses BSD make-specific features such as the **conditionals** above and flags like `-V`.
GNU make doesn't support the same conditionals as BSD make : [gmake conditionals syntax](https://www.gnu.org/software/make/manual/html_node/Conditional-Syntax.html) and it doesn't have a `-V` flag.

So the only way we can build FreeBSD kernel is to use BSD make.
