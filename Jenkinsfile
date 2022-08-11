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
        stage ("make_zip") {
            steps {
                sh './zip_file.sh'
            }
        }
    }
}
