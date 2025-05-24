node {
   stage('Fetch changes') {
      git 'https://github.com/gouravpandey009/Java-Microservices-Integration-Platform.git'
   }
   stage('Build images') {
      sh "./package-projects.sh"
   }
   stage('Deploy ECS') {
      sh "./aws-deploy.sh"
   }
}
