node {
    // Define tools
    def mvnHome = tool 'MAV'
    def javaHome = tool 'JDK'
    env.PATH = "${javaHome}/bin:${mvnHome}/bin:${env.PATH}"

    // List of repo-branch pairs to build
    def buildConfigurations = [
        [repo: 'https://github.com/nabilelbajdi/hello-world', branch: '1'],
        [repo: 'https://github.com/nabilelbajdi/hello-world', branch: '2'],
        [repo: 'https://github.com/nabilelbajdi/hello-world2', branch: 'a'],
        [repo: 'https://github.com/nabilelbajdi/hello-world2', branch: 'b']
    ]

    buildConfigurations.each { config ->
        // Extract the simple name from the repo URL
        def repoName = config.repo.tokenize('/').last()

        // Construct the stage name as per the specified format
        String stageName = "building ${repoName} on branch ${config.branch}"
        
        stage(stageName) {
            echo "Checkout ${config.repo} on branch ${config.branch}"
            git branch: config.branch, url: config.repo
            
            echo "Run mvn clean install"
            sh "mvn clean install"
        }
    }
}
