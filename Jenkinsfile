pipeline {
  agent any
  tools { 
      maven 'mvn'
    }
  options {
    timestamps()
  }
  environment {
     DISABLE_AUTH = true
     DB_ENGINE    = 'sqlite'
     VERSION      = '1.3.0'
  }
  parameters{
     //string(name: 'ENVIRONMENT', defaultValue: 'UAT', description: 'Target Environment')
     choice(name: 'DATABASE VERSION', choices:['1.1.0','1.2.0','1.3.0'], description: 'used database version')
     booleanParam(name: 'APPLICATION_META', defaultValue: true, description: 'Facebook')
  }  
  stages {
    stage('pre-Build') {
        steps {
            git url: 'https://github.com/skalli3/MyJenkinsLearningRepo.git'
            //sh 'git checkout learning_J'
            echo "the Database Engine is: ${DB_ENGINE}"
            echo "the deactivation of authentication is: ${env.GIT_BRANCH}"
            echo "target Meta Application: ${params.APPLICATION_META}"
        }
    }
    stage('Build') {
        /*when {
          expression{
             env.GIT_BRANCH == 'origin/er' 
          }  
        }*/
        steps {
            git url: 'https://github.com/skalli3/MyJenkinsLearningRepo.git'
            /*withMaven {
                    sh "mvn clean test"
            }*/
            sh "mvn clean package"
          
            
        }
    }
    stage('Test') {
        steps {
            sh "mvn clean test"  
        }
    }
    stage('deploy') {
        /*when {
          expression{
             params.TO_DEPLOY == true 
          }  
        }*/

        steps {
          input(message: 'do you want to deploy to production?', ok: 'Yes')
          sh "mvn exec:java -Dexec.mainClass=\"alv\""
        }
    }
  }
  post{
      always{
          echo 'The build was finished'
      }
    success{
          echo 'Build was succeeded'  
    }
    aborted{
          echo 'Build was exited with error'  
    }
  }  
}
