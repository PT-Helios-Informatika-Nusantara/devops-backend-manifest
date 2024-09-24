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
            withCredentials([gitUsernamePassword(credentialsId: 'github-token-user-octohin', gitToolName: 'Default')]) {
                sh "git config --global user.name octohin"
                sh "git config --global user.email octovianus.pabubung@helios.id"
                
                sh "cat deployment.yaml"
                sh "sed -i 's+octovianus/hms-azure-backend.*+octovianus/hms-azure-backend:${params.DOCKERTAG}+g' deployment.yaml"
                
                sh "cat deployment.yaml"
                sh "git add ."
                sh "git commit -m 'Done by Jenkins job hms-backend-manifest: ${params.DOCKERTAG}'"
                sh "git push https://github.com/PT-Helios-Informatika-Nusantara/devops-backend-manifest.git HEAD:main"
                
            }
            
        // }
        
    }
}
