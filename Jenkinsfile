node ('master') {
    withEnv(['JAVA_HOME=/devops_tools/java/jdk', 'JRE_HOME=/devops_tools/java/jre']) {
        checkout scm
        stage('Build') {
            withMaven(maven: 'M3') {
                if (isUnix()) {
                    sh 'mvn -Dmaven.test.failure.ignore clean package'
                }
                else {
                    bat 'mvn -Dmaven.test.failure.ignore clean package'
                }   
            }   
        }
        stage('Results') {
            junit '**/target/surefire-reports/TEST-*.xml'
            archive 'target/*.jar'
        }
    }
}
