pipeline{
  agent any 
  tools {
    maven "maven3.8.6"
  }  
  stages {
    stage('1GetCode'){
      steps{
        sh "echo 'cloning the latest application version' "
        git branch: 'feature', url: 'https://github.com/drmalik7/maven-web-application.git'
        //git branch: 'feature', credentialsId: 'gitHubCredentials', url: 'https://github.com/LandmakTechnology/maven-web-application'
      }
    }
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
     stage('8deploy2prod'){
      steps{
        deploy adapters: [tomcat9(credentialsId: '6f4c1da1-712f-4634-8caf-33e3640e6117', path: '', url: 'http://18.209.7.70:8080/')], contextPath: null, war: 'target/*war'
        //deploy adapters: [tomcat8(credentialsId: 'tomcat-credentials', path: '', url: 'http://35.170.249.131:8080/')], contextPath: null, war: 'target/*war'   }
    }     
  }
}
post{
    always{
      emailext body: '''Hi
Progress report
Aviel technologies''', recipientProviders: [buildUser(), contributor(), upstreamDevelopers(), developers()], subject: 'Review Build status', to: 'paypay-prodteam@gmail.com'
/*emailext body: '''Hey guys
Please check build status.

Thanks
Landmark 
+1 437 215 2483''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'paypal-team@gmail.com'
    }
    success{
      emailext body: '''Hey guys
Good job build and deployment is successful.

Thanks
Landmark 
+1 437 215 2483''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'paypal-team@gmail.com'
    } 
    failure{
      emailext body: '''Hey guys
Build failed. Please resolve issues.

Thanks
Landmark 
+1 437 215 2483''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'paypal-team@gmail.com'
    }
  } */ 
}
}
}
