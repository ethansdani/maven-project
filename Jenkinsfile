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
			stage('Confirm Deploy to Staging') {
				agent none
				steps {
				input(message: 'Deploy to Stage', ok: "Yes, let's do it!")
				}
			}
			stage ('Deploy') {
				steps {
					sshagent(['4c1a1761-cc25-4f2c-abce-7d43911dcaa4']) {
						sh 'scp webapp/target/*.war ec2-user@52.66.205.167:/usr/share/tomcat/webapps/'
					}
				}
			}
			
		}
}
