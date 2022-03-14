pipeline {
    agent any
    tools {
        maven "MAVEN"
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{

//                     def mavenPom = readMavenPom file: 'pom.xml'
//                     def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot" : "simpleapp-release"
                        nexusArtifactUploader artifacts: [
                        [artifactId: 'simple-app', 
                         classifier: '',
                         file: 'target/simple-app-3.0.0-SNAPSHOT.war', 
                         type: 'war']
                        ],
                         credentialsId: 'NEXUS_CRED',
                         groupId: 'in.javahome', 
                         nexusUrl: 'http://10.73.15.109/',
                         nexusVersion: 'nexus3',
                         protocol: 'http',
                         repository: 'maven-central-repo', 
                         version: '3.0.0-SNAPSHOT'
                }
            }
        }
    }
}
