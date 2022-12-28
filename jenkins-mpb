pipeline{
  agent any 
  tools {
    maven "maven3"
  }  
  stages {
    stage('1GetCode'){
      steps{
        sh "echo 'cloning the latest application version' "
        git "https://github.com/hope4lifeu/maven-web-application"
      }
    }
    /*
    stage('3Test+Build'){
      steps{
        sh "echo 'running JUnit-test-cases' "
        sh "echo 'testing must passed to create artifacts ' "
        sh "mvn clean package"
      }
    }
    stage('4CodeQuality'){
      steps{
        sh "echo 'Perfoming CodeQualityAnalysis' "
        sh "mvn sonar:sonar"
      }
    } 
    stage('5uploadNexus'){
      steps{
        sh "mvn deploy"
      }
    }
    stage('6deployment2appserver'){
        steps{
  deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://44.211.145.60:8080/')], contextPath: null, war: 'target/*war'
        }
        
    }
    }
    post{
        always{
    emailext body: 'kindly check this build and act accordingly', recipientProviders: [buildUser(), previous(), developers()], subject: 'HI all.'
  }
   success{
       emailext body: 'kindly check this build and act accordingly', recipientProviders: [buildUser(), previous(), developers()], subject: 'HI all.'
}
 failure{
     emailext body: 'kindly check this build and act accordingly', recipientProviders: [buildUser(), previous(), developers()], subject: 'HI all.'
 }
  }
  /*
}
}
