def groovyScript
def os

pipeline {
    agent any
    parameters {
        booleanParam(name: "RELEASE", defaultValue: false)
    }
    stages {
        stage("Init") {
            steps {
                script {
                    groovyScript = load "build.groovy"
                    os = groovyScript.findOS()
                    echo 'Building the application...'
                }
            }
        }
        stage("Build") {
            parallel {
                stage("Debug") {
                    when { expression { !params.RELEASE } }
                    steps {
                        script {
                            // If operating system is macOS
                            if(os.equal("macOS")) {
                            sh 'chmod +x build.sh'
                            sh 'build.sh Debug'
                            archiveArtifacts artifacts: 'build/macOS/Debug/*', fingerprint: true
                            }  else if(os.equal("Windows")) {
                                // Perform Windows related build task
                            } else {
                                // Perform Linux related build task
                            }
                        }
                    }
                }
                stage("Release") {
                    when { expression { params.RELEASE } }
                    steps {
                        script {
                            // If operating system is macOS
                            if(os.equal("macOS")) {
                            sh 'chmod +x build.sh'
                            sh 'build.sh Release'
                            archiveArtifacts artifacts: 'build/macOS/Release/*', fingerprint: true
                            }  else if(os.equal("Windows")) {
                                // Perform Windows related build task
                            } else {
                                // Perform Linux related build task
                            }
                        }
                    }
                }
            }
        }
        stage("Test") {
            steps {
                script {
                    echo 'Running the application...'
                    // If operating system is macOS
                    if(os.equal("macOS")) {
                        sh 'chmod +x run.sh'
                        sh 'run.sh'
                    } else if(os.equal("Windows")) {
                        // Perform Windows related test task
                    } else {
                        // Perform Linux related test task
                    }
                }
            }
        }
    }
}