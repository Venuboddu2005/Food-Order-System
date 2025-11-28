pipeline {
    agent any 

    stages{

        stage("BuildCode"){
            steps {
                sh "ant clean"
                sh "ant jar"
            }
        }
    }
}