pipeline {
	agent {
		label 'nodejs'
	}
    parameters {
        string(name: 'image', defaultValue: '', description: 'Docker image to use')
        string(name: 'root_cert', defaultValue: '', description: 'Root certificate to inject')
    }
	stages{
		stage("Inject rootcert"){
			steps{
				writeFile(file: "myroot.crt", text: params.root_cert)
				sh label: '', script: 'cat myroot.crt'
				sh label: '', script: 'docker build -t {$params.image} .'
				
			}
		}
	}
}
