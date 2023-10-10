pipeline {
    agent any
  
    stages {
 stage('Pull Repository') {
            steps {
                // Pull the repository source code from Git
                git branch: 'master', url: 'https://github.com/Jlassi25/jenkins-test.git'
            }
        }
    
        stage('Build Spring') {
            
            steps {
                      sh '''
         mvn clean package
         cd target
         cp ../src/main/resources/web.config web.config
         cp todo-app-java-on-azure-1.0-SNAPSHOT.jar app.jar 
         zip todo.zip app.jar web.config
      '''

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
