
node{
    def mvnHome = tool 'Maven 3.5.x'
    env.JAVA_HOME="${tool 'Oracle JDK 1.8 (latest)'}"
    // What branch are we running in?
    def branchType = branch()
    stage("checkout") {
        checkout scm
    }

    stage("Unit Tests") {
        sh "${mvnHome}/bin/mvn clean test"
    }
    stage("Packaging") {
        sh "${mvnHome}/bin/mvn install"
    }

    if (branchType == 'master') {
        stage("deploy"){
            def userInput = input(
                    id: 'userInput', message: 'Let\'s deploy?', parameters: [
                    [$class: 'TextParameterDefinition', defaultValue: 'S3', description: 'Environment', name: 'env']])
            echo ("Env: "+userInput)
        }
    }
}



/**
 * Return the shortened git sha-1 commit identifier for the workspace git repo
 * @return string shortened sha-1 git commit
 */
def gitCommit() {
    sh(returnStdout: true, script: 'git rev-parse HEAD').trim().substring(0,8)
}

/**
 * Return the git flow branch "type".
 * Useful for altering the pipeline based on the branch type.
 *
 * @return string: either release, hotfix, develop, master, or the full branch name if neither a release, develop or a hotfix branch.
 */
def branch() {
    def branchMatch = (env.BRANCH_NAME =~ '((release|hotfix)/)?(.+)$')
    (branchMatch[0][2]) ? branchMatch[0][2] : branchMatch[0][3]
}


