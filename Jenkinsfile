node {
    stage('Clone repository') {
        //deleteDir() // Delete workspace directory for cleanup
        checkout([
            $class: 'GitSCM',
            branches: [[name: BRANCH_NAME]],
            extensions: [[$class: 'CloneOption', noTags: false]],
            userRemoteConfigs: [[credentialsId: 'f1602c25-1e78-40aa-98de-3a7b678344ce', url: 'https://github.com/Rezwaan/rails-kube-demo.git']]])
        }
    stage('Build image') {
        app = docker.build("asia.gcr.io/brave-scanner-234908/rails-kube-demo_app")
    }
    stage('Push image') {
    docker.withRegistry('https://asia.gcr.io', 'gcr:pace-config-updated') {
        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
    }
    }

    stage('Deploy App') {
    sh("kubectl apply -f ./kube/web-deployment.yml")
    //sh("kubectl get pods")
    }
}
