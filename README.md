# Image_migrator
Jenkins pipeline job which promotes images from one private registry to other registry.

## Steps to run Jenkins Pipeline job:

1.Run the Jenkins pipeline job by selecting the build with parameters option.

2.Update the string box with the list of images with tag ex:
nginx:.2
jenkins:2.0

3.Update the Source box with registry URL that you want to pull the images from ex: "private_registry:80"

4.Select the  DESTINATION registry from the drop-down button

5.Click on the build button
