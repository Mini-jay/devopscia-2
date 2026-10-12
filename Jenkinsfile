
pipeline {
    agent any

    environment {
        MAVEN_HOME = 'C:\\Users\\SNUC\\Downloads\\apache-maven-3.10.0-bin\\apache-maven-3.10.0'
        PROJECT_DIR = 'C:\\Users\\SNUC\\Downloads\\Student-Starter\\Student-Starter'
    }

    stages {
        stage('Prepare Source') {
            steps {
                bat '''
                    if not exist "%PROJECT_DIR%\\pom.xml" exit /b 1
                    robocopy "%PROJECT_DIR%" "%WORKSPACE%" /E /XD .git target /XF Jenkinsfile
                    if errorlevel 8 exit /b 1
                    exit /b 0
                '''
            }
        }

        stage('Build and Test') {
            steps {
                bat '"%MAVEN_HOME%\\bin\\mvn.cmd" clean test'
            }
        }

        stage('Package') {
            steps {
                bat '"%MAVEN_HOME%\\bin\\mvn.cmd" package'
            }
        }
    }

    post {
        always {
            junit testResults: 'course-registration-app/target/surefire-reports/TEST-*.xml',
                  allowEmptyResults: true
        }

        success {
            archiveArtifacts artifacts: 'course-registration-app/target/*.jar',
                             fingerprint: true
        }
    }
}
