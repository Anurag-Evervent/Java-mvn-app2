pipeline {
    agent {label 'slave_2'}
    
     tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-3.6.3"
    }

    stages {
        stage('SCM Checkout') {
            steps {
                echo 'Hello World'
                git 'https://github.com/Anurag-Evervent/Java-mvn-app2.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Perform appliction build'
                // Run Maven on a selve agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }  
        stage('Deploy to QA server') {
            steps {
                echo 'Deploy to QA'
                sshPublisher(publishers: [sshPublisherDesc(configName: 'QA_Server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: 'target/', sourceFiles: 'target/mvn-hello-world.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }  
    }
}
