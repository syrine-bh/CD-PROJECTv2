pipeline
{
	agent any 
	stages {
		stage('Pull') {
			steps{
			script{
				checkout([$class: 'GitSCM' , branches: [[name: '*/master']],
					userRemoteConfigs: [[ 
					url: 'https://github.com/syrine-bh/CD-PROJECTv2.git']]])
				}
			}
		}
		
	 	stage('build') {
	    	steps{
	     		script{
	     	          sh "npm ci"

	                  sh " ansible-playbook ansible/build.yml  -i /ansible/inventory/host.yml -e 'ansible_become_password=ansible' -vvv "

	           }
	        }
	    }
	    	stage('docker') {
	    	steps{
	     		script{
	          		sh "ansible-playbook ansible/docker.yml  -i /ansible/inventory/host.yml -e 'ansible_become_password=ansible' -vvv"
	           }
	        }
	    }
	    stage ('DockerHub'){
     	 steps{
        script{
        sh "ansible-playbook ansible/docker-registry.yml  -i /Ansible/inventory/host.yml -e 'ansible_become_password=ansible'"

        }
      }
    }
	}
}
