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
}
