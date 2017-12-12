pipeline {
    agent {
        docker {
            image 'maven:3.5'
            args '-v /root/.m2:/root/.m2 -v /tmp:/tmp/host'
        }
    }
    stages {
        stage('Build') {
            steps {
                mail to: 'nirroz93@gmail.com',
                                subject: "Started Pipeline: ${currentBuild.fullDisplayName}",
                                body: "pipelinestart"
		sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deliver') { 
            steps {
                sh 'mv target/spring-petclinic-1.5.1.jar /tmp/host' 
            }
        }
    }
    post {
       failure {
           echo "FAIL JENKINS PIPE"
	   mail to: 'nirroz93@gmail.com',
               subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
               body: "Build fail"
       }
    }
    
}
