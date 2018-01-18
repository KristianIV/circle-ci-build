# Circle CI Build image

This repository is for building of a Docker image which can be used to perform builds in Circle CI

It also adds google-cloud sdk so that it is possible to deploy built artefacts to google cloud

I had planned on migrating to an Alpine Linux base image
but this was not possible due to my tests requiring to use
grpc-based APIs

Below is an output of the google compatability check

```
OS details:
  os.detected.name: linux
  os.detected.arch: x86_64
  os.detected.classifier: linux-x86_64
  os.detected.release: alpine
  os.detected.release.version: 3.6.2
JVM details:
  Java version: 1.8.0_161
  Java specification version: 1.8
  JVM bit mode: 64
OpenSSL details:
  open ssl is available: false
  ALPN is supported: false
Checking compatibility...
  [PASS] This OS + architecture is supported.
  [PASS] 64-bit JVM is supported.
  [FAIL] Open SSL is NOT available
         Open SSL Unavailability cause:
java.lang.IllegalArgumentException: Failed to load any of the given libraries: [netty-tcnative-linux-x86_64, netty-tcnative-linux-x86_64-fedora, netty-tcnative]
	at io.netty.util.internal.NativeLibraryLoader.loadFirstAvailable(NativeLibraryLoader.java:178)
	at io.netty.handler.ssl.OpenSsl.loadTcNative(OpenSsl.java:403)
	at io.netty.handler.ssl.OpenSsl.<clinit>(OpenSsl.java:85)
	at com.google.cloud.compatchecker.GoogleCloudCompatChecker.check(GoogleCloudCompatChecker.java:58)
	at com.google.cloud.compatchecker.GoogleCloudCompatChecker.main(GoogleCloudCompatChecker.java:47)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.codehaus.mojo.exec.ExecJavaMojo$1.run(ExecJavaMojo.java:282)
	at java.lang.Thread.run(Thread.java:748)
  [FAIL] Open SSL ALPN is NOT supported
Result: FAIL
  Your environment is not supported by Forked Tomcat Native.
  See http://netty.io/wiki/forked-tomcat-native.html for details.
  This means that you won't be able to use grpc-based APIs, but
  http1-based APIs should still work.
```
