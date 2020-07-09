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
        echo "${BUILD_ID}"
        }
      steps {
        build(job: 'ppom/master', propagate: true, wait: true)
      }
    }
    stage('Deploying to TEST') {
      when {
        branch 'master'
        expression { BUILD_ID ==  '' || DEPLOY_TO ==  'TEST' }
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
