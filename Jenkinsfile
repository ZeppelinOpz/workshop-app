podTemplate(containers: [                                      
                    containerTemplate(name: 'maven', image: 'maven:3.6.0-jdk-11-slim', command: 'cat', ttyEnabled: true)                         
            ],
            volumes: [
                    hostPathVolume(hostPath: '/maven', mountPath: '/root/.m2')                    
            ]) 
{
    node() {
        properties([disableConcurrentBuilds()])
        try{
        stage('Checkout') {
            checkout scm
        }
        stage('UnitTest') {
            if(env.BRANCH_NAME == "master") {
                container('maven') {
                    sh 'unset MAVEN_CONFIG && ./mvnw test'
                }
            }
        }
        stage('Build package') {
            container('maven') {
                sh 'unset MAVEN_CONFIG && ./mvnw package -DskipTests'
            }
        }
        }
        finally {
        }
    }
}
