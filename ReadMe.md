Fail the Jenkins Build if SonarQube scan fails:
https://jenkins.io/blog/2017/04/18/continuousdelivery-devops-sonarqube/

However, I had encounter the below error after following the above link.

org.codehaus.groovy.control.MultipleCompilationErrorsException: startup failed:
WorkflowScript: 32: Expected a step @ line 32, column 25.
                           def qg = waitForQualityGate()
                           ^
WorkflowScript: 33: Expected a step @ line 33, column 25.
                           if (qg.status != 'OK') {
                           ^
2 errors

	at org.codehaus.groovy.control.ErrorCollector.failIfErrors(ErrorCollector.java:310)
	at org.codehaus.groovy.control.CompilationUnit.applyToPrimaryClassNodes(CompilationUnit.java:1085)
	at org.codehaus.groovy.control.CompilationUnit.doPhaseOperation(CompilationUnit.java:603)
	at org.codehaus.groovy.control.CompilationUnit.processPhaseOperations(CompilationUnit.java:581)
	at org.codehaus.groovy.control.CompilationUnit.compile(CompilationUnit.java:558)
	at groovy.lang.GroovyClassLoader.doParseClass(GroovyClassLoader.java:298)
	at groovy.lang.GroovyClassLoader.parseClass(GroovyClassLoader.java:268)
	at groovy.lang.GroovyShell.parseClass(GroovyShell.java:688)
	at groovy.lang.GroovyShell.parse(GroovyShell.java:700)
	at org.jenkinsci.plugins.workflow.cps.CpsGroovyShell.doParse(CpsGroovyShell.java:133)
	at org.jenkinsci.plugins.workflow.cps.CpsGroovyShell.reparse(CpsGroovyShell.java:127)
	at org.jenkinsci.plugins.workflow.cps.CpsFlowExecution.parseScript(CpsFlowExecution.java:557)
	at org.jenkinsci.plugins.workflow.cps.CpsFlowExecution.start(CpsFlowExecution.java:518)
	at org.jenkinsci.plugins.workflow.job.WorkflowRun.run(WorkflowRun.java:290)
	at hudson.model.ResourceController.execute(ResourceController.java:97)
	at hudson.model.Executor.run(Executor.java:421)


I had fixed the Jenkinsfile by following the solution given on the below page (i.e. by adding script block):

https://stackoverflow.com/questions/39832862/jenkins-cannot-define-variable-in-pipeline-stage