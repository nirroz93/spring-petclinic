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
                sh 'mvn -B -DskipTests clean package'
		echo "OPFPSPF"
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                failure {
			mail to: 'nirroz93@gmail.com',
             			subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             			body: "Build fail"
			echo "Fail!"
                }
            }
        }
        stage('Deliver') { 
            steps {
                sh 'mv target/spring-petclinic-1.5.1.jar /tmp/host' 
            }
        }
    }
}
