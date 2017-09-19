node{
    def mvnHome = tool 'mvn3.5.0'
    stage("checkout") {
        checkout scm
    }

    stage("Unit Tests") {
        sh "${mvnHome}/bin/mvn clean test"
    }
    stage("Packaging") {
        sh "${mvnHome}/bin/mvn install"
    }
}
