pipeline {
    agent any
   
    stages {

        stage('Clone repository') {
            steps {
            checkout scm
            }
        }
		
        
        stage('master - 5.5-mysql') {
            when { branch 'master'}
            steps {
                script {
                    def tag = "5.5-mysql"
                    app1 = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app1.push("${tag}")
                    app1.push("${tag}-${env.BUILD_NUMBER}")
                    }
                }
            }
            when { not {branch 'master'} }
            steps {
                script {
                    def tag = "5.5-mysql"
                    app4 = docker.build("anvibo/nginx-php", "-f ${tag}/Dockerfile --pull .")

                    withDockerRegistry([url: "", credentialsId: "dockerhub-anvibo"]) {
                    app4.push("${tag}-${env.BRANCH_NAME}")
                    app4.push("${tag}-${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    }
                }
            }
        }

       /* stage('branch - 5.5-mysql') {
           
        }*/

        stage('master - 7.2') {
            when { branch 'master'}
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

        stage('branch - 7.2') {
            when { not {branch 'master'} }
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

        stage('master - 7.2-mysql') {
            when { branch 'master'}
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

        stage('branch - 7.2-mysql') {
            when { not {branch 'master'} }
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
