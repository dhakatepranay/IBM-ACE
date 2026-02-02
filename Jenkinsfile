pipeline {
  agent any

  stages {

    stage('Build BAR') {
      steps {
        bat '''
          call "C:\\Program Files\\IBM\\ACE\\12.0.12.19\\server\\bin\\mqsiprofile.cmd"

          mqsicreatebar ^
            -data "%WORKSPACE%" ^
            -b Test_Rest.bar ^
            -a Test_Rest ^
            -cleanBuild
        '''
      }
    }

    stage('Deploy BAR') {
      steps {
        bat '''
          call "C:\\Program Files\\IBM\\ACE\\12.0.12.19\\server\\bin\\mqsiprofile.cmd"

          mqsideploy ACE_TEST ^
            -e default ^
            -a Test_Rest.bar
        '''

        archiveArtifacts artifacts: 'Test_Rest.bar'
      }
    }
  }
}
