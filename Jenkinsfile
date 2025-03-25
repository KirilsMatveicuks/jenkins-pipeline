pipeline {
    agent any  

    stages {
        stage('install-pip-deps') {
            steps {
                script {
                    echo "Installing dependencies..."
                    sh 'git clone https://github.com/mtararujs/python-greetings'
                    sh 'ls python-greetings'
                    sh 'pip3 install -r python-greetings/requirements.txt'
                }
            }
        }

        stage('deploy-to-dev') {
            steps {
                script {
                    deploy('dev', 7001)
                }
            }
        }

        stage('tests-on-dev') {
            steps {
                script {
                    run_tests('dev')
                }
            }
        }

        stage('deploy-to-staging') {
            steps {
                script {
                    deploy('staging', 7002)
                }
            }
        }

        stage('tests-on-staging') {
            steps {
                script {
                    run_tests('staging')
                }
            }
        }

        stage('deploy-to-preprod') {
            steps {
                script {
                    deploy('preprod', 7003)
                }
            }
        }

        stage('tests-on-preprod') {
            steps {
                script {
                    run_tests('preprod')
                }
            }
        }

        stage('deploy-to-prod') {
            steps {
                script {
                    deploy('prod', 7004)
                }
            }
        }

        stage('tests-on-prod') {
            steps {
                script {
                    run_tests('prod')
                }
            }
        }
    }
}

def deploy(environment, port) {
    echo "Deploying to ${environment}..."
    sh """
        git clone https://github.com/mtararujs/python-greetings
        pm2 delete greetings-app-${environment} || true
        pm2 start python-greetings/app.py --name greetings-app-${environment} -- --port ${port}
    """
}

def run_tests(environment) {
    echo "Running tests on ${environment}..."
    sh """
        git clone https://github.com/mtararujs/course-js-api-framework
        cd course-js-api-framework && npm install
        cd course-js-api-framework && npm run greetings greetings_${environment}
    """
}
