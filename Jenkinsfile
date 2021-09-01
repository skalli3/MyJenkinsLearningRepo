CODE_CHANGES = getGitChanges
pipeline {
  agent any
  tools { 
      maven 'mvn'
    }
  options {
    timestamps()
  }
  stages {
    stage('pre-Build') {
        steps {
            git url: 'https://github.com/skalli3/MyJenkinsLearningRepo.git'
            sh 'git checkout master'
        }
    }
    stage('Build') {
        when {
          expression{
             BRANCH_NAME == 'learning_J' && CODE_CHANGES == true 
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
             BRANCH_NAME == 'learning_J' ||  $BRANCH_NAME == 'learning_K' 
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
