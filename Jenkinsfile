pipeline {
  agent any
  /*tools { 
      maven 'mvn'
    }*/
  options {
    timestamps()
  }
  environment {
     DISABLE_AUTH = true
     DB_ENGINE    = 'sqlite'
     VERSION      = '1.3.0'
  }
  parameters{
     string(name: 'ENVIRONMENT', defaultValue: 'UAT', description: 'Target Environment')
     choice(name: 'VERSION', choices:['1.1.0','1.2.0','1.3.0'], description: 'deployment version choice')
     booleanParam(name: 'TO_DEPLOY', defaultValue: true, description: 'if to deploy')
  }  
  stages {
    stage('pre-Build') {
        steps {
            //git url: 'https://github.com/skalli3/MyJenkinsLearningRepo.git'
            //sh 'git checkout learning_J'
            echo "the Database Engine is: ${DB_ENGINE}"
            echo "the deactivation of authentication is: ${env.GIT_BRANCH}"
            echo "to deploy or not: ${params.TO_DEPLOY}"
        }
    }
    stage('Build') {
        when {
          expression{
             //env.GIT_BRANCH == 'origin/er' 
          }  
        }
        steps {
            /*git url: 'https://github.com/skalli3/MyJenkinsLearningRepo.git'
            withMaven {
                    sh "mvn clean verify"
            }*/
            
        }
    }
    stage('deploy') {
        when {
          expression{
             params.TO_DEPLOY == true 
          }  
        }
        steps {
          sh  'ssh -tt bdellatif_skalli@146.148.70.108'
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
