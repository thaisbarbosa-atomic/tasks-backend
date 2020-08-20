pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests') {
            steps {
                bat 'mvn test'
            }
        }
        stage ('Deploy Backend') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'TomCatLogin', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
            }
        }
        stage ('API Test') {
            steps {
            	dir('api-test') {
    				git credentialsId: 'github_login', url: 'https://github.com/thaisbarbosa-atomic/tasks-api-test'
            		bat 'mvn test'
				}
            }
        }
        stage ('Deploy Frontend') {
            steps {
                    dir('frontend') {
    					git credentialsId: 'github_login', url: 'https://github.com/thaisbarbosa-atomic/tasks-frontend'
            			bat 'mvn clean package
            			deploy adapters: [tomcat8(credentialsId: 'TomCatLogin', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks', war: 'target/tasks.war'
					}
            }
        }
        
        
        
    }
}


