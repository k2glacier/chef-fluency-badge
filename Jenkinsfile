node {
    stage('Git checkout'){
        git 'https://github.com/k2glacier/docker-demo.git'
    }
    stage('Docker Build'){
        sh 'docker build -t anandsundar/myimage:v1.0 .'    
    }
    stage('Docker push'){
        withCredentials([string(credentialsId: 'DockerHubCredential', variable: 'DHPwd')]) {
            sh "docker login -u anandsundar -p ${DHPwd}"
        }       
        sh "docker push  anandsundar/myimage:v1.0"
    }
    stage('Deploy to Staging'){
        def DOCBUILD='docker run -d --publish 8080:8080 -d anandsundar/myimage:v1.0'
        sshagent (['b9ba3cad-4e8b-40f9-b779-634347836d7b']) {
            sh "ssh -v -o StrictHostKeyChecking=no  -l cloud_user 18.217.4.37 ${DOCBUILD}"
        	}
	}
}
