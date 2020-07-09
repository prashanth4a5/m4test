pipeline {
  agent any
 parameters {
  choice choices: ['DEV','TEST', 'UAT', 'PROD'], description: 'Select the Environment to Deploy ', name: 'DEPLOY_TO'
   
}
  stages {
    stage('build-parent-pom-dev') {
      when {
        not {
        branch 'master'
        }
      }
      steps {
        echo 'Hi BUILD'
        echo DEPLOY_TO
        build(job: 'ppom/dev', propagate: true, wait: true)
      }
    }
    stage('Deploying to DEV') {
      when {
        not {
        branch 'master'
       
        }
        
         expression {DEPLOY_TO ==  null || DEPLOY_TO ==  'DEV' }
      }
      steps {
      echo 'Hi DEV'
       }
    }
    stage('build-parent-pom-master') {
      when {
        branch 'master'
       
        }
      steps {
        script {
                    env.TEST_VARIABLE = "some test value"
                }
        echo "TEST_VARIABLE = ${env.TEST_VARIABLE}"
        echo "The build number is ${env.BUILD_NUMBER}"
        build(job: 'ppom/master', propagate: true, wait: true)
      }
    }
    stage('Deploying to TEST') {
      when {
        branch 'master'
        expression { env.BUILD_NUMBER !=  1 || DEPLOY_TO ==  'TEST' }
      }
      steps {
        echo 'Hi TEST'
        }
    }
   stage('Deploying to UAT') {
      when {
        branch 'master'
        expression { DEPLOY_TO ==  'UAT' }
      }
      steps {
        echo 'Hi UAT'
        }
    }
  }
  options {
    timeout(time: 1, unit: 'HOURS')
  }
  post {
        always {
            echo 'I will always say Hello again!'
           
        }
  }
}
