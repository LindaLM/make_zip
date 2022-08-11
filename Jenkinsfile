pipeline {
    agent any
    
    parameters {
        string defaultValue: 'file.xml', name: 'M', trim: true
        string defaultValue: 'file2.xml', name: 'P_M', trim: true
        string defaultValue: 'id', name: 'A_ID', trim: true
        string defaultValue: 'v0.0.0', name: 'R_VER',  trim: true
        booleanParam defaultValue: true, name: 'DEPLOY_N'
        booleanParam defaultValue: true, name: 'DEPLOY_C'
        booleanParam defaultValue: true, name: 'DEPLOY_D'
        booleanParam defaultValue: true, name: 'MERGE'
        choice choices: ['aaaa', 'bbbb'], name: 'VERSION'
        choice choices: ['0.1', '2.2'], name: 'LINE'
        booleanParam defaultValue: true, name: 'TXT'
        booleanParam defaultValue: true, name: 'B4K'
    }
    options {
        ansiColor('xterm')
    }
    environment {
        RED='\033[0;31m'
        GREEN='\033[0;32m'
        NC='\033[0m'
    }
    
    stages {
        stage("Clean Workspace") {
            steps {
                cleanWs()
                echo "${RED}Workspace cleaned ${NC}"
            }
        }
        stage('Prepare Workspace') {
            options { timeout(1) }
            steps {
                git branch: "main", 
                url: 'https://github.com/LindaLM/make_zip.git'
            }
        }
        stage ("Set") {
            steps {
                echo "${LINE}_${VERSION}"
                sh 'sleep 9s'
                echo "${RED}Set ${NC}"
            }
        }
        stage ("Build") {
            options { timeout(time: 3, unit: 'HOURS') }
            steps{
                echo "${RED}Build${NC}"
            }
        }
        stage ("Test_1") {
            options { timeout(time: 12, unit: 'SECONDS') }
            steps {
                echo "${RED}Testing ... ${NC}"
                sh 'sleep 10s'
                echo "${RED}Tested${NC}"
            }
        }
        stage("Analysis") {
            options { timeout(time: 3, unit: "HOURS") }
            steps {
                echo "${RED}Analysis done${NC}"
            }
        }
        stage("List"){
            options { timeout(time: 1, unit: "HOURS") }
            steps {
                echo "${RED}List generated${NC}"
            }
        }

        stage("Archive") {
            options{ timeout(time: 1, unit: "HOURS") }
            parallel {
                stage ("0.1") {
                    when {environment name: 'LINE', value: '0.1'}
                    steps {
                        echo "line = 0.1"
                        sh './zip_file.sh l_0.1.txt'
                        echo "${RED}archived${NC}"
                    }
                }
                stage ("2.2") {
                    when {environment name: 'LINE', value: '2.2'}
                    steps {
                        echo "line = 2.2"
                        sh './zip_file.sh l_2.2.txt'
                        echo "${RED}archived${NC}"
                    }
                }
            }
        }
        stage("Test_2") {
            options { timeout(time: 1, unit: "HOURS") }
            steps {
                input {
                    message "Please download and test zip and press PROCEED to continue: \n ${env.BUILD_URL}"
                }
                steps {
                    echo "done"
                }
            }
        }
    }
}
