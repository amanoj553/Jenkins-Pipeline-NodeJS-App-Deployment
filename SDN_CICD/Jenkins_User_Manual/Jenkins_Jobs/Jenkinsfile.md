# Pipeline script for Application Deployment in Testbed


pipeline {
    agent {
        label 'WebApp_1'
    }

    stages {
        stage ('source stage') {
            steps {
             
                git branch: 'develop', url: 'https://github.com/openBackhaul/RegistryOffice.git' //credentialsId: 'github-jenkins'
            }
        }
        stage ('Docker Build and Tag') {

            steps {

                dir ('server')
                    {
                    sh 'docker ps -a'
                    sh 'docker stop registry-office-v1'
                    sh 'docker rm registry-office-v1'
                    sh 'docker rmi cicd_user/registry-office-v1'
                    sh "sed -i 's/^RUN npm install/RUN  npm --proxy http:\\/\\/172.16.1.2:8080 --without-ssl --insecure -g install/' dockerfile"
                    sh 'docker build -t cicd_user/registry-office-v1 .'
                    //sh 'docker tag registry-office-v1 cicd_user/registry-office-v1:$BUILD_NUMBER'
                }
            } 
        }
        /*stage('Publish image to Docker Hub') {
          
            steps {

                withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
                    sh  'docker push cicd_user/registry-office-v1'
                    //sh  'docker push cicd_user/registry-office-v1:$BUILD_NUMBER' 
                }       
            }
        }*/         
        stage('Run Docker container') {
             
            steps {

                sh 'docker run -d -p 8083:3000 --name registry-office-v1 -v TinyApplicationControllers:/home/openbackhaul/database/registryOffice cicd_user/registry-office-v1'
                echo '==========> List Images <=========='
                sh 'docker images'
                echo '=========> List Container <========='
                sh 'docker ps -a'
 
            }
        }
        /*stage('Run Docker container on remote hosts') {
             
            steps {

                sh 'docker -H ssh://jenkins@remote ip run -d -p 3000:3000 repo-name'
 
            }
        }*/
        stage('save Docker image'){

            steps{

                sh 'docker save -o /home/WebApp/gitlab_stage/docker-images-list/cicd_user-registry-office-v1-$(date +%Y-%m-%d-%H:%M:%S).tar cicd_user/registry-office-v1'

            }
        }
        /*stage(test){
              
            steps {
                echo 'Running Acceptence Test for app..'
                //sh  'docker -H ssh:cicduser@172.29.145.204:/home/cicduser/app/'
                dir('test-scripts'){
                    sh 'node RegistryOffice.js'
                }
            } 
        }*/
    }
    post {
        success {
            echo 'Deploy RegistryOffice Application completed in WebApp server..'
            //mail to: manoj.arra.external@telefonica.com, subject: ‘The Pipeline success :(‘
            
        }
    }
}


# Pipeline script for Acceptance Testcases in Testbed environment

pipeline {
    agent {
        label 'jenkins-master'
    }

    stages {
        stage ('source stage') {
            steps {
             
                git branch: 'develop', url: 'https://github.com/openBackhaul/RegistryOffice.git' //credentialsId: 'github-jenkins'
            }
        }
        stage ('copy RO postman collection file') {
            steps {

                 dir ('/var/lib/jenkins/workspace/RO_Testcases/test-suites/')
                    {
                    
                    sh 'cp RegistryOffice_0.0.1_tsi.date.time+testcases.1.postman_collection /var/lib/jenkins/workspace/RO_testcases'
                    
                }
            }
        }
        /*stage ('Replace  server details') {
            steps {

                 dir ('/var/lib/jenkins/workspace/RO_Testcases')
                    {
                    
                    sh "sed -i '' 's/https://125bf8ff-8193-4784-802a-b33bc1ec7879.mock.pstmn.io/http://172.29.145.71:8083/g' RegistryOffice_0.0.1_tsi.date.time+data.no.json"
                    
                }
            }
        }*/
        stage ('run Acceptance test cases') {
            steps {

                 dir ('/var/lib/jenkins/workspace/RO_testcases/')
                    {
                    
                    sh 'newman run RegistryOffice_0.0.1_tsi.date.time+testcases.1.postman_collection -d RegistryOffice_0.0.1_tsi.date.time+data.no.json -r htmlextra,cli --reporter-htmlextra-logs'

                }
            }
        }  
                stage ('Print test results in workspace dir.') {
            steps {

                 dir ('/var/lib/jenkins/workspace/RO_testcases/newman')
                    {
                    
                    sh 'ls -lrt'

                }
            }
        }  
    }
    post {
        success {
            echo 'Acceptance test cases are successfully running on RO Application..'
            //mail to: manoj.arra@ojas-it.com, subject: ‘The Pipeline success :(‘
        }
    
    }
}

# pipeline script for Application Deployment in Production

pipeline {
    
    agent {
        label 'Appserver_2'
    }

    stages {
        stage ('Docker image load stage') {
            steps {

                 dir ('/home/appserver/gitlab_prod/docker-images')
                    {
                    
                    sh 'docker images'
                    //sh 'docker ps -a'
                    //sh 'docker stop registry-office-v1'
                    //sh 'docker rm registry-office-v1'
                    //sh 'docker rmi cicd_user/registry-office-v1'
                    sh 'docker load -i cicd_user-registry-office-v1-2022-04-19-15:51:27.tar'
                    //sh 'docker tag aregistry-office-v1 cicd_user/registry-office-v1:$BUILD_NUMBER'

                }
            }
        }          
        /*stage('Publish image to Docker Hub') {
          
            steps {

                withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
                    sh  'docker push cicd_user/registry-office-v1:latest'
                    //sh  'docker push cicd_user/registry-office-v1:$BUILD_NUMBER' 
                }       
            }
        }*/         
        stage('Run Docker container') {
             
            steps {

                sh 'docker run -d -p 8083:3000 --name registry-office-v1 -v TinyApplicationControllers:/home/openbackhaul/database/registryOffice cicd_user/registry-office-v1'
                echo '==========> List Images <=========='
                sh 'docker images'
                echo '=========> List Container <========='
                sh 'docker ps -a'
 
            }
        }
        /*stage('Run Docker container on remote hosts') {
             
            steps {

                sh 'docker -H ssh://jenkins@remote ip run -d -p 8083:3000 repo-name'
 
            }
        }*/
    }
    environment {
            EMAIL_TO = 'manoj.arra.external@telefonica.com'
        }
    post {
    	success {
                emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                        to: "${EMAIL_TO}", 
                        subject: 'Successfull Build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    	failure {
                emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                        to: "${EMAIL_TO}", 
                        subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        unstable {
                emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                        to: "${EMAIL_TO}", 
                        subject: 'Unstable build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        changed {
                emailext body: 'Check console output at $BUILD_URL to view the results.', 
                        to: "${EMAIL_TO}", 
                        subject: 'Jenkins build is back to normal: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    }
}

# Pipeline script for Integration test cases in Production environment

pipeline {
    agent {
        label 'jenkins_master'
    }

    stages {
        stage ('source stage') {
            steps {
             
                git branch: 'develop', url: 'https://github.com/openBackhaul/RegistryOffice.git' //credentialsId: 'github-jenkins'
            }
        }
        stage ('copy RO postman collection file') {
            steps {

                 dir ('/var/lib/jenkins/workspace/RO_Testcases/test-suites/')
                    {
                    
                    sh 'cp RegistryOffice_0.0.1_tsi.date.time+testcases.1.postman_collection /var/lib/jenkins/workspace/RO_Testcases'
                    
                }
            }
        }
        /*stage ('Replace  server details') {
            steps {

                 dir ('/var/lib/jenkins/workspace/RO_Testcases')
                    {
                    
                    sh "sed -i '' 's/https://125bf8ff-8193-4784-802a-b33bc1ec7879.mock.pstmn.io/http://10.20.64.41:8083//g' RegistryOffice_0.0.1_tsi.date.time+data.no.json"
                    
                }
            }
        }*/
        stage ('run Integration test cases') {
            steps {

                 dir ('/var/lib/jenkins/workspace/RO_Testcases/')
                    {
                    
                    sh 'newman run RegistryOffice_0.0.1_tsi.date.time+testcases.1.postman_collection -d RegistryOffice_0.0.1_tsi.date.time+data.no.json -r htmlextra,cli --reporter-htmlextra-logs'

                }
            }
        }  
        stage ('Print test results in workspace dir.') {
            steps {

                 dir ('/var/lib/jenkins/workspace/RO_Testcases/newman')
                    {
                    
                    sh 'ls -lrt'

                }
            }
        }
    }
    environment {
            EMAIL_TO = 'manoj.arra.external@telefonica.com , rajitha.pitta.external@telefonica.com'
        }
    post {
    	success {
                emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                        to: "${EMAIL_TO}", 
                        subject: 'Successfull Build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    	failure {
                emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                        to: "${EMAIL_TO}", 
                        subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        unstable {
                emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                        to: "${EMAIL_TO}", 
                        subject: 'Unstable build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        changed {
                emailext body: 'Check console output at $BUILD_URL to view the results.', 
                        to: "${EMAIL_TO}", 
                        subject: 'Jenkins build is back to normal: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    }
}


 [<- Back to Jenkins PollSCM Jobs](../Jenkins_Jobs/Jenkins-pollSCM-PipelineJob.md) - - - [Back to Main](../main.md)
