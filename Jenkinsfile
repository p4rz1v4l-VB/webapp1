pipeline {
    
    agent none
    
    tools{
        maven 'Maven'
        
    }
    

    
    stages {
        
        stage ('Initialise'){

             agent {
            label 'built-in'
            }
            
            steps{
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
            }
            
        }

        stage('Check Git Secrets'){

            sh '''
            docker pull gesellix/trufflehog
            docker run gesellix/trufflehog --json https://github.com/p4rz1v4l-VB/webapp.git > trufflehog
            cat trufflehog
            '''

        }
        
        stage('Build'){

            agent {
            label 'built-in'
            }
            steps{
                sh 'mvn clean package'
            }
        }

        // stage('Deploy'){
        //     agent {
        //     label 'built-in'
        //     }
        //     steps{
        //         sshagent(['Tomcat']){
        //             sh 'scp -o StrictHostKeyChecking=no target/WebApp.war ubuntu@13.232.214.108:/var/lib/tomcat10/webapps/webapp.war'
        //         }

        //     }
        // }
        
    }
    
}
