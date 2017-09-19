node{
    stage("Prepare environment") {
        echo "Starting the process"
        withMaven(maven: "3.5.0"){
            sh "mvn clean install"
        }


    }
}
