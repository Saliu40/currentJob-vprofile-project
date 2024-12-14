def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger',
    'UNSTABLE': 'warning'
]

pipeline {
    agent any
    tools {
        maven "maven3"
        jdk "jdk17"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '192.168.33.10'
        NEXUSPORT = '8081'
        SONARSCANNER = 'sonar-scanner'
        SONARSERVER = 'sonar-server'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Build successful. Archiving artifacts."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Test') {
            steps {
                sh 'mvn -s settings.xml test'
            }
        }

        stage('Checkstyle Analysis') {
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }

        stage('Sonar Analysis') {
            environment {
                scannerHome = tool "${SONARSCANNER}"
            }
            steps {
                withSonarQubeEnv("${SONARSERVER}") {
                    sh '''
                    ${scannerHome}/bin/sonar-scanner \
                    -Dsonar.projectKey=vprofile \
                    -Dsonar.projectName="vprofile" \
                    -Dsonar.projectVersion=1.0 \
                    -Dsonar.sources=src/ \
                    -Dsonar.java.binaries=target/classes \
                    -Dsonar.junit.reportsPath=target/surefire-reports/ \
                    -Dsonar.jacoco.reportPath=target/jacoco.exec \
                    -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml
                    '''
                }
            }
        }

        stage('Upload Artifact') {
            steps {
                // Optional: Debugging step to ensure artifact exists
                sh 'ls -l target'

                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "${NEXUSIP}:${NEXUSPORT}",
                    groupId: 'QA',
                    version: "${env.BUILD_NUMBER}",
                    repository: "${RELEASE_REPO}",
                    credentialsId: 'nexus-cred',
                    artifacts: [
                        [artifactId: 'vproapp',
                            classifier: '',
                            file: 'target/vprofile-v2.war',
                            type: 'war']
                    ]
                )
            }
        }
    }

    post {
        always {
            echo "Sending Slack Notification."
            script {
                def color = COLOR_MAP.get(currentBuild.currentResult, 'warning') // Default to 'warning' for unknown results
                slackSend(
                    channel: '#jenkins',
                    color: color,
                    message: """
                    *${currentBuild.currentResult}*: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}
                    More info: ${env.BUILD_URL}
                    """
                )
            }
        }
    }
}
