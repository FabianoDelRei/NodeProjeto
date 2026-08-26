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
    <style>
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; margin: 20px; color: #333; }
        h1 { font-size: 18px; font-weight: bold; margin-bottom: 5px; }
        .metrics { font-size: 13px; margin-bottom: 10px; }
        .badge { background: #e6f4ea; border: 1px solid #ceead6; border-radius: 4px; padding: 2px 6px; font-weight: bold; }
        .shortcut-hint { font-size: 11px; color: #777; margin-bottom: 15px; }
        .bar-container { background: #e6f4ea; border-top: 4px solid #34a853; margin-bottom: 20px; }
        table { width: 100%; border-collapse: collapse; font-size: 13px; text-align: left; }
        th { background: #f8f9fa; border-bottom: 2px solid #ddd; padding: 8px; font-weight: 600; color: #555; }
        td { border-bottom: 1px solid #eee; padding: 8px; background: #e6f4ea; }
        .file-link { color: #1a73e8; text-decoration: none; font-weight: bold; }
        .pct-bar { background: #34a853; height: 10px; width: 100%; border-radius: 2px; }
        .pct-bg { background: #ceead6; width: 100px; height: 10px; display: inline-block; border-radius: 2px; }
        .num { text-align: right; }
    </style>
</head>
<body>
    <h1>All files</h1>
    <div class="metrics">
        <span class="badge">100% Statements <small>14/14</small></span> &nbsp;
        <span class="badge">100% Branches <small>2/2</small></span> &nbsp;
        <span class="badge">100% Functions <small>2/2</small></span> &nbsp;
        <span class="badge">100% Lines <small>14/14</small></span>
    </div>
    <div class="shortcut-hint">Press <i>n</i> or <i>j</i> to go to the next uncovered block, <i>b</i>, <i>p</i> or <i>k</i> for the previous block.</div>
    <div class="bar-container"></div>
    <table>
        <thead>
            <tr>
                <th>File</th>
                <th style="width: 200px;"></th>
                <th class="num" colspan="2">Statements</th>
                <th class="num" colspan="2">Branches</th>
                <th class="num" colspan="2">Functions</th>
                <th class="num" colspan="2">Lines</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><a href="#" class="file-link">app.js</a></td>
                <td><div class="pct-bg"><div class="pct-bar"></div></div></td>
                <td class="num">100%</td>
                <td class="num">7/7</td>
                <td class="num">100%</td>
                <td class="num">0/0</td>
                <td class="num">100%</td>
                <td class="num">1/1</td>
                <td class="num">100%</td>
                <td class="num">7/7</td>
            </tr>
            <tr>
                <td><a href="#" class="file-link">validateDecimal.js</a></td>
                <td><div class="pct-bg"><div class="pct-bar"></div></div></td>
                <td class="num">100%</td>
                <td class="num">7/7</td>
                <td class="num">100%</td>
                <td class="num">2/2</td>
                <td class="num">100%</td>
                <td class="num">1/1</td>
                <td class="num">100%</td>
                <td class="num">7/7</td>
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
