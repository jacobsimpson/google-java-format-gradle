# google-format-gradle

Sample project integrating `google-java-format` into a gradle build script.

While configuring the project, I ran into an error that was difficult to diagnose.

```
You probably need to add a repository containing the '[com.google.googlejavaformat:google-java-format:1.8]' artifact in the 'build.gradle' of your root project.
```

## Configuration

How the project was configured:

```
$ gradle init

Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 2

Select implementation language:
  1: C++
  2: Groovy
  3: Java
  4: Kotlin
  5: Scala
  6: Swift
Enter selection (default: Java) [1..6] 3

Split functionality across multiple subprojects?:
  1: no - only one application project
  2: yes - application and library projects
Enter selection (default: no - only one application project) [1..2] 1

Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1

Select test framework:
  1: JUnit 4
  2: TestNG
  3: Spock
  4: JUnit Jupiter
Enter selection (default: JUnit 4) [1..4] 2

Project name (default: t): sample
Source package (default: sample):

> Task :init
Get more help with your project: https://docs.gradle.org/7.0/samples/sample_building_java_applications.html

BUILD SUCCESSFUL in 1m 17s
2 actionable tasks: 2 executed
```

Copy configuration from [spotless](https://github.com/diffplug/spotless/tree/main/plugin-gradle)
plugin documentation.

## Errors

```
$ gradle build

> Task :spotlessInternalRegisterDependencies FAILED
You probably need to add a repository containing the '[com.google.googlejavaformat:google-java-format:1.8]' artifact in the 'build.gradle' of your root project.
E.g.: 'buildscript { repositories { mavenCentral() }}'
org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration$ArtifactResolveException: Could not resolve all files for configuration ':spotless1972418318'.
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration.rethrowFailure(DefaultConfiguration.java:1420)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration.access$3600(DefaultConfiguration.java:150)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration$DefaultResolutionHost.rethrowFailure(DefaultConfiguration.java:2032)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration$ConfigurationFileCollection.visitContents(DefaultConfiguration.java:1392)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration.visitContents(DefaultConfiguration.java:499)
        at org.gradle.api.internal.file.AbstractFileCollection.getFiles(AbstractFileCollection.java:130)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration_Decorated.getFiles(Unknown Source)
        at org.gradle.api.internal.artifacts.configurations.DefaultConfiguration.resolve(DefaultConfiguration.java:489)
        at com.diffplug.gradle.spotless.GradleProvisioner.lambda$fromRootBuildscript$0(GradleProvisioner.java:73)
        at com.diffplug.gradle.spotless.GradleProvisioner$RootProvisioner.provisionWithTransitives(GradleProvisioner.java:55)
        at com.diffplug.spotless.JarState.provisionWithTransitives(JarState.java:68)
        at com.diffplug.spotless.JarState.from(JarState.java:57)
        at com.diffplug.spotless.JarState.from(JarState.java:52)
        at com.diffplug.spotless.java.GoogleJavaFormatStep$State.<init>(GoogleJavaFormatStep.java:123)
        at com.diffplug.spotless.java.GoogleJavaFormatStep.lambda$create$0(GoogleJavaFormatStep.java:75)
        at com.diffplug.spotless.FormatterStepImpl.calculateState(FormatterStepImpl.java:56)
        at com.diffplug.spotless.LazyForwardingEquality.state(LazyForwardingEquality.java:56)
        at com.diffplug.spotless.LazyForwardingEquality.writeObject(LazyForwardingEquality.java:68)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:64)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:564)
        at java.base/java.io.ObjectStreamClass.invokeWriteObject(ObjectStreamClass.java:1196)
        at java.base/java.io.ObjectOutputStream.writeSerialData(ObjectOutputStream.java:1523)
        at java.base/java.io.ObjectOutputStream.writeOrdinaryObject(ObjectOutputStream.java:1444)
        at java.base/java.io.ObjectOutputStream.writeObject0(ObjectOutputStream.java:1187)
        at java.base/java.io.ObjectOutputStream.writeObject(ObjectOutputStream.java:353)
        at org.gradle.internal.snapshot.impl.DefaultValueSnapshotter.serialize(DefaultValueSnapshotter.java:172)
        at org.gradle.internal.snapshot.impl.DefaultValueSnapshotter.processValue(DefaultValueSnapshotter.java:164)
        at org.gradle.internal.snapshot.impl.DefaultValueSnapshotter.processValue(DefaultValueSnapshotter.java:89)
        at org.gradle.internal.snapshot.impl.DefaultValueSnapshotter.snapshot(DefaultValueSnapshotter.java:54)
        at org.gradle.internal.execution.impl.DefaultInputFingerprinter$InputCollectingVisitor.visitInputProperty(DefaultInputFingerprinter.java:93)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter$TaskExecution.visitInputs(ExecuteActionsTaskExecuter.java:305)
        at org.gradle.internal.execution.impl.DefaultInputFingerprinter.fingerprintInputProperties(DefaultInputFingerprinter.java:50)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.captureExecutionState(CaptureStateBeforeExecutionStep.java:181)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.lambda$captureExecutionStateOp$1(CaptureStateBeforeExecutionStep.java:137)
        at org.gradle.internal.execution.steps.BuildOperationStep$1.call(BuildOperationStep.java:37)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:200)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:195)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:75)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:153)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:62)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.lambda$call$2(DefaultBuildOperationExecutor.java:76)
        at org.gradle.internal.operations.UnmanagedBuildOperationWrapper.callWithUnmanagedSupport(UnmanagedBuildOperationWrapper.java:54)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:76)
        at org.gradle.internal.execution.steps.BuildOperationStep.operation(BuildOperationStep.java:34)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.captureExecutionStateOp(CaptureStateBeforeExecutionStep.java:136)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.lambda$execute$0(CaptureStateBeforeExecutionStep.java:77)
        at java.base/java.util.Optional.map(Optional.java:258)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.execute(CaptureStateBeforeExecutionStep.java:77)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.execute(CaptureStateBeforeExecutionStep.java:49)
        at org.gradle.internal.execution.steps.ValidateStep.execute(ValidateStep.java:105)
        at org.gradle.internal.execution.steps.ValidateStep.execute(ValidateStep.java:50)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.lambda$execute$2(SkipEmptyWorkStep.java:86)
        at java.base/java.util.Optional.orElseGet(Optional.java:362)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.execute(SkipEmptyWorkStep.java:86)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.execute(SkipEmptyWorkStep.java:32)
        at org.gradle.internal.execution.steps.legacy.MarkSnapshottingInputsStartedStep.execute(MarkSnapshottingInputsStartedStep.java:38)
        at org.gradle.internal.execution.steps.LoadExecutionStateStep.execute(LoadExecutionStateStep.java:43)
        at org.gradle.internal.execution.steps.LoadExecutionStateStep.execute(LoadExecutionStateStep.java:31)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.lambda$execute$0(AssignWorkspaceStep.java:40)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter$TaskExecution$2.withWorkspace(ExecuteActionsTaskExecuter.java:283)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.execute(AssignWorkspaceStep.java:40)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.execute(AssignWorkspaceStep.java:30)
        at org.gradle.internal.execution.steps.IdentityCacheStep.execute(IdentityCacheStep.java:37)
        at org.gradle.internal.execution.steps.IdentityCacheStep.execute(IdentityCacheStep.java:27)
        at org.gradle.internal.execution.steps.IdentifyStep.execute(IdentifyStep.java:49)
        at org.gradle.internal.execution.steps.IdentifyStep.execute(IdentifyStep.java:35)
        at org.gradle.internal.execution.impl.DefaultExecutionEngine$1.execute(DefaultExecutionEngine.java:76)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.executeIfValid(ExecuteActionsTaskExecuter.java:184)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.execute(ExecuteActionsTaskExecuter.java:173)
        at org.gradle.api.internal.tasks.execution.CleanupStaleOutputsExecuter.execute(CleanupStaleOutputsExecuter.java:109)
        at org.gradle.api.internal.tasks.execution.FinalizePropertiesTaskExecuter.execute(FinalizePropertiesTaskExecuter.java:46)
        at org.gradle.api.internal.tasks.execution.ResolveTaskExecutionModeExecuter.execute(ResolveTaskExecutionModeExecuter.java:51)
        at org.gradle.api.internal.tasks.execution.SkipTaskWithNoActionsExecuter.execute(SkipTaskWithNoActionsExecuter.java:57)
        at org.gradle.api.internal.tasks.execution.SkipOnlyIfTaskExecuter.execute(SkipOnlyIfTaskExecuter.java:56)
        at org.gradle.api.internal.tasks.execution.CatchExceptionTaskExecuter.execute(CatchExceptionTaskExecuter.java:36)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.executeTask(EventFiringTaskExecuter.java:77)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:55)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:52)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:200)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:195)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:75)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:153)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:62)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.lambda$call$2(DefaultBuildOperationExecutor.java:76)
        at org.gradle.internal.operations.UnmanagedBuildOperationWrapper.callWithUnmanagedSupport(UnmanagedBuildOperationWrapper.java:54)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:76)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter.execute(EventFiringTaskExecuter.java:52)
        at org.gradle.execution.plan.LocalTaskNodeExecutor.execute(LocalTaskNodeExecutor.java:74)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:408)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:395)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:388)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:374)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.lambda$run$0(DefaultPlanExecutor.java:127)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.execute(DefaultPlanExecutor.java:191)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.executeNextNode(DefaultPlanExecutor.java:182)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.run(DefaultPlanExecutor.java:124)
        at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:64)
        at org.gradle.internal.concurrent.ManagedExecutorImpl$1.run(ManagedExecutorImpl.java:48)
        at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1130)
        at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:630)
        at org.gradle.internal.concurrent.ThreadFactoryImpl$ManagedThreadRunnable.run(ThreadFactoryImpl.java:56)
        at java.base/java.lang.Thread.run(Thread.java:832)
Caused by: org.gradle.internal.resolve.ModuleVersionNotFoundException: Cannot resolve external dependency com.google.googlejavaformat:google-java-format:1.8 because no repositories are defined.
Required by:
    project :
You probably need to add a repository containing the '[com.google.googlejavaformat:google-java-format:1.8]' artifact in the 'build.gradle' of your root project.
E.g.: 'buildscript { repositories { mavenCentral() }}'
org.gradle.api.InvalidUserDataException: Cannot add a configuration with name 'spotless1972418318' as a configuration with that name already exists.
        at org.gradle.api.internal.DefaultNamedDomainObjectCollection.assertCanAdd(DefaultNamedDomainObjectCollection.java:213)
        at org.gradle.api.internal.AbstractNamedDomainObjectContainer.create(AbstractNamedDomainObjectContainer.java:77)
        at org.gradle.api.internal.AbstractValidatingNamedDomainObjectContainer.create(AbstractValidatingNamedDomainObjectContainer.java:47)
        at org.gradle.api.internal.AbstractNamedDomainObjectContainer.create(AbstractNamedDomainObjectContainer.java:56)
        at com.diffplug.gradle.spotless.GradleProvisioner.lambda$fromRootBuildscript$0(GradleProvisioner.java:66)
        at com.diffplug.gradle.spotless.GradleProvisioner$RootProvisioner.provisionWithTransitives(GradleProvisioner.java:55)
        at com.diffplug.spotless.JarState.provisionWithTransitives(JarState.java:68)
        at com.diffplug.spotless.JarState.from(JarState.java:57)
        at com.diffplug.spotless.JarState.from(JarState.java:52)
        at com.diffplug.spotless.java.GoogleJavaFormatStep$State.<init>(GoogleJavaFormatStep.java:123)
        at com.diffplug.spotless.java.GoogleJavaFormatStep.lambda$create$0(GoogleJavaFormatStep.java:75)
        at com.diffplug.spotless.FormatterStepImpl.calculateState(FormatterStepImpl.java:56)
        at com.diffplug.spotless.LazyForwardingEquality.state(LazyForwardingEquality.java:56)
        at com.diffplug.spotless.LazyForwardingEquality.toBytes(LazyForwardingEquality.java:85)
        at com.diffplug.spotless.LazyForwardingEquality.hashCode(LazyForwardingEquality.java:102)
        at org.gradle.internal.execution.impl.DefaultInputFingerprinter$InputCollectingVisitor.visitInputProperty(DefaultInputFingerprinter.java:98)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter$TaskExecution.visitInputs(ExecuteActionsTaskExecuter.java:305)
        at org.gradle.internal.execution.impl.DefaultInputFingerprinter.fingerprintInputProperties(DefaultInputFingerprinter.java:50)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.captureExecutionState(CaptureStateBeforeExecutionStep.java:181)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.lambda$captureExecutionStateOp$1(CaptureStateBeforeExecutionStep.java:137)
        at org.gradle.internal.execution.steps.BuildOperationStep$1.call(BuildOperationStep.java:37)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:200)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:195)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:75)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:153)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:62)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.lambda$call$2(DefaultBuildOperationExecutor.java:76)
        at org.gradle.internal.operations.UnmanagedBuildOperationWrapper.callWithUnmanagedSupport(UnmanagedBuildOperationWrapper.java:54)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:76)
        at org.gradle.internal.execution.steps.BuildOperationStep.operation(BuildOperationStep.java:34)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.captureExecutionStateOp(CaptureStateBeforeExecutionStep.java:136)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.lambda$execute$0(CaptureStateBeforeExecutionStep.java:77)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.execute(CaptureStateBeforeExecutionStep.java:77)
        at org.gradle.internal.execution.steps.CaptureStateBeforeExecutionStep.execute(CaptureStateBeforeExecutionStep.java:49)
        at org.gradle.internal.execution.steps.ValidateStep.execute(ValidateStep.java:105)
        at org.gradle.internal.execution.steps.ValidateStep.execute(ValidateStep.java:50)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.lambda$execute$2(SkipEmptyWorkStep.java:86)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.execute(SkipEmptyWorkStep.java:86)
        at org.gradle.internal.execution.steps.SkipEmptyWorkStep.execute(SkipEmptyWorkStep.java:32)
        at org.gradle.internal.execution.steps.legacy.MarkSnapshottingInputsStartedStep.execute(MarkSnapshottingInputsStartedStep.java:38)
        at org.gradle.internal.execution.steps.LoadExecutionStateStep.execute(LoadExecutionStateStep.java:43)
        at org.gradle.internal.execution.steps.LoadExecutionStateStep.execute(LoadExecutionStateStep.java:31)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.lambda$execute$0(AssignWorkspaceStep.java:40)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter$TaskExecution$2.withWorkspace(ExecuteActionsTaskExecuter.java:283)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.execute(AssignWorkspaceStep.java:40)
        at org.gradle.internal.execution.steps.AssignWorkspaceStep.execute(AssignWorkspaceStep.java:30)
        at org.gradle.internal.execution.steps.IdentityCacheStep.execute(IdentityCacheStep.java:37)
        at org.gradle.internal.execution.steps.IdentityCacheStep.execute(IdentityCacheStep.java:27)
        at org.gradle.internal.execution.steps.IdentifyStep.execute(IdentifyStep.java:49)
        at org.gradle.internal.execution.steps.IdentifyStep.execute(IdentifyStep.java:35)
        at org.gradle.internal.execution.impl.DefaultExecutionEngine$1.execute(DefaultExecutionEngine.java:76)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.executeIfValid(ExecuteActionsTaskExecuter.java:184)
        at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.execute(ExecuteActionsTaskExecuter.java:173)
        at org.gradle.api.internal.tasks.execution.CleanupStaleOutputsExecuter.execute(CleanupStaleOutputsExecuter.java:109)
        at org.gradle.api.internal.tasks.execution.FinalizePropertiesTaskExecuter.execute(FinalizePropertiesTaskExecuter.java:46)
        at org.gradle.api.internal.tasks.execution.ResolveTaskExecutionModeExecuter.execute(ResolveTaskExecutionModeExecuter.java:51)
        at org.gradle.api.internal.tasks.execution.SkipTaskWithNoActionsExecuter.execute(SkipTaskWithNoActionsExecuter.java:57)
        at org.gradle.api.internal.tasks.execution.SkipOnlyIfTaskExecuter.execute(SkipOnlyIfTaskExecuter.java:56)
        at org.gradle.api.internal.tasks.execution.CatchExceptionTaskExecuter.execute(CatchExceptionTaskExecuter.java:36)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.executeTask(EventFiringTaskExecuter.java:77)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:55)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter$1.call(EventFiringTaskExecuter.java:52)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:200)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$CallableBuildOperationWorker.execute(DefaultBuildOperationRunner.java:195)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:75)
        at org.gradle.internal.operations.DefaultBuildOperationRunner$3.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:153)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.execute(DefaultBuildOperationRunner.java:68)
        at org.gradle.internal.operations.DefaultBuildOperationRunner.call(DefaultBuildOperationRunner.java:62)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.lambda$call$2(DefaultBuildOperationExecutor.java:76)
        at org.gradle.internal.operations.UnmanagedBuildOperationWrapper.callWithUnmanagedSupport(UnmanagedBuildOperationWrapper.java:54)
        at org.gradle.internal.operations.DefaultBuildOperationExecutor.call(DefaultBuildOperationExecutor.java:76)
        at org.gradle.api.internal.tasks.execution.EventFiringTaskExecuter.execute(EventFiringTaskExecuter.java:52)
        at org.gradle.execution.plan.LocalTaskNodeExecutor.execute(LocalTaskNodeExecutor.java:74)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:408)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$InvokeNodeExecutorsAction.execute(DefaultTaskExecutionGraph.java:395)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:388)
        at org.gradle.execution.taskgraph.DefaultTaskExecutionGraph$BuildOperationAwareExecutionAction.execute(DefaultTaskExecutionGraph.java:374)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.lambda$run$0(DefaultPlanExecutor.java:127)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.execute(DefaultPlanExecutor.java:191)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.executeNextNode(DefaultPlanExecutor.java:182)
        at org.gradle.execution.plan.DefaultPlanExecutor$ExecutorWorker.run(DefaultPlanExecutor.java:124)
        at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:64)
        at org.gradle.internal.concurrent.ManagedExecutorImpl$1.run(ManagedExecutorImpl.java:48)
        at org.gradle.internal.concurrent.ThreadFactoryImpl$ManagedThreadRunnable.run(ThreadFactoryImpl.java:56)

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':spotlessInternalRegisterDependencies'.
> Cannot add a configuration with name 'spotless1972418318' as a configuration with that name already exists.

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 562ms
6 actionable tasks: 1 executed, 5 up-to-date
```
