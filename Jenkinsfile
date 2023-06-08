// declarative groovy script

pipeline{
    agent { label "new-node" }
    tools{
       maven "maven3.9.0"
    }
    stages{
        stage("1. start of git clone"){
          steps{
            git branch: 'main', credentialsId: 'newtomcat_cred', url: 'https://github.com/Israelbill/web-app.git'
            sh "echo end of git clone"
        }
    }
        stage("2. building from maven"){
        steps{
        git branch: 'main', credentialsId: 'newtomcat_cred', url: 'https://github.com/Israelbill/web-app.git'
        sh "echo end of built from maven"
        }
    }
    
    stage("3. code quality check"){
        steps{
        sh "mvn sonar:sonar"
        sh "echo end of code quality check"
        }
    }
   stage("5. deployment to tomcat UAT"){
        steps{
            deploy adapters: [tomcat9(credentialsId: 'newtomcat_cred', path: '', url: 'http://44.201.197.21:9091')], contextPath: null, war: 'target/*.war'
        sh "echo end of deployment to tomcat"
        }
    }
    }
    }
