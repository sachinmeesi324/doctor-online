@Library("shared") _

pipeline {
    agent any
    
    stages{
        stage('git')
        {
            steps
            {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/javahometech/doctor-online'
            }
        }
        stage('build')
        {
            steps{
            sh 'mvn clean package'
            }
        }
        stage('tomcat deploy')
        {
            steps{
                tomcatDeploy("172.31.41.246", "ec2-user", "doctor-online.war", "tomcat-dev")
                }
            }
        }
        post {
  success {
    cleanWs()
  }
}
    }
