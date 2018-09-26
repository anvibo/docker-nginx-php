pipeline {
    agent any
    /* post {
      failure {
        updateGitlabCommitStatus name: 'build', state: 'failed'
      }
      success {
        updateGitlabCommitStatus name: 'build', state: 'success'
      }
    }
     options {
      gitLabConnection('gitlab')
    }
    triggers {
        gitlab(triggerOnPush: true, triggerOnMergeRequest: true, branchFilterType: 'All')
    }*/

    stages {

        stage('Clone repository') {
            steps {
            checkout scm
            }
        }

        stage('Build image: 5.9-mysql') {
            steps {
                script {
                    app = docker.build("anvibo/nginx-php", "-f 5.9-mysql/Dockerfile .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app.push("5.9-mysql")
                    app.push("5.9-mysql-${env.BUILD_NUMBER}")
                    app.push("5.9-mysql-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    }
                }
            }
        }
    }
}
  