node {
    stage "Prepare environment"
        checkout scm
        def environment  = docker.build 'cloudbees-node'

        environment.inside {
            stage "Checkout and build deps"
                sh "yarn"

            stage "Validate types"
                sh "./node_modules/.bin/flow"

            stage "Test and validate"
                sh "yarn add gulp-cli --no-lockfile && ./node_modules/.bin/gulp"
                step([$class: 'JUnitResultArchiver', testResults: 'reports/**/*.xml'])
        }

    stage "Cleanup"
        deleteDir()
}
