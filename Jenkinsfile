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
                echo "Scanning code..."
            }
        }

        stage("QG-Check"){
            steps {
                echo "Checking QG..."
            }
        }



    }
}