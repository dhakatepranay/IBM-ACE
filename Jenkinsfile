pipeline {
   agent any

   stages {
      stage('checkout code') {
         steps {
            git branch: 'main', 'https://github.com/dhakatepranay/IBM-ACE.git'
         }
      }
      stage('Build BAR') {
      steps {
        bat '''
          call "C:\\Program Files\\IBM\\ACE\\12.0.12.19\\server\\bin\\mqsiprofile.cmd"

          mqsicreatebar ^
           -data %workspace_test% ^
           -b test_%BUILD_NUMBER%.bar ^
           -a Test_Rest ^
        '''
      }
    }

    stage('Archive') {
      steps {
        archiveArtifacts artifacts: '*.bar'
      }
    }
  }

}
