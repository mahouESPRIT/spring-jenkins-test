node {
    stage("Git Clone"){
        git credentialsId: 'git_hub_cred', url: 'https://github.com/mahouESPRIT/spring-jenkins-test.git'
    }  
    
     stage('Gradle Build') {
       sh './gradlew build'
    }
    
    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t jhooq-docker-demo .'
        sh 'docker image list'
        sh 'docker tag jhooq-docker-demo ayoubmahou/jhooq-docker-demo:jhooq-docker-demo'
    }
    withCredentials([string(credentialsId: 'docker-cred', variable: 'PASSWORD')]) {
        sh 'docker login -u ayoubmahou -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  ayoubmahou/jhooq-docker-demo:jhooq-docker-demo'
    }
    
    stage("SSH Into k8s Server") {
        def remote = [:]
        remote.name = 'minikube'
        remote.host = '192.168.59.100'
        remote.user = 'docker'
        remote.password = 'tcuser'
        remote.allowAnyHosts = true
        
        stage('Put k8s-spring-boot-deployment.yml onto k8smaster') {
                sshPut remote: remote, from: 'k8s-spring-boot-deployment.yml', into: '.'
            } 
}
  }





