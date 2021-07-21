pipeline {
	agent {
		node {
			label 'nodejs'
		}
	}
	triggers {
		pollSCM ('H/3 * * * *')
	}
	options {
		disableConcurrentBuilds()
	}
	stages {
		stage ('validate') {
			steps {
				sh 'oc project demo'
				sh 'oc apply --dry-run --validate -k helloworld'
			}
		}
		stage ('apply') {
			when {
				branch 'master'
			}
			steps {
				sh 'oc project demo'
				sh 'oc apply -k helloworld'
			}
		}
	}
}
