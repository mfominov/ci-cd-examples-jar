node ('dockerhost') {
    timestamps {
        ansiColor('xterm') {
            stage('Checkout') {
                checkout scm
            }

            stage ('Build & Deploy Jar') {
                docker.image('docker.art.lmru.tech/maven:3.6.0-jdk-8-slim').inside() {
                    configFileProvider([configFile(fileId: 'settings_xml', targetLocation: './settings.xml')]) {
                        sh "mvn clean deploy -s settings.xml -B"
                    }
                }
            }

            stage ('Wipe') {
                cleanWs();
            }
        }
    }
}