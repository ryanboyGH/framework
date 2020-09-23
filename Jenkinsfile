node {
    stage("composer_install") {
        // Run `composer update` as a shell script
        sh 'composer update'
    }
    stage("phpunit") {
        // Run PHPUnit
        sh 'vendor/bin/phpunit'
    }

    // If this is the master or develop branch being built then run
    // some additional integration tests
    if (["master", "8.x"].contains(env.BRANCH_NAME)) {
        stage("integration_tests") {
            sh 'echo integration_tests'
        }
    }

    // Create new deployment assets
    switch (env.BRANCH_NAME) {
        case "master":
            stage("codedeploy") {
                sh "echo codedeploy"
            }
            break
        case "8.x":
            stage("codedeploy") {
                sh "echo 8.x"
            }
            break
        default:
            // No deployments for other branches
            break
    }
}
