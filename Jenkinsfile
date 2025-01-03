// pipeline {
//     agent any

//     stages {
//         stage('Build') {
//             steps {
//                 echo 'Creating virtual environment and installing dependencies...'
//                 bat 'python -m venv venv'
//                 bat 'venv\\Scripts\\pip install -r requirements.txt'
//     }
// }

// }
//         stage('Test') {
//             steps {
//                 echo 'Running tests...'
//                 sh 'python3 -m unittest discover -s .'
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 echo 'Deploying application...'
//                 sh '''
//                 mkdir -p ${WORKSPACE}/python-app-deploy
//                 cp ${WORKSPACE}/app.py ${WORKSPACE}/python-app-deploy/
//                 '''
//             }
//         }
//         stage('Run Application') {
//             steps {
//                 echo 'Running application...'
//                 sh '''
//                 nohup python3 ${WORKSPACE}/python-app-deploy/app.py > ${WORKSPACE}/python-app-deploy/app.log 2>&1 &
//                 echo $! > ${WORKSPACE}/python-app-deploy/app.pid
//                 '''
//             }
//         }
//         stage('Test Application') {
//             steps {
//                 echo 'Testing application...'
//                 sh '''
//                 python3 ${WORKSPACE}/test_app.py
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed. Check the logs for more details.'
//         }
//     }
// }
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Creating virtual environment and installing dependencies...'
                sh '''
                python -m venv venv
                source venv/Scripts/activate
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh '''
                source venv/Scripts/activate
                python -m unittest discover -s .
                '''
            }
        }
        stage('Deploy') {
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                echo 'Deploying application...'
                // Add deployment steps
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed.'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
