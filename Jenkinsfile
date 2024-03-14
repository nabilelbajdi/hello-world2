node {
    // define required tools based on jenkins global tool configruation names
    def mvnHome = tool 'MAV'
    def javaHome = tool 'JDK'
    env.PATH = "${javaHome}/bin:${mvnHome}/bin:${env.PATH}"

    // define list of repo-branch pairs to build
    def buildConfigurations = [
        [repo: 'https://github.com/nabilelbajdi/hello-world', branch: '1'],
        [repo: 'https://github.com/nabilelbajdi/hello-world', branch: '2'],
        [repo: 'https://github.com/nabilelbajdi/hello-world2', branch: 'a'],
        [repo: 'https://github.com/nabilelbajdi/hello-world2', branch: 'b']
    ]
    
    //iterate over each repo-branch pair
    buildConfigurations.each { config ->
        // extract name from the repo URL
        def repoName = config.repo.tokenize('/').last()

        // modify stage name
        String stageName = "building ${repoName} on branch ${config.branch}"
        
        stage(stageName) {
            echo "Checkout ${config.repo} on branch ${config.branch}"
            git branch: config.branch, url: config.repo
            
            echo "Run mvn clean install"
            sh "mvn clean install"
        }
    }
}
