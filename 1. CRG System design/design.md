1. SQL implemetation:
   SQL query to to do compatibility check with exiting meta data in cnap DB

2. For given cluster_id and for given product_name the new version passed in input json is it compatible ?  
     
3. Input json format to run sql query:  
     

{

   cluster_id: "W1",  
   cluster_name: "W",

   kafka_new_version : "5.0",

   weblogicserver_new_version : "4.0",

   dbcs_new_version : "6.0"

}

1. Sql Logic :  
     
2. Output Json format return type from the sql query ran against the cnap DB:  
     

{

  "BRM" : {

    "kafka" :{

      "current_version" : "1.0",

      "new version " : "5.0",

      "incompatibility" : true

    }

  },

  "AIA" : {

    "weblogicserver" : {

      "current_version" : "2.0",

      "new version " : "4.0",

      "incompatibility" : true

    }

  },

  "STAP" : {

    "dbcs" : {

      "current_version" : "3.0",

      "new version " : "6.0",

      "incompatibility" : true

    }

  }

}