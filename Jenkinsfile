pipeline {
    agent any
    tools{
        maven 'maven3'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AneeshMSomayaji/Devopsss']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                
                    bat 'docker build -t aneeshmsomayaji/devops-integration .'
                
            }
        }
        stage('Push image to Hub'){
            steps{
                   bat 'docker login -u javatechie -p Madhu@0708'

}
                   bat 'docker push javatechie/devops-integration'
                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
                }
            }
        }
    }
}
