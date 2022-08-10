pipeline{
     agent any
  tools{
      jdk 'java8'
      maven 'maven'
  }
  environment{
      NEW_VERSION='1.2.0'
      SERVER_CRED=credentials('server')
  }
  parameters{
    string(name: 'Branch',defaultValue: 'main',description: 'please type branch')
    choice(name: 'Version',choices: ['1.2.0','1.2.1','1.2.2'],description: 'select version')
    booleanParam(name: 'executeTests',defaultValue: true,description: 'test')
  }
  stages{
    stage("build"){
      steps{
         echo "build application"
      }
    }
    stage("test"){
      when{
        expression{params.executeTests}
      }
      steps{
         echo "test application"
      }
    }
    stage("deploy"){
      when{
           expression{params.Branch=='main'}
      }
      steps{
         echo "deploy application"
         withCredentials([
                       usernamePassword(credentialsId: 'server',usernameVariable: 'USER', passwordVariable: 'PWD')])
                        { 
                               sh "some script ${USER} ${PWD}"
                         }
      }
    }
  }
}
