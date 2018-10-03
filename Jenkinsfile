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
    
  
    }
    stage('nexus uploader'){
    
   nexusArtifactUploader artifacts: [[artifactId: 'vprofile', classifier: '',
      file: '/var/lib/jenkins/workspace/nexus_test/target/vprofile-v1.war', type: 'war']],
       credentialsId: '3ba1009c-230e-4ffc-9608-f02dc46a6b01', groupId: 'dev', nexusUrl: '35.196.10.23:8081/nexus',
       nexusVersion: 'nexus2', protocol: 'http', repository: 'sample_job', version: '0.0.1'
    }
   
}
