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
    
}
