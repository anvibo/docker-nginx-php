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

        stage('Build image 18.04 from master') {
            when { branch 'master' }
            steps {
                script {
                    app = docker.build("anvibo/nginx-php", "-f 5.9-mysql/Dockerfile .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app.push("5.9-mysql")
                    }
                }
            }
        }

        stage('Build image 18.04 from branch') {
            when { not { branch 'master' } }
            steps {
                script {
                app = docker.build("anvibo/nginx-php", "-f 5.9-mysql/Dockerfile .")

                withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                app.push("5.9-mysql-${env.BRANCH_NAME}")
                app.push("5.9-mysql")

                }
                }
            }
        }

    }
}
  