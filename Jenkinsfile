node { //node opening 

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

def mavenHome = tool name: "maven3.8.6"

stage('Checkout the code') {

git credentialsId: '0f883400-249a-44dd-bb36-09e062ce0775', url: 'https://github.com/JashuwaMSS/maven-web-application.git'

}

stage('Build') {

sh "${mavenHome}/bin/mvn clean package" 

}
stage('Execute the Sonarqube report') {

sh "${mavenHome}/bin/mvn clean sonar:sonar" 

}
stage('Upload Build Artifact into nexus repository') {

sh "${mavenHome}/bin/mvn clean deploy"

}
stage('Deploy the package into Application Server') {

sshagent(['8be945bf-8cf1-4152-8a9f-157cdb93eae2']) {
    
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.7.253.217:/opt/apache-tomcat-9.0.83/webapps/"

}

}

} //node closing
