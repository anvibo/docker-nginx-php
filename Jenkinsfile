pipeline {
    agent any
    / * post {
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
    } */
    stages {

        stage('Clone repository') {
            steps {
            checkout scm
            }
        }

        stage('Build image 5.9 from master') {
            when { branch 'master' }
            steps {
                script {
                    def tag = "5.9-mysql"
                    app = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app.push("${tag}")
                    app.push("${tag}-${env.BUILD_NUMBER}")
                    }
                }
            }
        }

        stage('Build image 5.9 from branch') {
            when { not { branch 'master' } }
            steps {
                script {
                  def tag = "5.9-mysql"
                  app = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                  withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                  app.push("${tag}-${env.BRANCH_NAME}")
                  app.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                  }
                }
            }
        }

        stage('Build image 7.0 from master') {
            when { branch 'master' }
            steps {
                script {
                    def tag = "7.0"
                    app = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app.push("${tag}")
                    app.push("${tag}-${env.BUILD_NUMBER}")
                    }
                }
            }
        }

        stage('Build image 7.0 from branch') {
            when { not { branch 'master' } }
            steps {
                script {
                  def tag = "7.0"
                  app = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                  withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                  app.push("${tag}-${env.BRANCH_NAME}")
                  app.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                  }
                }
            }
        }

         stage('Build image 7.0-mysql from master') {
            when { branch 'master' }
            steps {
                script {
                    def tag = "7.0-mysql"
                    app = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app.push("${tag}")
                    app.push("${tag}-${env.BUILD_NUMBER}")
                    }
                }
            }
        }

        stage('Build image 7.0-mysql from branch') {
            when { not { branch 'master' } }
            steps {
                script {
                  def tag = "7.0-mysql"
                  app = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                  withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                  app.push("${tag}-${env.BRANCH_NAME}")
                  app.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                  }
                }
            }
        }





      }
}