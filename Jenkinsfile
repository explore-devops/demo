node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn sonar:sonar -Dsonar.projectKey=${{ github.event.repository.name }} -Dsonar.pullrequest.key=${{ github.event.number }} -Dsonar.pullrequest.branch=${{ github.event.pull_request.head.ref }} -Dsonar.pullrequest.base=main -Dsonar.scm.revision=${{ github.event.pull_request.head.sha }}"
    }
  }
}
