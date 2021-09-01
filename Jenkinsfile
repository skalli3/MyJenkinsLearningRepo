//CODE_CHANGES = getGitChanges()
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
  }
  stages {
    stage('pre-Build') {
        steps {
            git url: 'https://github.com/skalli3/MyJenkinsLearningRepo.git'
            sh 'git checkout master'
        }
    }
    stage('Build') {
       //echo 'its OKKKKKKKKKKKKKKK'
        when {
          expression{
             env.BRANCH_NAME == 'master' || DISABLE_AUTH == true 
          }  
        }
        steps {
            git url: 'https://github.com/skalli3/MyJenkinsLearningRepo.git'
            withMaven {
                    sh "mvn clean verify"
            }
            
        }
    }
    stage('deploy') {
        when {
          expression{
             env.BRANCH_NAME == 'learning_J' //||  $BRANCH_NAME == 'learning_K' 
          }  
        }
        steps {
            git url: 'https://github.com/skalli3/MyJenkinsLearningRepo.git'
            withMaven {
                    sh "mvn clean verify"
            } 
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
