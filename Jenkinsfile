pipeline {
	agent {
		label 'nodejs'
	}
    parameters {
        string(name: 'image', defaultValue: 'v2.0.9-occ/vvp-appmanager:2.0.9', description: 'Docker image to use')
        string(name: 'root_cert', defaultValue: '', description: 'Root certificate to inject')
    }
	stages{
		stage("Inject rootcert"){
			steps{
				writeFile(file: "myroot.crt", text: params.root_cert)
				sh label: '', script: 'cat myroot.crt'
				//sh label: '', script: 'docker build -t ${params.image} .'
				sh "docker build -t ${params.image} ."
				
				
			}
		}
		stage("Copy Image"){
			steps{
					withDockerRegistry([credentialsId: 'PUBLISH_TO_ARTIFACTORY', url: 'https://artifactory.com"]) {
						sh "docker push ${params.image}"
					}
			}
		}
	}
}
