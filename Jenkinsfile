pipeline {
   agent any

   stages {
      stage('checkout code') {
         steps {
            deleteDir()
            git 'https://github.com/dhakatepranay/IBM-ACE.git'
         }
      }
      stage('build bar') {
        steps {
        bat label: '', script: '''
echo off
set projectName=Test_Rest
"C:\\Program Files\\IBM\\ACE\\12.0.12.19\\server\\bin\\mqsicreatebar.exe" -data . -b %projectName%.bar -a %projectName% -cleanBuild
'''
}
      }
      stage('deploy bar') {
 steps {
 bat label: '', script: '''
echo off
set workspace=%cd%
cd C:\\Program Files\\IBM\\ACE\\12.0.12.19\\server\\bin\\
call .\\mqsiprofile.cmd
cd %workspace%
mqsideploy ACE_TEST -e default -a test.bar
'''

archiveArtifacts 'test.bar'
}
 }
   }
}
