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
    } */
    stages {

        stage('Clone repository') {
            steps {
            checkout scm
            }
        }

	stage('Build images and push to dockerhub - master') {
		when { branch 'master'}
		parallel {
            stage('5.9-mysql') {
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

            stage('7.2') {
            
                steps {
                    script {
                        def tag = "7.2"
                        app = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                        withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                        app.push("${tag}")
                        app.push("${tag}-${env.BUILD_NUMBER}")
                        app.push("latest")
                        }
                    }
                }
            }

            stage('Build image 7.2-mysql from master') {
            
                steps {
                    script {
                        def tag = "7.2-mysql"
                        app = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                        withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                        app.push("${tag}")
                        app.push("${tag}-${env.BUILD_NUMBER}")
                        }
                    }
                }
            }
        }
	}

    stage('Build images and push to dockerhub - branch') {
		when { not {branch 'master'} }
		parallel {
            stage('5.9-mysql') {
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

            stage('7.2') {
            
                steps {
                    script {
                        def tag = "7.2"
                        app = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                        withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                        app.push("${tag}-${env.BRANCH_NAME}")
                        app.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        }
                    }
                }
            }

            stage('7.2-mysql') {
            
                steps {
                    script {
                    def tag = "7.2-mysql"
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
      }
}
