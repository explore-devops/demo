node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'Default Maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn sonar:sonar " +
	                    "-Dsonar.branch.name=${env.BRANCH_NAME} " +  
                            "-Dsonar.pullrequest.key=${env.CHANGE_ID} " +
                            "-Dsonar.pullrequest.branch=${env.CHANGE_BRANCH} " +
                            "-Dsonar.pullrequest.base=${env.CHANGE_TARGET}" +
			    "-Dsonar.pullrequest.provider=GitHub " +
			    "-Dsonar.pullrequest.github.repository=explore-devops/demo"
    }
	timeout(time: 1, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
  }
}
