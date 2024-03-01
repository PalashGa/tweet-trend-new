def registry = 'https://sourabh77.jfrog.io/'
def imageName = 'sourabh77.jfrog.io/valaxy-docker-local/ttrend'
def version   = '2.1.2'
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
        

        stage(" Docker Build ") {
          steps {
            script {
               echo '<--------------- Docker Build Started --------------->'
               app = docker.build(imageName+":"+version)
               echo '<--------------- Docker Build Ends --------------->'
            }
          }
        }

        stage (" Docker Publish "){
            steps {
                script {
                   echo '<--------------- Docker Publish Started --------------->'  
                    docker.withRegistry(registry, 'artifact-cred'){
                        app.push()
                    }    
                   echo '<--------------- Docker Publish Ended --------------->'  
                }
            }
        }
    }
}

