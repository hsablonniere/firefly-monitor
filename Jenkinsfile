node {
  stage('🚧 Checkout') {
    println("☘️" + env.BRANCH_NAME)
    checkout scm
  }
  stage('📦 Build') {
    println("🚧 building project")
    def nodeHome = tool name: 'nodejs', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
    env.PATH = "${nodeHome}/bin:${env.PATH}"
    sh "npm install"
    sh "npm test"  
  }
  stage('🚢 Check if Deploy') {
    println("☘️" + env.BRANCH_NAME)
    if(env.BRANCH_NAME.equals("master")) {
      stage('Deploy to production 🚀') {
        println("🎉 it's time to deploy to Clever-Cloud 🍾")
        //it's done automatically by Clever-Cloud
      }
    } else {
      stage('Time to test 🚧') {
        println("👷 it's time to test")
        def nodeHome = tool name: 'nodejs6103', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        env.PATH = "${nodeHome}/bin:${env.PATH}"
        
        sh "clever create -t node firefly-test-01 --org wey-yu --region par --alias firefly-test-01"
        sh "clever env set PORT 8080 --alias firefly-test-01"
        //sh "clever scale --flavor pico --alias firefly-test-01"
        
        exit 0
        ls
        
        
        //app_id=$(grep -o '"app_id": *"[^"]*"' .clever.json | grep -o '"[^"]*"$')
        //echo "APPID: $app_id"
        //git remote add clever git+ssh://git@push-par-clevercloud-customers.services.clever-cloud.com/$app_id.git
        //git push clever master
        
        // call the API
      }
    }
  }
}
