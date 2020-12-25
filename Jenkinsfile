pipeline {
   agent any

   stages {
      stage('pull code') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'b8ed4de7-56e7-48e3-a001-7fd5edec5a17', url: 'git@github.com:youdong123/ansible.git']]])
         }
      }
      stage('code checking') {
         steps {

            script {
                 //引入SonarQubeScanner工具
                scannerHome = tool 'sonar-scanner'
            }
            //引入SonarQube的服务器环境
            withSonarQubeEnv('sonarqube') {
                sh "${scannerHome}/bin/sonar-scanner"
            }
         }
      }
      stage('build project') {
         steps {
            sh 'mvn  -version '
         }
      }
      stage('publish project') {
         steps {
         sh "echo "It is a test""
         }
      }
   }
   post {
         always {
            emailext(
               subject: '构建通知：${PROJECT_NAME} - Build # ${BUILD_NUMBER} - ${BUILD_STATUS}!',
               body: '${FILE,path="email.html"}',
               to: '1014671449@qq.com'
            )
         }
   }
}
