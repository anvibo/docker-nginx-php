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

	stage('Build - master') {
		when { branch 'master'}
        steps {
        stage('5.9-mysql') {
            steps {
                script {
                    def tag = "5.9-mysql"
                    app1 = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app1.push("${tag}")
                    app1.push("${tag}-${env.BUILD_NUMBER}")
                    }
                }
            }
        }

        stage('7.2') {
        
            steps {
                script {
                    def tag = "7.2"
                    app2 = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app2.push("${tag}")
                    app2.push("${tag}-${env.BUILD_NUMBER}")
                    app2.push("latest")
                    }
                }
            }
        }

        stage('7.2-mysql') {
        
            steps {
                script {
                    def tag = "7.2-mysql"
                    app3 = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app3.push("${tag}")
                    app3.push("${tag}-${env.BUILD_NUMBER}")
                    }
                }
            }
        }
	}
    }

    stage('Build images and push to dockerhub - branch') {
		when { not {branch 'master'} }
        steps {
            stage('5.9-mysql') {
                steps {
                    script {
                        def tag = "5.9-mysql"
                        app4 = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                        withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                        app4.push("${tag}-${env.BRANCH_NAME}")
                        app4.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        }
                    }
                }
            }

            stage('7.2') {
            
                steps {
                    script {
                        def tag = "7.2"
                        app5 = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                        withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                        app5.push("${tag}-${env.BRANCH_NAME}")
                        app5.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        }
                    }
                }
            }

            stage('7.2-mysql') {
            
                steps {
                    script {
                    def tag = "7.2-mysql"
                    app6 = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app6.push("${tag}-${env.BRANCH_NAME}")
                    app6.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    }
                    }
                }
            }
        }
	}
      }
}
