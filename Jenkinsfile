pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/Bhavesh-Muleva/demo-counter-app.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'Sonar-Token') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                      waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-Token'
//                          timeout(time: 5, unit: ‘MINUTES’) {
//                              def qg= waitForQualityGate()
//                              if (qg.status!= ‘OK’){
//                                 error “Pipeline aborted due to quality gate failure: ${qg.status}”
//                              }
//                          }         
//                      echo ‘Quality Gate Passed’
                    }
                }
            }
        }
}
