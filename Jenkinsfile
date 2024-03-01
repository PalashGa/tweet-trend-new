pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
    }
    stages {
        stage("Build") {
            steps {
                echo "-----------Build started---------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "-----------Build completed--------"
            }
        }
        stage("Test") {
            steps {
                echo "------------Unit test started-------"
                sh 'mvn surefire-report:report'
                echo "----------Unit test completed-------"
            }
        }
        
    }
}

