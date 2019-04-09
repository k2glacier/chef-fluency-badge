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
    stage('Deploy to staging'){
        def DOCBUILD='docker run -d --publish 8080:8080 -d anandsundar/myimage:v1.0'
        sshagent (['3951a54a-e4b0-495f-8b79-dc5b96204f82']) {
            sh "ssh -v -o StrictHostKeyChecking=no  -l cloud_user 18.222.131.208 ${DOCBUILD}"
        	}
	}
}
