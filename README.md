# GraalVM Sample Groovy Applicaiton

GraalVM does not build Groovy Applications:
```
Fatal error: com.oracle.graal.pointsto.util.AnalysisError$ParsingError: Error encountered while parsing java.lang.invoke.CallSite.setTargetNormal(java.lang.invoke.MethodHandle) 
```

This is 
[https://github.com/graalvm/native-build-tools/tree/master/samples/java-application](native-build-tools/samples/java-application) converted to Groovy.

Environment Setup:
```
sdk use java 22.2.r11-grl
```

```
% ./gradlew nativeCompile

> Task :nativeCompile
[native-image-plugin] Using executable path: ~/.sdkman/candidates/java/22.2.r11-grl/bin/native-image
========================================================================================================================
GraalVM Native Image: Generating 'java-application' (executable)...
========================================================================================================================
[1/7] Initializing...                                                                                    (6.2s @ 0.35GB)
 Version info: 'GraalVM 22.2.0 Java 11 CE'
 Java version info: '11.0.16+8-jvmci-22.2-b06'
 C compiler: cc (apple, arm64, 14.0.0)
 Garbage collector: Serial GC
 1 user-specific feature(s)
 - com.oracle.svm.polyglot.groovy.GroovyIndyInterfaceFeature
[2/7] Performing analysis...  []                                                                         (6.3s @ 1.28GB)
   4,979 (89.21%) of  5,581 classes reachable
   7,150 (58.90%) of 12,140 fields reachable
  25,906 (82.78%) of 31,296 methods reachable
      45 classes,     0 fields, and     0 methods registered for reflection

Fatal error: com.oracle.graal.pointsto.util.AnalysisError$ParsingError: Error encountered while parsing java.lang.invoke.CallSite.setTargetNormal(java.lang.invoke.MethodHandle) 
Parsing context:
   at java.lang.invoke.CallSite.setTargetNormal(CallSite.java:286)
   at java.lang.invoke.MutableCallSite.setTarget(MutableCallSite.java:156)
   at java.lang.invoke.SwitchPoint.invalidateAll(SwitchPoint.java:225)
   at org.codehaus.groovy.vmplugin.v8.IndyInterface.invalidateSwitchPoints(IndyInterface.java:186)
   at org.codehaus.groovy.vmplugin.v8.IndyInterface.lambda$static$0(IndyInterface.java:172)

        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.util.AnalysisError.parsingError(AnalysisError.java:152)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlow.createFlowsGraph(MethodTypeFlow.java:104)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlow.ensureFlowsGraphCreated(MethodTypeFlow.java:83)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlow.getOrCreateMethodFlowsGraph(MethodTypeFlow.java:65)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.typestate.DefaultVirtualInvokeTypeFlow.onObservedUpdate(DefaultVirtualInvokeTypeFlow.java:109)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.TypeFlow.update(TypeFlow.java:558)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.PointsToAnalysis$1.run(PointsToAnalysis.java:635)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.util.CompletionExecutor.executeCommand(CompletionExecutor.java:193)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.util.CompletionExecutor.lambda$executeService$0(CompletionExecutor.java:177)
        at java.base/java.util.concurrent.ForkJoinTask$RunnableExecuteAction.exec(ForkJoinTask.java:1426)
        at java.base/java.util.concurrent.ForkJoinTask.doExec(ForkJoinTask.java:290)
        at java.base/java.util.concurrent.ForkJoinPool$WorkQueue.topLevelExec(ForkJoinPool.java:1020)
        at java.base/java.util.concurrent.ForkJoinPool.scan(ForkJoinPool.java:1656)
        at java.base/java.util.concurrent.ForkJoinPool.runWorker(ForkJoinPool.java:1594)
        at java.base/java.util.concurrent.ForkJoinWorkerThread.run(ForkJoinWorkerThread.java:183)
Caused by: org.graalvm.compiler.java.BytecodeParser$BytecodeParserError: com.oracle.svm.hosted.substitute.DeletedElementException: Unsupported method java.lang.invoke.MethodHandleNatives.setCallSiteTargetNormal(CallSite, MethodHandle) is reachable
To diagnose the issue, you can add the option --report-unsupported-elements-at-runtime. The unsupported element is then reported at run time when it is accessed the first time.
        at parsing java.lang.invoke.CallSite.setTargetNormal(CallSite.java:286)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.throwParserError(BytecodeParser.java:2506)
        at org.graalvm.nativeimage.builder/com.oracle.svm.hosted.phases.SharedGraphBuilderPhase$SharedBytecodeParser.throwParserError(SharedGraphBuilderPhase.java:105)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.iterateBytecodesForBlock(BytecodeParser.java:3367)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.handleBytecodeBlock(BytecodeParser.java:3319)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.processBlock(BytecodeParser.java:3164)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.build(BytecodeParser.java:1138)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.buildRootMethod(BytecodeParser.java:1030)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.GraphBuilderPhase$Instance.run(GraphBuilderPhase.java:84)
        at org.graalvm.nativeimage.builder/com.oracle.svm.hosted.phases.SharedGraphBuilderPhase.run(SharedGraphBuilderPhase.java:79)
        at jdk.internal.vm.compiler/org.graalvm.compiler.phases.Phase.run(Phase.java:49)
        at jdk.internal.vm.compiler/org.graalvm.compiler.phases.BasePhase.apply(BasePhase.java:261)
        at jdk.internal.vm.compiler/org.graalvm.compiler.phases.Phase.apply(Phase.java:42)
        at jdk.internal.vm.compiler/org.graalvm.compiler.phases.Phase.apply(Phase.java:38)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.AnalysisParsedGraph.parseBytecode(AnalysisParsedGraph.java:135)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.meta.AnalysisMethod.ensureGraphParsed(AnalysisMethod.java:685)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlowBuilder.parse(MethodTypeFlowBuilder.java:168)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlowBuilder.apply(MethodTypeFlowBuilder.java:343)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.flow.MethodTypeFlow.createFlowsGraph(MethodTypeFlow.java:93)
        ... 13 more
Caused by: com.oracle.svm.hosted.substitute.DeletedElementException: Unsupported method java.lang.invoke.MethodHandleNatives.setCallSiteTargetNormal(CallSite, MethodHandle) is reachable
To diagnose the issue, you can add the option --report-unsupported-elements-at-runtime. The unsupported element is then reported at run time when it is accessed the first time.
        at org.graalvm.nativeimage.builder/com.oracle.svm.hosted.substitute.AnnotationSubstitutionProcessor.lookup(AnnotationSubstitutionProcessor.java:245)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.infrastructure.SubstitutionProcessor$ChainedSubstitutionProcessor.lookup(SubstitutionProcessor.java:140)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.infrastructure.SubstitutionProcessor$ChainedSubstitutionProcessor.lookup(SubstitutionProcessor.java:140)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.meta.AnalysisUniverse.lookupAllowUnresolved(AnalysisUniverse.java:426)
        at org.graalvm.nativeimage.pointsto/com.oracle.graal.pointsto.infrastructure.WrappedConstantPool.lookupMethod(WrappedConstantPool.java:170)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.lookupMethodInPool(BytecodeParser.java:4179)
        at org.graalvm.nativeimage.builder/com.oracle.svm.hosted.phases.SharedGraphBuilderPhase$SharedBytecodeParser.lookupMethodInPool(SharedGraphBuilderPhase.java:133)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.lookupMethod(BytecodeParser.java:4173)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.genInvokeStatic(BytecodeParser.java:1636)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.processBytecode(BytecodeParser.java:5224)
        at jdk.internal.vm.compiler/org.graalvm.compiler.java.BytecodeParser.iterateBytecodesForBlock(BytecodeParser.java:3359)
        ... 28 more
------------------------------------------------------------------------------------------------------------------------
                        0.8s (6.4% of total time) in 19 GCs | Peak RSS: 2.09GB | CPU load: 4.43
========================================================================================================================
Failed generating 'java-application' after 12.6s.
Error: Image build request failed with exit status 1

> Task :nativeCompile FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':nativeCompile'.
> Process 'command '~/.sdkman/candidates/java/22.2.r11-grl/bin/native-image'' finished with non-zero exit value 1

* Try:
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 14s
4 actionable tasks: 1 executed, 3 up-to-date
```
