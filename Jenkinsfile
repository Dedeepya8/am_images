node {
    label 'dev-builder'
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
 
        checkout scm
    }
 
    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
          def ubuntu = docker.image('ubuntu:latest')
         def ubuntu = docker.build("jenkins-ms/amimages:ubuntu", ')
        /*alpine = docker.build("jenkins-ms/amimages:alpine", "./alpine/")
        rhel   = docker.build("jenkins-ms/amimages:rhel", "./rhel/")*/
       /*app = docker.build("jenkins-ms/amimages:rhel")*/
    }
 
    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */
    }
 
    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://hub.docker.com/r/dvenigal/ubuntu', 'docker-hub-credentials') {
            ubuntu.push()
            ubuntu.push('latest')
            /*alpine.push()
            rhel.push()8/
            /*app.push("alpine")*/
            /*app.push("rhel")*/
        }
    }
}
