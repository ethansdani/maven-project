pipeline {
	agent any
		stages {
			stage ('Fetch Source') {
				steps {
					git 'https://github.com/ethansdani/maven-project.git'
				}
			}
			stage ('Build') {
				steps {
					withMaven(jdk: 'JAVA_HOME', maven: 'MAVEN_HOME') {
					sh 'mvn clean install'
					}
				}
			}
			stage ('Archive Artifacts') {
				steps {
					archiveArtifacts artifacts: '**/*.war', fingerprint: true
				}
			}
			stage ('Deploy') {
				steps {
					deploy adapters: [tomcat7(credentialsId: 'e466ad80-4c69-4bf6-896d-2b1122865f54', path: '', url: 'http://52.66.205.167:8080/')], contextPath: null, war: '**/*.war'
				}
			}
			
		}
}
