pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage ('checkout') {
            steps {
                git branch: 'features/greg', credentialsId: '859d834a-84f4-42a3-93d0-9398275dba78', url: 'https://github.com/kraiem12/ProjetCD-GRIM.git'
            }
        }
//        stage ('dependances') {
//            steps {
//                sh 'todo' 
//        }
//            }

        stage ('parallel') {
            parallel {
                stage('junit tests') {
                    steps {
                        sh 'mvn -f pom.xml -s settings.xml test'
                    }
                }
                stage('pmd tests') {
                    steps {
                        sh 'mvn pmd:pmd'
                    }
                }
            }
        }
    
        stage('deploy on nexus') {
            steps {
                sh 'mvn -f pom.xml -s settings.xml deploy'
            }
        }
    }
}
