node() {
    // some block
   stage('SCM Checkout'){
     git 'https://github.com/ashok-g/VProfile.git'
   }
   stage('Compile-Package'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
   }
    
    
    stage('SonarQube Analysis') {
        def mvnHome =  tool name: 'maven-3', type: 'maven'
        withSonarQubeEnv('sonar-6') { 
        sh "${mvnHome}/bin/mvn sonar:sonar"
    }
    
    
    
    stage('nexus uploader'){
    
    nexusArtifactUploader artifacts: [[artifactId: 'myweb',
    classifier: '', file: '/var/lib/jenkins/workspace/vpro-test/target/myweb-0.0.1.war',
    type: 'war']], credentialsId: 'f3390c6a-2656-4419-a68d-ddc7ebd8a426',
    groupId: 'dev', nexusUrl: '34.218.209.217:8081/nexus', nexusVersion: 'nexus2',
    protocol: 'http', repository: 'test_repo', version: '0.0.1'

    }
}
