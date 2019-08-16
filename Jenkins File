pipeline 
{
    agent{
        label 'master'
    }
    stages
	{
		stage('ABC')
		{
			steps
			{
				input ('Ready to go for ABC Job?')  //Asking Permission before Triggering 'ABC' Job
				build job: 'ABC', parameters: [
                    [$class: 'StringParameterValue', name: 'a', value: "${a}"],
					[$class: 'StringParameterValue', name: 'b', value: "${c}"],
					[$class: 'StringParameterValue', name: 'c', value: "${a}"],
					[$class: 'StringParameterValue', name: 'd', value: "${d}"],
				]
			}
			
		}
		stage('PQR')
		{
			steps
			{
				build job: 'PQR', parameters: [
                    [$class: 'StringParameterValue', name: 'a', value: "${a}"],
				]
			}
			
		}
		//Many More Stages may be included
	}
	post('Send eMAIL') {
        failure {    // notify users when the Pipeline fails
            // deleteDir() /* clean up our workspace */
            mail (to: 'abc@abc.com',
            subject: "Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) has Completed",
            body: "Please go to ${env.BUILD_URL} to verify failure status");
        }
        success {    // notify users when the Pipeline succeeds
            deleteDir() /* clean up our workspace */
            mail (to: 'abc@abc.com',
            subject: "Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) has Completed",
            body: "Please go to ${env.BUILD_URL} to verify success status");
        }
    }
}
