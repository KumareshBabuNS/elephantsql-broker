# ElephantSQL Broker

## Overview

ElephantSQL Broker provides PostgreSQL database instanses on demand as a Cloud Foundry service. The service broker does not include a PostegreSQL server or cluster. Instead, it is meant to be deployed alongside a managed ElephantSQL account, which provide provision and maintainace of PostgreSQL instances though APIs.
 
The ElephantSQL Broker tasks that the broker performs are as follows:
    
- Provisioning of PostgreSQL database instanse (create)
- Provide access to database credentials (bind)
- Remove access to database credentials (unbind)
- Remove of PostgreSQL database instance (delete)
- Update databasen instance plan (update)

## Installation

### 1. Compile source code and package 

- Checkout the ElephantSQL broker from github and enter the project's directory.
```
$ git clone https://github.com/ipolyzos/elephantsql-broker.git
$ cd elephantsql-broker
```
- Clean compile and package the project.
```
$ > mvn clean
$ > mvn package
```

### 2. Edit the **manifest.yml** file.

The [sample manifest.yml](https://github.com/ipolyzos/elephantsql-broker/blob/master/manifest-sample.yml) provided can be used as a reference. The specific
variables for the mongodb atlas broker are :

| Key           |Description    | Default      |
| :------------- | :------------- | :------------- | 
| **ELEPHANTSQL_API_URL** | The default API URL as provided by ElephantSQL documentation i.e.|*https://customer.elephantsql.com/api*| 
| **ELEPHANTSQL_REGION** | Region to provision servers. (please advie [ElephantSQL Documentaion](https://www.elephantsql.com/docs/index.html) for the list of available regions)| amazon-web-services::eu-west-1 |
| **ELEPHANTSQL_API_KEY** | API Key as generated from ElephantSQL.| - |

### 3. Push the code and create register thr broker
1. Push the broker into CF i.e.  ``` cf push  ```
2. Register service broker in CF : 
```
cf create-service-broker elephantsql admin P455w0rd https://elephantsql-broker.{{ domain }}
```
### 3. Enable access to the broker 
 
 Finally you need to allow access to the broker e.g. ``` cf enable-service-access elephantsql ```

## Developing
 
 See the [contribution guidelines](https://github.com/ipolyzos/elephantsql-broker/tree/master/CONTRIBUTING.md).
 
## Disclaimer 
 
 Please *NOTE* the broker is still under development and does not intend to be used in production.
 
## License

   Copyright 2017 Ioannis Polyzos

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.