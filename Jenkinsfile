pipeline {
    agent any
    parameters {
        choice(name: 'NUMBER',
            choices: [10,20,30,40,50,60,70,80,90],
            description: 'Select the value for F(n) for the Fibonnai sequence.')
    }
    options {
        buildDiscarder(logRotator(daysToKeepStr: '10', numToKeepStr: '10'))
        timeout(time: 12, unit: 'HOURS')
        timestamps()
    }
    triggers {
        cron '@midnight'
    }
    stages {
        stage('Make executable') {
            steps {
                script {
                    if(isUnix()) {
                        sh returnStdout: true, script: "chmod +x ./scripts/fibonacci.sh"
                        echo "UNIX SYSTEM!"
                    } else {
                        echo "WINDOWS SYSTEM!"
                    }                    
                }
            }
        }
        stage('Relative path') {
            steps {
                script {
                    if(isUnix()) {
                        sh returnStdout: true, script: "./scripts/fibonacci.sh ${env.NUMBER}"
                    } else {
                        start cmd.exe /c ./scripts/fibonacci.sh env.NUMBER
                        //bat returnStdout: true, script: "dir .\scripts\fibonacci.sh env.NUMBER"
                    }                    
                }
            }
        }
        //stage('Full path') {
        //    steps {
        //        script {
        //            ${env.WORKSPACE}/scripts/fibonacci.sh ${env.NUMBER}"
        //        }
        //    }
        //}
        //stage('Change directory') {
        //    steps {
        //        script {
        //            dir("${env.WORKSPACE}/scripts"){
        //                ./fibonacci.sh ${env.NUMBER}"
        //            }
        //        }
        //    }
        //}
    }
}
