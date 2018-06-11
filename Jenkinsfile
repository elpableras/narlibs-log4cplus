pipeline {
    
    agent none

	stages {
		stage ('Checkout'){
			parallel {
				stage('Windows') {
					agent { label "windows" }
					steps {
						deleteDir()
						checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'SubmoduleOption', disableSubmodules: false, parentCredentials: false, recursiveSubmodules: true, reference: '', trackingSubmodules: false]], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/CERN/narlibs-log4cplus']]])
					}
				}
				stage('Unix') {
					agent { label "unix" }
					steps {
						deleteDir()
						checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'SubmoduleOption', disableSubmodules: false, parentCredentials: false, recursiveSubmodules: true, reference: '', trackingSubmodules: false]], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/CERN/narlibs-log4cplus']]])
					}    
				}
			}
		}
			
		stage('Copy Artifacts') { 
			parallel {
				stage('Windows') {                  
					agent { label "windows" }
					steps {
						copyArtifacts filter: 'msvc14/x64/bin.Release/*.*', fingerprintArtifacts: true, projectName: 'log4cplus', target: 'src/nar/resources/aol/amd64-Windows-msvc/lib'
					}
				}
				stage('Unix') {            
					agent { label "unix" }
					steps {
						copyArtifacts filter: 'include/log4cplus/**/*.*', fingerprintArtifacts: true, projectName: 'log4cplus', target: 'src/nar/resources/noarch/include'
						copyArtifacts filter: '.libs/liblog4cplus.so', fingerprintArtifacts: true, projectName: 'log4cplus', target: 'src/nar/resources/aol/amd64-Linux-gpp/lib/'						
						sh 'mv src/nar/resources/aol/amd64-Linux-gpp/lib/liblog4cplus.so src/nar/resources/aol/amd64-Linux-gpp/lib/liblog4cplus-nar-2.0.0.so'
					}					
				}
			}
		}
	}
}
