pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('Frontend Tests') {
            agent {
                docker {
                    image 'btamas/puppeteer-git'
                    reuseNode true
                }
            }
            environment {
                HOME = '.'
                PARALLEL_TESTS = 2
            }
            options {
                skipDefaultCheckout()
            }
            steps {
                dir('.') {
                    sh(
                        label: 'Setup frontend toolchain',
                        script: 'npm install'
                    )
                    sh(
                        label: 'Show eslint errors'
                        script: 'npm run lint || true'
                    )
                    sh(
                        label : 'Run frontend tests',
                        script: 'npm run test:cov calculator'
                    )
                    sh(
                        label : 'Show coverage',
                        script: 'npm run coverage'
                    )
                }
            }
        }
    }
}