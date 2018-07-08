pipeline {
    agent any
    
    parameters {
        string(name: 'tomcat_dev', defaultValue: '18.232.137.131', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: '34.205.246.165', description: 'Production Server')
    }

    triggers {
        pollSCM('* * * * *')
    }

    stage ('Deployments'){
        parallel{
            stage ('Deploy to Staging'){
                steps {
                    sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"
                }
            }

            stage ("Deploy to Production"){
                steps {
                    sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat/webapps"
                }
            }
        }
    }
}