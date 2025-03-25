pipeline {
    agent any  // Используем любой доступный агент

    stages {

        stage('install-pip-deps') {
            steps {
                echo '🔹 Устанавливаем зависимости Python...'
                sh 'git clone https://github.com/mtararujs/python-greetings app'
                sh 'cd app && pip install -r requirements.txt'
            }
        }

        stage('deploy-to-dev') {
            steps {
                echo '🚀 Деплой в DEV среду...'
                sh 'pm2 delete greetings-app-dev || true'
                sh 'pm2 start app/app.py --name greetings-app-dev -- --port 7001'
            }
        }

        stage('tests-on-dev') {
            steps {
                echo '✅ Тестируем в DEV среде...'
                sh 'git clone https://github.com/mtararujs/course-js-api-framework tests'
                sh 'cd tests && npm install'
                sh 'cd tests && npm run greetings greetings_dev'
            }
        }

        stage('deploy-to-staging') {
            steps {
                echo '🚀 Деплой в STAGING среду...'
                sh 'pm2 delete greetings-app-staging || true'
                sh 'pm2 start app/app.py --name greetings-app-staging -- --port 7002'
            }
        }

        stage('tests-on-staging') {
            steps {
                echo '✅ Тестируем в STAGING среде...'
                sh 'cd tests && npm run greetings greetings_staging'
            }
        }

        stage('deploy-to-preprod') {
            steps {
                echo '🚀 Деплой в PREPROD среду...'
                sh 'pm2 delete greetings-app-preprod || true'
                sh 'pm2 start app/app.py --name greetings-app-preprod -- --port 7003'
            }
        }

        stage('tests-on-preprod') {
            steps {
                echo '✅ Тестируем в PREPROD среде...'
                sh 'cd tests && npm run greetings greetings_preprod'
            }
        }

        stage('deploy-to-prod') {
            steps {
                echo '🚀 Деплой в PROD среду...'
                sh 'pm2 delete greetings-app-prod || true'
                sh 'pm2 start app/app.py --name greetings-app-prod -- --port 7004'
            }
        }

        stage('tests-on-prod') {
            steps {
                echo '✅ Тестируем в PROD среде...'
                sh 'cd tests && npm run greetings greetings_prod'
            }
        }
    }
}
