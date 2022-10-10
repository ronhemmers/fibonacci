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
                        //.\scripts\fibonacci.sh env.NUMBER
                        //def output = bat returnStdout: true, script: ".\\scripts\\fibonacci.sh env.NUMBER"
                        def output = sh(script: ".\\scripts\\fibonacci.sh env.NUMBER", returnStdout: true).trim()
                        echo output
                    }                    
                }
            }
        }
        stage('Full path') {
            steps {
                script {
                    if(isUnix()) {
                        sh returnStdout: true, script: "${env.WORKSPACE}/scripts/fibonacci.sh ${env.NUMBER}"
                    } else {
                        def output = bat returnStdout: true, script: "${env.WORKSPACE}\\scripts\\fibonacci.sh ${env.NUMBER}"
                        echo output
                    }                   
                }
            }
        }
        stage('Change directory') {
            steps {
                script {
                    if(isUnix()) {
                        dir("${env.WORKSPACE}/scripts") {
                            sh returnStdout: true, script: "./fibonacci.sh ${env.NUMBER}"
                        }
                    } else {
                        dir("${env.WORKSPACE}/scripts") {
                            bat returnStdout: true, script: ".\\fibonacci.sh ${env.NUMBER}"
                        }
                    }                   
                }
            }
        }
    }
}
