pipeline {
    agent { label 'java-node' }
    tools {
      maven 'apache-maven-3.8.6'
    }
    triggers {
        pollSCM 'H * * * *'
    }
    stages {
        stage('clone') {
            steps {
                git 'https://github.com/Spandana0922/java-web-app-docker.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('archive artifacts') { 
            steps {
                archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false 
            }
            
        }
        stage('deploy') { 
            steps {
                deploy adapters: [tomcat9(credentialsId: 'admin', path: '', url: 'http://13.233.207.245:8080/')], contextPath:null, war: '**/*.war'
            }            
        }
          
    }
}
