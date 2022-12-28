node{
  def mavenHome = tool name: 'maven3'
  stage('1cloneCode'){
    git "https://github.com/hope4lifeu/maven-web-application"
  }
  stage('2Test&Build'){
    sh "${mavenHome}/bin/mvn clean package"
    //bat "${mavenHome}/bin/mvn clean package"
  }
  stage('3codeQuality'){
    sh "${mavenHome}/bin/mvn clean sonar:sonar"
  }
  stage('4uploadArtifacts'){
    sh "${mavenHome}/bin/mvn deploy"
  }
  stage('5deploy2UAT'){
    sh "echo 'deploy to UAT' "
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://172.31.85.147:8080/')], contextPath: null, onFailure: false, war: 'target/*war'
  }
  stage('6approvalGate'){
      "echo 'application ready for your review, kindly review and revert back' "
     timeout(time:5, unit:'DAYS'){
     input message: 'Application ready for deployment, please review and approve'
     }
     
  }
 stage('8emailNotification'){
    emailext body: '''Hi All,

Check Build status.

Landmark Technologies''', recipientProviders: [buildUser(), developers(), upstreamDevelopers(), brokenBuildSuspects(), brokenTestsSuspects(), contributor()], subject: 'build status', to: 'tesla-app@gmail.com'
  }
  stage('deploy2production'){
      sh "echo 'production deployment' "
     deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://172.31.85.147:8080/')], contextPath: null, war: 'target/*war' 
  }
}
