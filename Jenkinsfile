

import groovy.json.*

node {
	//try {
		stage('Code checkout'){
		    try {
			echo "**************Checkout code in SCM***********"
			checkout scm
			}
		    catch(exc) {
			println "Error in checkout:" + e
			continuePipeline = false
			throw e
			}
		}
	
		specs_read = readYaml file: "${WORKSPACE}/specs/eb_deploy_specs.yml"
		specs = specs_read
	
		stage('EB deployment'){
		    
			echo "*******************Elastic Beanstalk Deployment*******************"
			//steps{
			    step([
				    $class: 'AWSEBDeploymentBuilder',
				    config: specs.ebdeploy.config,
				    awsRegion: specs.ebdeploy.awsRegion,
				    credentialId: specs.ebdeploy.credentialId,
				    environmentName: specs.ebdeploy.environmentName,
				    applicationName: specs.ebdeploy.applicationName,
				    versionLabelFormat: specs.ebdeploy.versionLabelFormat,
				    versionDescriptionFormat: specs.ebdeploy.versionDescriptionFormat,
				    bucketName: specs.ebdeploy.bucketName,
				    keyPrefix: specs.ebdeploy.keyPrefix,
				    rootObject: specs.ebdeploy.rootObject,
				    includes: specs.ebdeploy.includes,
				    excludes: specs.ebdeploy.excludes,
				    checkHealth: specs.ebdeploy.checkHealth,
				    maxAttempts: specs.ebdeploy.maxAttempts,
				    skipEnvironmentUpdates: specs.ebdeploy.skipEnvironmentUpdates,
				    sleepTime: specs.ebdeploy.sleepTime,
				    zeroDowntime: specs.ebdeploy.zeroDowntime
				])
			//}
		    
			
		    //catch(exc) {
			//println "Error in EB deployment:" + e
			//continuePipeline = false
			//throw e
		    //}
		}
	//}
	
	//catch(exc) {
	    //println "Build deploy failed"
	    //currentBuild.result = 'FAILED'
	//}
}
	
	
