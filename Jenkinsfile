node {

    stage("Git Clone"){

        git credentialsId: 'GIT_CREDENTIALS', url: 'https://github.com/mahouESPRIT/spring-jenkins-test.git'
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

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u ayoubmahou -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  ayoubmahou/jhooq-docker-demo:jhooq-docker-demo'
    }

    
    }

}

