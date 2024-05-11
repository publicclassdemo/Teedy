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
            archiveArtifacts artifacts: 'docs-core/target/**/pmd.html', fingerprint: true
            archiveArtifacts artifacts: 'docs-core/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: 'docs-core/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: 'docs-core/target/surefire-report', fingerprint: true
            archiveArtifacts artifacts: 'docs-web/target/**/pmd.html', fingerprint: true
            archiveArtifacts artifacts: 'docs-web/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: 'docs-web/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: 'docs-web/target/surefire-report', fingerprint: true
            archiveArtifacts artifacts: 'docs-web-common/target/**/pmd.html', fingerprint: true
            archiveArtifacts artifacts: 'docs-web-common/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: 'docs-web-common/target/surefire-report/TEST-com.sismics.docs.rest.util.TestValidationUtil.xml', fingerprint: true
        }
    }
}
