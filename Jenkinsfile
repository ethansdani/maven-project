pipeline {

agent any

stages
{

stage('cloning code')

{

steps

{git 'https://github.com/chaitanyapratap19/maven-project.git'
}
}

stage('compile my project')
{
steps
{
withMaven(jdk: 'localJDK', maven: 'localMaven') {
    sh 'mvn compile'
	println 'added println'
}}}
    
stage('test my project')
{
steps
{
withMaven(jdk: 'localJDK', maven: 'localMaven') {
    sh 'mvn test'
}}}
    
stage('package my project')
{
steps
{
withMaven(jdk: 'localJDK', maven: 'localMaven') {
    sh 'mvn package'
}}}
    

    
        
stage('package my install')
{
steps
{
withMaven(jdk: 'localJDK', maven: 'localMaven') {
    sh 'mvn install'
}}}
	
   
	
	
stage('deploy to  tomcat')
{
steps
{
    sshagent(['tomcat']) {
	 sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@172.31.93.79:/var/lib/tomcat/webapps'
						}
}
}
    
    
    

}
}
