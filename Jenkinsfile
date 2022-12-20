

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
 
        stage('Permission') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }
    }
}
