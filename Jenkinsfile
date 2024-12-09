pipeline{
    agent{
      // run this task on node machine where label match
        label "node"
    }
    stages{
        stage("test"){
            steps{
               //check maven installed or not
               sh 'mvn --version'
               //for test run command > mvn test
               sh 'mvn test'
                echo "========executing A========"
            }    
        }
        stage("build"){
            steps{
               //for build >> mvn package
               sh 'mvn package'
                echo "========executing A========"
            }    
        }
        stage("deploy_on_test"){
            steps{
               //for deploy on container >> container of plugins
                deploy adapters: [tomcat9(credentialsId: 'ec8ed907-6f26-40bc-be33-e5bfe9dc91ed', path: '', url: 'http://192.168.8.247:8081')], contextPath: '/app', war: '**/*.war'
            }    
        }
        stage("Deploy_on_prod"){
            steps{
               //for deploy on container >> container of plugins
               deploy adapters: [tomcat9(credentialsId: 'ec8ed907-6f26-40bc-be33-e5bfe9dc91ed', path: '', url: 'http://192.168.8.249:8081')], contextPath: '/app', war: '**/*.war'
                echo "========executing A========"
            }    
        }

    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
