pipeline {
    agent any 
    stages {
        stage('Compile and Clean') {
            steps {
               sh "mvn clean compile"
            }
        }
        stage('test') {
            steps {
                sh "mvn test" 
            }
        }
        stage('deploy') {
            steps {
                sh "mvn package" 
            }
        }
	stage('Build Docker Image') {
            steps {
                sh "docker build -t kishoregubili/docker-jenkinsfile:${BUILD_NUMBER} ." 
            }
        }
	stage('Docker Login') {
            steps {
                sh "docker login -u kishoregubili -p kishore2A@" 
            }
        }
	stage('Docker Pushing to Repository') {
            steps {
                sh "docker push kishoregubili/docker-jenkinsfile:${BUILD_NUMBER}" 
            }
        }
	stage('Archiveing'){
	   steps{
	       archiveArtifacts '**/target/*.jar'
	       }
	}
    }
}
