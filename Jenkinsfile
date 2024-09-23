node {
    // Parameters definition
    properties([
        parameters([
            string(name: 'DOCKERTAG', defaultValue: 'default_value', description: 'This is a parameter passed from another job')
        ])
    ])
    
    stage('Clone repository') {
      checkout scm
    }
    stage('Read Parameter') {
        echo "Received parameter: ${params.DOCKERTAG}"
    }
    
    stage('Update Git') {
        // steps {
            echo "Received parameter: ${params.DOCKERTAG}"
            withCredentials([gitUsernamePassword(credentialsId: 'helios-jenkins-new', gitToolName: 'Default')]) {
                sh "git config --global user.name hheelliiooss-admin"
                sh "git config --global user.email developerteamhelios@gmail.com"
                
                sh "cat deployment.yaml"
                sh "sed -i 's+octovianus/hms-s3-front.*+octovianus/hms-s3-front:${params.DOCKERTAG}+g' deployment.yaml"
                
                sh "cat deployment.yaml"
                sh "git add ."
                sh "git commit -m 'Done by Jenkins job update-deployment: ${params.DOCKERTAG}'"
                sh "git push https://github.com/hheelliiooss-admin/hms-s3-front-manifest.git HEAD:main"
                
            }
            
        // }
        
    }
}
