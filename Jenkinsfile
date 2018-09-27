node{
    def mvnHome
    stage('Checkout SCM'){
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/AmolBagulDevops/Maven_Desktop.git']]])
    }
    stage('Build'){
        mvnHome = tool 'M3'
        sh "'${mvnHome}'/bin/mvn clean install"
    }
    stage('Test'){
        mvnHome = tool 'M3'
        sh "'${mvnHome}'/bin/mvn test"
    }
    stage('Result'){
        junit 'target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
    }
    stage('SonarQube Analysis'){
        mvnHome = tool 'M3'
        withSonarQubeEnv('Sonar') {
            sh "'${mvnHome}'/bin/mvn sonar:sonar"
        }
    }
}
