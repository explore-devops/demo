node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn sonar:sonar " +
                            "-Dsonar.pullrequest.key=${env.CHANGE_ID} " +
                            "-Dsonar.pullrequest.branch=${env.CHANGE_BRANCH} " +
                            "-Dsonar.pullrequest.base=${env.CHANGE_TARGET}"
    }
	timeout(time: 1, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
  }
}
