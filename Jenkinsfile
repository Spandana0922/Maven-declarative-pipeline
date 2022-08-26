pipeline {
    agent { label 'redhat-node' }
    tools {
      maven 'apache-maven-3.8.6'
    }
    triggers {
        pollSCM 'H * * * *'
    }
    stages {
        stage('clone') {
            steps {
                git 'https://github.com/Spandana0922/Maven-declarative-pipeline.git'
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
                deploy adapters: [tomcat9(credentialsId: 'admin', path: '', url: 'http://http://13.234.111.184:8080/')], contextPath: 'java-web-app', war: '**/*.war'
            }            
        }
          
    }
}
