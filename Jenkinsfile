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
        
        stage('Build'){

            agent {
            label 'built-in'
            }
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

            agent{
                 docker.withServer('tcp://10.0.0.33:2375'){
                     docker.image('varun/tomcat:latest').withRun('-p 80:8080'){
                         sh 'pwd'
                     }

                 }
            }
            options{skipDefaultCheckout true}
            steps {
                sh '''pwd
                /usr/local/tomcat/bin/catalina.sh run
                '''

            }

        }
        
    }
    
}
