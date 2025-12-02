pipeline {
    agent any 
    // tools {
    //     ant 'ant-1.10.15'   // <--- uses the Ant tool named ant-1.10.15
    // }

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