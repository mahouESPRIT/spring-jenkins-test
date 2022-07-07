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
    stage('Orchestrate')
    {
        sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
        sh 'chmod u+x ./kubectl'  
        sh './kubectl get pods'
        sh 'kubectl apply -f k8s-spring-boot-deployment.yaml'    
    }

}





