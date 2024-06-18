@Library("shared") _

pipeline {
    agent any
    
    stages{
        stage('git')
        {
            steps
            {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/javahometech/ga-app'
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
                tomcatDeploy("172.31.41.246", "ec2-user", "ga-app.war", "tomcat-dev")
                }
            }
        }
        post {
  success {
    cleanWs()
  }
}
    }
