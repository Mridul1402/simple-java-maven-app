pipeline {
	agent any
	tools {
		maven 'MAVEN_HOME'
	}
	stages{
		stage('Check-out Repos'){
			steps{
				checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Mridul1402/simple-java-maven-app.git']])
			}
		}
		stage('Compile and Package'){
			steps{
				bat 'mvn compile package'
			}
		}
		stage('Archive'){
			steps{
				archiveArtifacts artifacts: 'target\\my-app-1.0-SNAPSHOT.jar', followSymlinks: false
			}
		}
		stage('Test'){
			steps{
				bat 'mvn test'
				junit '**/target/surefire-reports/*.xml'
				jacoco classPattern: '**/target/classes', exclusionPattern: '**/*Test*.class', execPattern: '**/target/jacoco.exec', inclusionPattern: '**/*.class', sourceExclusionPattern: 'generated/**/*.java', sourceInclusionPattern: '**/*.java'
			}
		}
	}
}
