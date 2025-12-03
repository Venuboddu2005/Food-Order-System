pipeline {
    agent any 
    stages{

        stage("BuildCode"){
            steps {
                sh """
                    cd food_order
                    ant clean
                    ant jar
                """
            }
        }

        stage("Run-Unit-Tests"){
            steps {
                sh """
                    cd food_order
                    ant clean
                    ant test
                """
            }
        }

        stage("Sonar-Scanning"){
            steps {
               
               script {
                    withSonarQubeEnv( installationName: 'sonar-server-01', credentialsId: 'sonar-jenkins-creds') {
                        sh """
                            cd food_order
                            sonar-scanner \
                                        -Dsonar.projectKey=Food-Order-System \
                                        -Dsonar.projectName=Food-Order-System \
                                        -Dsonar.sources=. \
                                        -Dsonar.sourceEncoding=UTF-8
                        """
                    }
               }
            }
        }

        stage("Sonar Quality Gate") {
            steps {
                script {
                    timeout(time: 3, unit: 'MINUTES') {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline failed due to quality gate: ${qg.status}"
                        }
                    }
                }
            }
        }

        stage("Upload-Artifacts-Nexus"){
            steps {

                script {

                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: 'nexus:8081',
                        groupId: 'com.example',
                        version: '1.0.0',
                        repository: 'maven-public',
                        credentialsId: 'nexus-creds',
                        artifacts: [
                            [
                                file: "Food-Order-System/food_order/dist/anagrams.jar",
                                type: "jar",
                                classifier: ""
                            ]
                        ]
                    )

                }

            }
        }

    }
}