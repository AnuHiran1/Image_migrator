node
{
properties([parameters([text(defaultValue: '''api-application-status:R5.4.0_P1_AZURE
api-ump:R5.4.0_P1_AZURE''', description: '', name: 'string'), string(defaultValue: 'registry-nonprod.imiconnect.net:80', description: 'Enter Source registry', name: 'SOURCE', trim: false), choice(choices: ['registry-campaign.imicampaign.io:80'], description: 'Enter Destination registry', name: 'DESTINATION')])])

 

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
