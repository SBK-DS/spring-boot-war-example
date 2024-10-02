pipeline{
    agent any
    tools {
        maven 'Maven'
        jdk 'JAVA_JDK'
    }
    environment {
        JAVA_HOME = "${tool 'JAVA_JDK'}" 
        PATH = "${JAVA_HOME}/bin:${env.PATH}" 
    }
    stages{
        stage("Test"){
            steps{
                // mvn test
                bat '''
                    echo "test"
                    echo "JAVA_HOME=%JAVA_HOME%"
                    mvn test
                '''
            }
        }
        stage("Build"){
            steps{
                // mvn package
                bat '''
                    echo "========executing A========"
                    mvn package
                '''
            }
        }
        stage("Deploy on Test"){
            steps{
                bat '''
                    echo "========executing A========"
                    deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://192.168.56.101:8082')], contextPath: '/app', war: '**/*.war'
                '''
            }
        }
        stage("Deploy on Production"){
            steps{
                bat '''
                    echo "========executing A========"
                    deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://192.168.56.102:8082')], contextPath: '/app', war: '**/*.war'
                '''
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
