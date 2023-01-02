pipeline {
    agent any
    stages {
        stage('compile') {
                        steps {
                echo 'compiling..'
                                git branch: 'master',
                                url: "https://github.com/Mosh094/Edureka-Project.git"
                                bat label: '', script: 'mvn compile'
            }
        }
        stage('codereview-pmd') {
                        steps {
                echo 'codereview..'
                                bat label: '', script: 'mvn -P metrics pmd:pmd'
            }
                        post {
                success {
                    pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/pmd.xml', unHealthy: ''
                }
            }

        }
        stage('unit-test') {
                        steps {
                echo 'codereview..'
                                bat label: '', script: 'mvn test'
            }
                        post {
                success {
                    junit 'target/surefire-reports/*.xml'
                }
            }

        }
        stage('metric-check') {
                        steps {
                echo 'unit test..'
                                bat label: '', script: 'mvn verify'
            }
                        post {
                success {
                                jacoco(
                    execPattern: '**/target/**.exec',
                    classPattern: '**/target/classes',
                    sourcePattern: '**/src',
                    inclusionPattern: 'com/iamvickyav/**',
                    changeBuildStatus: true,
                    minimumInstructionCoverage: '30',
                    maximumInstructionCoverage: '80')
                }
            }

        }
        stage('package') {
                        steps {
                echo 'metric-check..'
                                bat label: '', script: 'mvn package'
            }

        }
    }
}
