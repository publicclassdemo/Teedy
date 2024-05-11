pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test --fail-never'
            }
        }

        stage('Generate Surefire Report') {
            steps {
                sh 'mkdir -p surefire-report'
                sh 'mvn surefire-report:report -Dsurefire.report.directory=surefire-report'
            }

        }
        stage('Generate Javadoc') {
            steps {
                sh 'mvn javadoc:jar'
            }

        }


    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/**/pmd.html', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: '**/target/surefire-report', fingerprint: true
            archiveArtifacts artifacts: '**/target/surefire-report/TEST-com.sismics.docs.rest.util.TestValidationUtil.xml', fingerprint: true
        }
    }
}
