# JBoss Drools - DMN
  
## Create DMN model using [dmn.new](http://dmn.new/)

* Create the decision model  
  ![dmn_model](dmn_model.png)  

* Define the data type 
  ![dmn_data](dmn_datatype.png) 

* Define the decision table  
  ![dmn_decision](dmn_decisiontable.png)  

* Download the [DMN file](fico.dmn)  

## Use JBoss Drools locally

* Start the docker containers for business-central and kie-server
>docker run -p 8080:8080 -p 8001:8001 -d --name jbpm-workbench jboss/business-central-workbench-showcase:latest  
docker run -p 8180:8080 -d --name kie-server --link jbpm-workbench:kie-wb jboss/kie-server-showcase:latest  

* Login (admin/admin) to [business central](http://localhost:8080/business-central)  
  ![drools_businesscentral](drools_businesscentral.png)   

* Create a new project and import the DMN file 
  ![drools_projects](drools_projects.png) 

* Check the decision model
  ![drools_model](drools_decisiontable.png)  

* Test the model  
  ![drools_test](drools_testscenario.png)  

* Deploy to KIE server  
  ![drools_deploy](drools_deploy.png)  

* Check on the KIE server  
  ![drools_kie](drools_kieserver.png)  

* Check the decision service schema  
  ![drools_kie_schema](drools_kieserver_schema.png)  

## Execute the model
* Create the [input JSON](input.json) file  
* Invoke it from the command line!  
>curl -u kieserver:kieserver1! -H "accept: application/json" -H "content-type: application/json" -X POST "http://localhost:8180/kie-server/services/rest/server/containers/CreditScore/dmn" -d @input.json  
 
> {  
   "type" : "SUCCESS",  
   "msg" : "OK from container 'CreditScore'",  
   "result" : {  
     "dmn-evaluation-result" : {  
       "messages" : [ ],  
       "model-namespace" : "https://kiegroup.org/dmn/_4B1EDB3E-BB80-4CDD-8785-52AF13FFCD32",  
       "model-name" : "CreditScore",  
       "decision-name" : "Check Credit Score",  
       "dmn-context" : {  
         "Check Credit Score" : "excellent",  
         "Applicant" : {  
           "fico" : 700,  
           "name" : "John"  
         }  
      },  
      "decision-results" : {  
        "_5C29E6BC-E182-40B0-8FCD-D2F0312227B4" : {  
          "messages" : [ ],  
          "decision-id" : "_5C29E6BC-E182-40B0-8FCD-D2F0312227B4",  
          "decision-name" : "Check Credit Score",  
          "result" : "excellent",  
          "status" : "SUCCEEDED"  
        }  
      }  
    }  
  }  
}  

