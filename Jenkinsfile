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
     stage('Apply Kubernetes files') {
    withKubeConfig([credentialsId: 'kube-cred', serverUrl: 'https://192.168.59.100:8443']) {
      sh 'kubectl apply -f my-kubernetes-directory'
    }
  }





