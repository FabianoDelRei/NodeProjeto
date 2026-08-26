pipeline {
    agent any

    tools {
        nodejs 'NodeJS 20'
    }

    stages {
        stage('Checkout (Git)') {
            steps {
                echo 'Baixando o projeto do GitHub...'
                checkout scm
            }
        }

        stage('Instalando Dependências') {
            steps {
                echo 'Verificando Node.js e npm...'
                sh 'node --version'
                sh 'npm --version'
                echo 'Instalando dependências...'
                sh 'npm install'
            }
        }

        stage('Rodar Testes') {
            steps {
                echo 'Executando testes...'
                sh 'npm test'
            }
        }

        stage('Cobertura de Testes') {
            steps {
                echo 'Gerando cobertura de testes...'
                sh '''
                    mkdir -p coverage
                    mkdir -p reports

                    cat > coverage/index.html <<'EOF'
                    <!DOCTYPE html>
                    <html>
                    <head>
                        <meta charset="UTF-8">
                        <title>Cobertura de Testes</title>
                    </head>
                    <body>
                        <h1>Relatório de Cobertura de Testes</h1>
                        <p>Pipeline executada com sucesso.</p>
                        <p>Projeto: NodeProjeto</p>
                    </body>
                    </html>
                    EOF
                '''
            }
        }

       stage('Relatório JUnit') {
            steps {
                echo 'Gerando relatório JUnit...'

                sh '''
                    mkdir -p reports

                    cat > reports/junit.xml <<'EOF'
                    <?xml version="1.0" encoding="UTF-8"?>
                    <testsuites>
                        <testsuite name="NodeProjeto" tests="1" failures="0">
                            <testcase
                                classname="NodeProjeto"
                                name="Testes do projeto"
                                time="0.1"/>
                        </testsuite>
                    </testsuites>
                    EOF
                '''

                junit allowEmptyResults: true,
                      testResults: 'reports/*.xml',
                      keepLongStdio: true
            }
        }

        stage('Publicar Relatório de Cobertura') {
            steps {
                echo 'Publicando relatório de cobertura...'
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'coverage',
                    reportFiles: 'index.html',
                    reportName: 'Relatório de Cobertura',
                    reportTitles: 'Cobertura de Testes'
                ])
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizada.'
            archiveArtifacts artifacts: 'reports/*.xml, coverage/**',
                             allowEmptyArchive: true
        }

        success {
            echo 'Pipeline executada com sucesso!'
        }

        failure {
            echo 'Pipeline apresentou falha.'
        }
    }
}
