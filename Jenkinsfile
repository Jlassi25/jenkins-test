pipeline {
    agent any
  tools { 
      maven 'MAVEN_HOME' 
      jdk 'JAVA_HOME' 
    }
    stages {
 stage('Pull Repository') {
            steps {
                // Pull the repository source code from Git
                git branch: 'master', url: 'https://github.com/Jlassi25/jenkins-test.git'
            }
        }
    
        stage('Build Spring') {
            
            steps {
                      sh 'mvn clean install '

            }
        }
        stage('Build docker image') {
            steps {
             script{
                sh 'docker build -t firstspring .'
             }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d -p 8080:8080 firstspring'
                }
            }
        }
    }
}
