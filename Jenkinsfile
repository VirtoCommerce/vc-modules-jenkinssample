import groovy.json.*

node 
{
	stage 'Checkout'
        checkout([
            $class: 'GitSCM', 
            branches: [[name: '*/master']], 
            extensions: [[
			    $class: 'PathRestriction', 
			    excludedRegions: 'CommonAssemblyInfo\\.cs', 
			    includedRegions: ''
		    ]], 
            userRemoteConfigs: [[
                credentialsId: 'sasha-jenkins', 
                url: 'git@github.com:VirtoCommerce/vc-module-jenkinssample.git']]])
}