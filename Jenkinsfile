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
        withCredentials([usernamePassword(credentialsId: 'server', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
  // available as an env variable, but will be masked if you try to print it out any which way
  // note: single quotes prevent Groovy interpolation; expansion is by Bourne Shell, which is what you want
  sh 'echo $PASSWORD'
  // also available as a Groovy variable
  echo USERNAME
  // or inside double quotes for string interpolation
  echo "username is $USERNAME"
}
      }
    }
  }
}
