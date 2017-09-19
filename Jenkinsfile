node{
    stage("Prepare environment") {
        def mvnHome = tool 'mvn3.5.0'
        checkout scm
        echo "Starting the process"
        sh "${mvnHome}/bin/mvn clean install"

    }
}
