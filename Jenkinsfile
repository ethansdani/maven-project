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
					cmd 'mvn clean install'
					}
				}
			}
			stage ('Archive Artifacts') {
				steps {
					archiveArtifacts artifacts: '**/*.war', fingerprint: true
				}
			}
			stage ('Copy Artifacts') {
				steps {
					copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, projectName: 'sample-project'
				}
			}
			stage ('Deploy') {
				steps {
					deploy adapters: [tomcat7(credentialsId: '319d5184-50b8-4c81-93eb-98d0d9f6edab', path: '', url: 'http://localhost:9090')], contextPath: null, onFailure: false, war: '**/*.war'
				}
			}
			
		}
}
