pipeline {
    
    agent none
    
    tools{
        maven 'Maven'
        
    }
    

    
    stages {
        
        stage ('Initialise'){
            
            steps{
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
            }
            
        }
        
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }

        // stage('Deploy'){
        //     steps{
        //         sshagent(['Tomcat']){
        //             sh 'scp -o StrictHostKeyChecking=no target/WebApp.war ubuntu@43.204.110.54:/var/lib/tomcat10/webapps/webapp.war'
        //         }

        //     }
        // }

        stage('Run Docker'){

            agent { label 'integration-slave' }
            steps {
                sh 'pwd'

            }

        }
        
    }
    
}
