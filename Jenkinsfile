pipeline {
    /*if you want to execute on specific node use:
        agent { label 'mac-mini-slave-local' }
    */
    agent any
    
//     parameters {
//         // the default choice for commit-triggered builds is the first item in the choices list
//         choice(name: 'buildType', choices: ['Scan_only', 'Debug_firebaseDistribution', 'Release_AppStore_Testflight'],
//                description: 'The build types')
//         booleanParam(name: 'Push_To_Remote', defaultValue: false, description: 'Toggle to push changes back to remote(check for repo permission on this)')
//         }
    environment {
        PATH = "$HOME/.fastlane/bin:" +
                "$HOME/.rvm/gems/ruby-2.5.3/bin:" +
                "$HOME/.rvm/gems/ruby-2.5.3@global/bin:" +
                "$HOME/.rvm/rubies/ruby-2.5.3/bin:" +
                "/usr/local/bin:" +
                "$PATH"
        ANDROID_HOME = "$HOME/Library/Android/sdk"
    }

    stages {
//         stage('Print Selected Values') {
//             steps {
//                 echo 'Selected Values are: \n'
//                 echo params.buildType
//                 echo 'environment variables are: \n'
//                 echo env.BUILD_TYPE
//             }
//         }
        
        stage('Deploy to Firebase') {
            steps {
                
                script {
                    withCredentials([file(credentialsId: 'firebase_key', variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
                        sh """
                        fastlane firebaseDistribution
                        """
                    }
                    
                }
            }
        }
    }
}
