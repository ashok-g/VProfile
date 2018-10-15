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
  
