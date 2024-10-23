pipeline {
    
    agent any
    
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

        stage('Check Git Secrets'){

            steps{

            sh '''
            docker pull gesellix/trufflehog
            docker run gesellix/trufflehog --json https://github.com/p4rz1v4l-VB/webapp.git > trufflehog
            cat trufflehog
            '''
            }

        }

        stage ('Source Composition Analysis') {
            steps {
                sh 'rm owasp* || true'
                sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
                sh 'chmod +x owasp-dependency-check.sh'
                sh 'bash owasp-dependency-check.sh'
                sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
      }
    }
        stage ('SAST'){
            steps{
                withSonarQubeEnv('SonarQube'){
                sh 'mvn sonar:sonar'
                sh 'cat target/sonar/report-task.txt'
                }
            }
        }
        
        stage('Build'){


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
