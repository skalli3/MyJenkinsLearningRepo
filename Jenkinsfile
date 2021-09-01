pipeline {
  agent any
  tools { 
      maven 'mvnfc' //'/usr/share/maven' 
      //jdk //'/usr/lib/jvm/java-8-openjdk-amd64/jre' 
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
