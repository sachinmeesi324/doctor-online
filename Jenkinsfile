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
        stage('tomcat dev deploy')
        {
            when{
                branch 'dev'
            }
            steps{
                tomcatDeploy("172.31.41.246", "ec2-user", "doctor-online.war", "tomcat-dev")
                echo "Deploying dev"
                }
            }

        stage('tomcat test deploy')
        {
             when
             {
                   branch 'test'
             }
            steps{
                tomcatDeploy("172.31.41.246", "ec2-user", "doctor-online.war", "tomcat-dev")
                echo "Deploying test"
                }
            }

            stage('tomcat prod deploy')
        {
             when{
                branch 'prod'
            }
            steps{
                tomcatDeploy("172.31.41.246", "ec2-user", "doctor-online.war", "tomcat-dev")
                echo "deploying to prod"
                }
            }

        }
        post {
  success {
    cleanWs()
  }
}
    }
