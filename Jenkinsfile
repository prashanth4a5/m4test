pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                script{
                    def response = httpRequest customHeaders: [[name: 'Authorization', value: 'Basic YXVzbnN3MTA6QXVzbnN3MTA=']], url: 'https://maven.anypoint.mulesoft.com/api/v1/organizations/20db3a05-030a-4002-8df3-0188ff228246/maven/20db3a05-030a-4002-8df3-0188ff228246/t2/maven-metadata.xml'
                   
println(response.content);
def list =  new XmlParser().parseText(response.content)
println('**');
def vers = list.value()[2].value()[0].value()[0]
new_ver= (vers.substring(0,vers.lastIndexOf(".")+1) + (Integer.parseInt(vers.substring(vers.lastIndexOf(".")+1)) + 1))
println('**');


}
echo "${new_ver}"
                }
               
            }
        }
    }
