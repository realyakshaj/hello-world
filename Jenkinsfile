pipeline{
    agent any
    stages{
        stage("clone repo"){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devops-ismailattar/hello-world.git']])
                
            }
        }
        
        stage("mvn packange insall"){
            steps{
                sh "mvn clean install"
            }
        }
        
        
        stage("copy war file tomcat server"){
            steps{
                sshagent(['tomcat']){
                   // some block
                   sh """
                   
                   scp -o StrictHostKeyChecking=no webapp/target/*.war ubuntu@172.31.10.169:/opt/apache-tomcat-9.0.94/webapps
                   ssh ubuntu@172.31.10.169 /opt/apache-tomcat-9.0.94/bin/shutdown.sh
                   ssh ubuntu@172.31.10.169 /opt/apache-tomcat-9.0.94/bin/startup.sh
                   
                   
                   """
                    
                }
                
                
            }
        }
    }
}
***
