#!groovy
import groovy.json.*
import groovy.util.*

node
{
	checkout scm
	
	def manifestFile = readFile file: 'module.manifest', encoding: 'utf-8'
	def manifest = new XmlSlurper().parseText(manifestFile)

	echo manifestFile
	def title = manifest.title.toString()
    	echo "Upading module ${manifest.id}"
    	updateModule(manifest)

/*

        "id": "VirtoCommerce.Core",
        "version": "2.12.0",
        "platformVersion": "2.11.0",
        "title": "Commerce core module",
        "description": "Common e-commerce domain functionality",
        "groups": [ "commerce" ],
        "authors": [ "Virto Commerce" ],
        "owners": [ "Virto Commerce" ],
        "projectUrl": "https://github.com/VirtoCommerce/vc-module-core",
        "iconUrl": "https://raw.githubusercontent.com/VirtoCommerce/vc-module-core/master/VirtoCommerce.CoreModule.Web/Content/logoVC.png",
        "packageUrl": "https://github.com/VirtoCommerce/vc-module-core/releases/download/v2.12/VirtoCommerce.Core_2.12.0.zip"

*/
}

def updateModule(def manifest)
{
	// MODULES
        dir('modules') {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'sasha-jenkins', url: 'git@github.com:VirtoCommerce/vc-modules.git']]])

            def inputFile = readFile file: 'modules.json', encoding: 'utf-8'
            def parser = new JsonSlurper()
            echo inputFile
            def json = parser.parseText(inputFile)
            echo json
            def builder = new JsonBuilder(json)
            
            for (rec in json) {
               if ( rec.id == manifest.id) {
               	    echo "found record, updating ${rec.id}"
               	    rec.description = "test"
		break
               }
            }
            
            println(builder.toPrettyString())
        }
}
