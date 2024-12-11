pipeline {
    agent any
    tools {
        maven "maven3"
        jdk "jdk17"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'Abdulll40'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL-REPO = 'vpro-maven-central'
        NEXUSIP = '192.168.33'
        NEXUS_PORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexus-cred'
    }

    stages {
        stage{'Build'}{
            steps {
                sh 'mvn -s sethings.xml -Dskiptests install'
            }
        }
    }
}