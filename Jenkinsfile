
pipeline{
    agent any
    tools{
         maven 'maven3.6'
    }
    stages{
        stage('checkout scm'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git_cred', url: 'https://github.com/Ravi053/Test_Job.git']]])
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the artifacts"
                    archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
                }
            }
        }
        stage('deploy'){
            steps{
                echo "deploying to tomcat"
               
            }
            post{
                success{
                   deploy adapters: [tomcat9(credentialsId: 'tomcatcredential', path: '', url: 'http://http://13.114.35.27:8080//')], contextPath: null, war: '**/*.war'
                }
            }
        }
         stage('test'){
            steps{
                   echo "testing team will run test cases"
                    sh 'sleep 2'
            }
         }    
    }
}
