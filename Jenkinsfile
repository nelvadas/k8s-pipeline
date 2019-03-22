pipeline {
    agent any
    
    tools {
            maven 'MVN'
        }
stages{
        stage('Maven Build'){            
            steps {
                container('jenkins-slave') {
                    sh """
                    mvn clean package
                    """
                }                
            }
        }
        stage('Docker Build') {
        steps {
            container('docker') {
                            sh """
                            docker build . -t dci-qa3we9tl-dtr-d9a138459d7e1789.elb.eu-west-1.amazonaws.com/admin/jenkins-server:v1 -${env.BUILD_ID}
                            docker login -u admin -p admin1234 dci-qa3we9tl-dtr-d9a138459d7e1789.elb.eu-west-1.amazonaws.com
                            docker image push dci-qa3we9tl-dtr-d9a138459d7e1789.elb.eu-west-1.amazonaws.com/admin/jenkins-server:v1-${env.BUILD_ID}
                            """
                            }
                }
        }
}
}
