// scripted groovy


node ("new-node"){
  //node  ("") {
    def MHD = tool name: "maven3.9.0"
    def bbc = "${MHD}/bin/mvn"
    
    
    stage("1. git cloning from repo"){
        sh "echo start of git clone"
        git branch: 'main', credentialsId: 'newtomcat_cred', url: 'https://github.com/Israelbill/web-app.git'
        sh "echo end of git clone"
    }
    stage ("2. building from maven"){
        //node ("new-node")
        sh "echo start of building from maven"
        sh "${bbc} clean package"
    }
    
    stage ("3. code quality scan"){
        sh "echo start of code scanning using sonarqube"
        sh "${bbc} sonar:sonar"
        sh "echo end of code quality scan"
    }
    
        stage ("6. Approval from PM"){ 
        sh "echo start of approval from PM"
        timeout(time:3, unit:'DAYS'){
        sh "echo end of approval from PM"
    }
    }
    stage ("7. deployment to tomcat"){
      sh "echo start of deployment to tomcat"
      deploy adapters: [tomcat9(credentialsId: 'newtomcat_cred', path: '', url: 'http://44.201.197.21:9091')], contextPath: null, war: 'target/*.war'
      sh "echo end of deployment to tomcat" 
        
    }
}
