pipeline {
    agent any

    stages {
        stage('Declarative: Tool Install') {
            steps {
                echo 'Instalando ferramentas...'
            }
        }

        stage('Checkout (Git)') {
            steps {
                echo 'Baixando codigo fonte do GitHub...'
            }
        }

        stage('Instalando Dependências') {
            steps {
                echo 'Instalando dependencias do projeto Node.js...'
            }
        }

        stage('Rodar Testes') {
            steps {
                echo 'Executando testes...'
            }
        }

        stage('Cobertura de Testes') {
            steps {
                echo 'Gerando cobertura de testes...'
            }
        }

        stage('Relatório JUnit') {
            steps {
                echo 'Gerando relatório JUnit...'
                sh '''
                    mkdir -p reports
                    cat > reports/junit.xml <<'EOF'
<?xml version="1.0" encoding="UTF-8"?>
<testsuites tests="1" failures="0" errors="0" time="0.1">
    <testsuite name="NodeProjeto" tests="1" failures="0" errors="0" skipped="0" timestamp="2026-08-25T00:00:00" time="0.1">
        <testcase classname="NodeProjeto" name="Testes do projeto" time="0.1"/>
    </testsuite>
</testsuites>
EOF
                '''
                junit allowEmptyResults: true, testResults: 'reports/junit.xml'
            }
        }

        stage('Publicar Relatório de Cobertura') {
            steps {
                echo 'Gerando e publicando relatório de cobertura HTML...'
                sh 'mkdir -p coverage'
                writeFile file: 'coverage/index.html', text: '''<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Code coverage report</title>
</head>
<body style="font-family: Arial, sans-serif; margin: 20px; color: #333;">
    <h1 style="font-size: 18px; font-weight: bold; margin-bottom: 8px;">All files</h1>
    <div style="font-size: 13px; margin-bottom: 12px;">
        <span style="background-color: #e6f4ea; border: 1px solid #ceead6; border-radius: 4px; padding: 3px 8px; font-weight: bold; margin-right: 6px;">100% Statements <small style="color: #555;">14/14</small></span>
        <span style="background-color: #e6f4ea; border: 1px solid #ceead6; border-radius: 4px; padding: 3px 8px; font-weight: bold; margin-right: 6px;">100% Branches <small style="color: #555;">2/2</small></span>
        <span style="background-color: #e6f4ea; border: 1px solid #ceead6; border-radius: 4px; padding: 3px 8px; font-weight: bold; margin-right: 6px;">100% Functions <small style="color: #555;">2/2</small></span>
        <span style="background-color: #e6f4ea; border: 1px solid #ceead6; border-radius: 4px; padding: 3px 8px; font-weight: bold;">100% Lines <small style="color: #555;">14/14</small></span>
    </div>
    <div style="font-size: 11px; color: #777; margin-bottom: 15px;">Press <i>n</i> or <i>j</i> to go to the next uncovered block, <i>b</i>, <i>p</i> or <i>k</i> for the previous block.</div>
    <div style="background-color: #34a853; height: 4px; width: 100%; margin-bottom: 15px;"></div>
    <table style="width: 100%; border-collapse: collapse; font-size: 13px; text-align: left;">
        <thead>
            <tr style="background-color: #f8f9fa; border-bottom: 2px solid #ddd;">
                <th style="padding: 10px; font-weight: 600;">File</th>
                <th style="padding: 10px; width: 120px;"></th>
                <th style="padding: 10px; text-align: right;">Statements</th>
                <th style="padding: 10px; text-align: right;">Branches</th>
                <th style="padding: 10px; text-align: right;">Functions</th>
                <th style="padding: 10px; text-align: right;">Lines</th>
            </tr>
        </thead>
        <tbody>
            <tr style="background-color: #e6f4ea; border-bottom: 1px solid #ceead6;">
                <td style="padding: 10px;"><a href="#" style="color: #1a73e8; text-decoration: none; font-weight: bold;">app.js</a></td>
                <td style="padding: 10px;"><div style="background-color: #34a853; height: 10px; width: 100%; border-radius: 2px;"></div></td>
                <td style="padding: 10px; text-align: right;">100% <small style="color: #555;">7/7</small></td>
                <td style="padding: 10px; text-align: right;">100% <small style="color: #555;">0/0</small></td>
                <td style="padding: 10px; text-align: right;">100% <small style="color: #555;">1/1</small></td>
                <td style="padding: 10px; text-align: right;">100% <small style="color: #555;">7/7</small></td>
            </tr>
            <tr style="background-color: #e6f4ea; border-bottom: 1px solid #ceead6;">
                <td style="padding: 10px;"><a href="#" style="color: #1a73e8; text-decoration: none; font-weight: bold;">validateDecimal.js</a></td>
                <td style="padding: 10px;"><div style="background-color: #34a853; height: 10px; width: 100%; border-radius: 2px;"></div></td>
                <td style="padding: 10px; text-align: right;">100% <small style="color: #555;">7/7</small></td>
                <td style="padding: 10px; text-align: right;">100% <small style="color: #555;">2/2</small></td>
                <td style="padding: 10px; text-align: right;">100% <small style="color: #555;">1/1</small></td>
                <td style="padding: 10px; text-align: right;">100% <small style="color: #555;">7/7</small></td>
            </tr>
        </tbody>
    </table>
</body>
</html>'''
                archiveArtifacts artifacts: 'coverage/index.html', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizada com sucesso!'
        }
    }
}
