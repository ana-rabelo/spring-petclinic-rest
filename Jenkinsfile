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
                withJavaHome {
                    sh 'mvn -B install --file pom.xml -Djacoco.skip=true -DdisableXmlReport=true'
                }
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    publishFlakyTestDetails(
                        flakyFailureThreshold: 3,
                        markAsFlakyThreshold: 2,
                        flakyFailureDiffThreshold: 10,
                        unclassifiedAsFlaky: true,
                        inputFilesPattern: '**/target/surefire-reports/*.xml',
                        flakyTestsOutputFile: 'flaky-tests.csv',
                        failedTestsOutputFile: 'failed-tests.csv'
                    )
                }
            }
        }
    }
}
