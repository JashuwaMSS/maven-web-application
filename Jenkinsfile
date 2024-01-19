pipeline {//pipeline opening 

agent any 

tools {

maven "maven3.8.6"

}

stages {//stages opening 

stage('checkout the code') {

steps {

git branch: 'development', credentialsId: '0f883400-249a-44dd-bb36-09e062ce0775', url: 'https://github.com/JashuwaMSS/maven-web-application.git'
}

}
stage('Build') {

steps {


sh "mvn clean package" 

}

}

}//stages closing 

}//pipeline closing 
