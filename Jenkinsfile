pipeline {
  agent any

  stages {

    stage('Build BAR') {
      steps {
        bat '''
          call "C:\\Program Files\\IBM\\ACE\\12.0.12.19\\server\\bin\\mqsiprofile.cmd"

          mqsicreatebar ^
            -data "%WORKSPACE%" ^
            -b CollectorNodeApp_v1.0.bar ^
            -a CollectorNodeApp ^
            -cleanBuild
        '''
      }
    }

    stage('Deploy BAR') {
      steps {
        bat '''
          call "C:\\Program Files\\IBM\\ACE\\12.0.12.19\\server\\bin\\mqsiprofile.cmd"

          mqsideploy ACE_DEV_CICD ^
            -e DEV_EG ^
            -a CollectorNodeApp_v1.0.bar
        '''

        archiveArtifacts artifacts: 'Test_Rest.bar'
      }
    }
  }
}


