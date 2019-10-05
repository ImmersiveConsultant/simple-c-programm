pipeline {
    agent any

    options {
        skipDefaultCheckout true
        buildDiscarder(logRotator(
            numToKeepStr: '3',
            daysToKeepStr: '3'))
        disableConcurrentBuilds()
        timestamps()
        timeout(time: 5, unit: 'MINUTES')
    }

    environment {
    }
    stages {
        stage('sanitize build environment') {
            steps {
                step([$class: 'WsCleanup'])
            }
        }
        stage('checkout') {
            steps {
                dir('src') {
                    checkout scm
                }
            }
        }
        stage('build') {
            steps {

                echo """
                    # #######################################################################
                    #                                                                       #
                    # We are basing our builds on these assumptions:                        #
                    #                                                                       #
                    # *  there is no information that needs to be changed                   #
                    #    IOW: all the source, no exceptions, can be used and built verbatim #
                    #    THAT INCLUDES AND IS ESPECIALLY TRUE FOR VERSION NUMBERs!          #
                    #                                                                       #
                    # *  All version numbers have been set and tested before commiting      #
                    #                                                                       #
                    # #######################################################################

                    (the SysAdmins send their regards!)
                """
                echo 'gcc --version'
            }
        }
        stage('publish'){
            steps {
                echo """
                    # #######################################################################
                    #                                                                       #
                    # *  You must not assume that you will be able to:                      #
                    #    * CHANGE any existing artifact that already has been built         #
                    #    * DELETE any existing artifact that already has been built         #
                    #    * RENAME any existing artifact that already has been built         #
                    #    * MOVE   any existing artifact that already has been built         #
                    #                                                                       #
                    # #######################################################################
                """
            }
        }
    }
    post {
        always {
            echo "This will always run."

        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'You killed the build!'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
