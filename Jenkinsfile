

pipeline {
    agent {
     label ("node1 || node2 ||  node3 || node4 ||  node5 ||  branch ||  main ||  jenkins-node || docker-agent ||  jenkins-docker2 ||  preproduction ||  production")
            }

options {
    buildDiscarder(logRotator(numToKeepStr: '2'))
    disableConcurrentBuilds()
    timeout (time: 60, unit: 'MINUTES')
    timestamps()
  }

    stages {
        stage('Setup parameters') {
            steps {
                script {
                    properties([
                        parameters([    
                        
                        choice(
                            choices: ['Dev', 'Sanbox','Prod'], 
                            name: 'Environment'   
                                ),

                          string(
                            defaultValue: 's4user',
                            name: 'User',
			                description: 'Required to enter your name',
                            trim: true
                            ),

                          string(
                            defaultValue: 'Tankoua-Jenkinsfile-02',
                            name: 'DB-Tag',
			                description: 'Required to enter the image tag',
                            trim: true
                            ),

                          string(
                            defaultValue: 'Tankoua-Jenkinsfile-02',
                            name: 'UI-Tag',
			                description: 'Required to enter the image tag',
                            trim: true
                            ),

                          string(
                            defaultValue: 'Tankoua-Jenkinsfile-02',
                            name: 'WEATHER-Tag',
			                description: 'Required to enter the image tag',
                            trim: true
                            ),

                          string(
                            defaultValue: 'Tankoua-Jenkinsfile-02',
                            name: 'AUTH-Tag',
			                description: 'Required to enter the image tag',
                            trim: true
                            ),
                        ])
                    ])
                }
            }
        }
 
        stage('permission') {
            steps {
		sh '''
               cat <<EOF > check.sh
		#! /bin/bash 
		USER=${User}
		cat permission.txt | grep -i $USER
		if 
		[[ $? -eq 0 ]]
		then 
		echo "You have permission to run this job"
		else 
		echo "You DON'T have permission to run this job"
		exit 1
		fi 
		EOF
		bash check.sh
                '''
            }
        }
        stage('cleaning') {
            steps {
                sh '''
                ls 
                pwd
               
                '''
            }
        }
       stage('SonarQube analysis') {
            agent {
                docker {
                  image 'sonarsource/sonar-scanner-cli:4.7.0'
                }
               }
               environment {
        CI = 'true'
        //  scannerHome = tool 'Sonar'
        scannerHome='/opt/sonar-scanner'
    }
            steps{
                withSonarQubeEnv('Sonar') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        stage('build-dev') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }
        stage('build-sanbox') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        }
        stage('build-prod') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        }
        stage('login') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        }
        stage('push-to-dokerhub-dev') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        }
       stage('push-to-dokerhub-sanbox') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        } 
         stage('push-to-dokerhub-prod') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        } 
         stage('update helm charts-sanbox') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        }
          stage('update helm charts-dev') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        }
          stage('update helm charts-prod') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        }
          stage('wait for argocd') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        }
          stage('post build report') {
            steps {
                sh '''
                ls 
                pwd
                uname-r
                '''
            }
        }
    }
post {
   
   success {
      slackSend (channel: '#development-alerts', color: 'good', message: "SUCCESSFUL: Application S4-EKTSS  Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }

 
    unstable {
      slackSend (channel: '#development-alerts', color: 'warning', message: "UNSTABLE: Application S4-EKTSS  Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }

    failure {
      slackSend (channel: '#development-alerts', color: '#FF0000', message: "FAILURE: Application S4-EKTSS Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
    }
   
    cleanup {
      deleteDir()
    }
  }
}
}
