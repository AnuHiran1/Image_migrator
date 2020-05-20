node
{
properties([parameters([text(defaultValue: '''nginx:.0
tomcat:latest''', description: '', name: 'string'), string(defaultValue: 'private_registry:80', description: 'Enter Source registry', name: 'SOURCE', trim: false), choice(choices: ['destination_registry1:80','destination_registry2:80], description: 'Enter Destination registry', name: 'DESTINATION')])])

 

stage('Image migration'){
def list = string.split("\\r?\\n").each { param ->
    //println "${param}"
    }
    for (int i = 0; i < list.size(); i++)
                    {
                    def filename = list[i]
                    echo "${filename}"
                    docker.withRegistry("https://${params.SOURCE}")
                    {
                    image = docker.image("${filename}")
                    image.pull()
                    }
                   //docker tag
                    sh "docker tag ${params.SOURCE}/${filename} ${params.DESTINATION}/${filename}"     
       
      //push image to destiantion registry
                    image = docker.image("${params.DESTINATION}/${filename}")
                    docker.withRegistry("https://${params.DESTINATION}")
                    {
                         image.push()
                         }
        //delete pulled and tagged images
                    sh "docker rmi ${params.SOURCE}/${filename} && docker rmi ${params.DESTINATION}/${filename} "
   
}
}
}
