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
            sh 'git checkout learning_J'
        }
    }
    stage('Build') {
        steps {
            git url: 'https://github.com/skalli3/MyJenkinsLearningRepo.git'
            withMaven {
                    sh "mvn clean verify"
            } 
        }
    }
    stage('deploy') {
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
    error{
          echo 'Build was exited with error'  
    }
  }  
}
