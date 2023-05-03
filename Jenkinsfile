pipeline {
    agent any
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