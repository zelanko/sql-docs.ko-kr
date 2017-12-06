---
title: "게시 및 Python 코드를 사용 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: f35ab73f5abadbf1405b4e68b506a169a98e31c4
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="publish-and-consume-python-web-services"></a>게시 및 Python 웹 서비스를 사용 합니다.

Microsoft 학습 서버 컴퓨터의에서 화 기능을 사용 하 여 웹 서비스에 작업 중인 Python 솔루션을 배포할 수 있습니다. 이 항목에서는 성공적으로 게시 한 후 솔루션을 실행 하는 단계를 설명 합니다.

이 문서에 대 한 대상 사용자는 Python 코드 또는 모델 Microsoft 학습 서버 컴퓨터에서에서 호스팅되는 웹 서비스로 게시 하는 방법을 알아 보 려는 데이터 과학자입니다. 설명 하 고 응용 프로그램을 소비할 수 있는 방법의 코드 또는 모델입니다. 이 문서에서는 Python에 능숙 한 한다고 가정 합니다.

> [!IMPORTANT]
>
> 이 예제는 학습 Server 컴퓨터 (독립 실행형)는 포함 되며 컴퓨터 학습 서버 버전의 기능을 사용 하 여 Python 버전에 대 한 개발 되었습니다 **9.1.0**합니다.
 > 
 > 학습 서버 컴퓨터에에서는 최신 라이브러리를 사용 하 여 다시 게시 동일한 샘플을 보려면 다음 링크를 클릭 합니다. 참조 [배포에서 Python 웹 서비스를 관리 하 고](https://docs.microsoft.com/machine-learning-server/operationalize/python/how-to-deploy-manage-web-services)합니다.

**적용 대상: Microsoft R Server (독립 실행형)**

## <a name="overview-of-workflow"></a>워크플로 개요

Python 웹 서비스를 사용 하는 데 게시에서 워크플로 다음과 같이 요약할 수 있습니다.

1. 처리는 [필수 구성 요소](#prereq) 코어 API Swagger 문서에서 Python 클라이언트 라이브러리를 생성 합니다.
2. 인증 및 헤더 논리 Python 스크립트를 추가 합니다.
3. Python 세션을 만들고 환경을 준비 환경을 유지 하기 위해 스냅숏을 만듭니다.
4. 웹 서비스를 게시 하 고이 스냅숏을 포함 합니다.
5. 세션에서 사용 하 여 웹 서비스를 해보세요.
6. 이러한 서비스를 관리 합니다.

![Swagger 워크플로](./media/data-scientist-python-workflow.png)

이 문서는 워크플로의 각 단계에 설명 하 고 iris 데이터 집합을 사용 하 여 샘플 Python 코드가 포함 되어 있습니다.

## <a name="sample-code"></a>예제 코드

이 샘플 코드에서는 충족 하는 [필수 구성 요소](#prereq) 해당 Swagger에서 Python 클라이언트 라이브러리를 생성 하려면 파일 및을 사용한 Autorest 합니다.

코드 블록을 한 후 전체 프로세스에 대 한 더 자세한 설명이 포함 된 단계별 연습을 찾을 수 있습니다.

> [!IMPORTANT]
> 이 예에서는 로컬 `admin` 인증에 대 한 계정입니다. 하지만 자격 증명을 대체 해야 및 [인증 방법을](#python-auth) 관리자를 구성 합니다.

```python
##################################################
##       IMPORT GENERATED CLIENT LIBRARY        ##
##################################################

# Import the generated client library. 

import deployrclient

# This example is intended for use with Microsoft R Server 9.0.1. 
# If you are using a newer version of Machine Learning Server, 
# use the mrs_server library instead.

##################################################
##              AUTHENTICATION                  ##
##################################################

#Using client library generated from Autorest
#Create client instance and point it at an R Server. 
#In this case, R Server is local.
client = deployrclient.DeployRClient("http://localhost:12800")
# To use ML Server, replace with mrs_server.MRSServer()

#Define the login request and provide credentials 
#Update values with the connection parameters from your admin
login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")

#Make a call to the /login API. 
#Store the returned an access token in a variable.
token_response = client.login(login_request)

#Add the returned access token to the headers variable.
headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}

#Verify that the server is running.
#Remember to include `headers` in all requests!
status_response = client.status(headers) 
print(status_response.status_code)


##################################################
##        CREATE SESSION, MODEL, SNAPSHOT       ##
##################################################

#Since already logged in, create a Python session.
#Define session using name (`Session 1`) and `runtime_type="Python"`.
#Remember to specify the Python runtime type.
create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")

#Make the call to start the session. 
#Remember to include headers in all method calls to the server.
#Returns a session ID.
response = client.create_session(create_session_request, headers) 
   
#Store the session ID in a variable called `session_id` 
#to be able to identify it later at execution time.
session_id = response.session_id

#Create model - Import SVM and datasets from the SciKit-Learn library
execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define the untrained Support Vector Classifier (SVC) object
#and the dataset to be preloaded.
execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
#Now, go create the object and preload Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define two rows from the Iris Dataset as a sample for scoring
workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

#Define how to train the classifier model; what to predict; what to return
execute_request = deployrclient.models.ExecuteRequest(
    "clf.fit(iris.data, iris.target)\n"+
    "result=clf.predict(species_1)\n"+
    "other_result=clf.predict(species_2)",
    [workspace_object,workspace_object_2], #Input
    ["result", "other_result"]) #Output

#Now, go train that model on the Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)

#If successful, print name and result of each output parameter. Else, print error.
if(execute_response.success):
    for result in execute_response.output_parameters:
        print("{0}: {1}".format(result.name,result.value))
else:
    print (execute_response.error_message)

#Create a snapshot of the current session
response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
#Return the snapshot ID for reference when you publish later.
response.snapshot_id
#If you forget the ID, list snapshots to get the ID again.
for snapshot in client.list_snapshots(headers):
    print(snapshot)

##################################################
##        PUBLISH AS A SERVICE IN PYTHON        ##
##################################################

#Define a web service that determines the iris species by scoring 
#a vector of sepal length and width, petal length and width

#Set `flower_data` for the sepal and petal length and width
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
#Set `iris_species` for the species of iris
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")

#Define the publish request for the web service and its arguments.
#Specify the code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

#Publish the service using the specified name (iris), version (V1.0)
client.publish_web_service_version("Iris", "V1.0", publish_request, headers)

##################################################
##           CONSUME SERVICE IN PYTHON          ##
##################################################

# Inspect holdings and metadata for service Iris V1.0.
for service in client.get_web_service_version("Iris","V1.0", headers):
    #print service metadata (description, who published,...)
    print(service)
    #Print input and output parameters as defined in service definition object
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Import the requests library to make requests on the server
import requests
#Import the JSON library to use for pretty printing of json responses
import json

#Create a requests `Session` object.
s = requests.Session()

#Record the R Server endpoint URL hosting the web services you created before
url = "http://localhost:12800"

#Give the request.Session object the authentication headers 
#so you don't have to repeat it with each request.
s.headers = headers

#Retrieve the service-specific swagger file using the requests library.
swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

#Either, download service-specific swagger file using the json library.
with open('iris_swagger.json','w') as f:
   (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

#Or, print just what you need from the Swagger file, 
#such as the routing paths for the endpoints to be consumed.
print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

#Or, print input and output parameters as defined in the Swagger.io format
print("Input")
print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
print("Output")
print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))

#Make the request to consume the service using these flower_data inputs
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
#Print the output
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

##################################################
##          MANAGE SERVICES IN PYTHON           ##
##################################################

#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)

#Or, publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

## <a name="walkthrough"></a>연습

이 섹션에서는 코드의 더 자세하게에서 작동 하는 방법을 설명 합니다.


### <a name="prereq"></a>1 단계입니다. 필수 구성 요소 클라이언트 라이브러리 만들기

게시 하 여 Python 코드와 모델 thorugh Microsoft 학습 서버 컴퓨터를 시작 하려면 먼저이 릴리스에 대 한 제공 된 Swagger 문서를 사용 하 여 클라이언트 라이브러리를 생성 해야 합니다.

1. 로컬 컴퓨터의 Swagger 코드 생성기를 설치 하 고 것을 잘 이해 해야 합니다. Python에서 API 클라이언트 라이브러리를 생성 하려면 사용 합니다. 인기 있는 도구에 포함 [Azure AutoRest](https://github.com/Azure/autorest) (Node.js 필요) 및 [Swagger Codegen](https://github.com/swagger-api/swagger-codegen)합니다. 

2. 서버를 학습 하는 컴퓨터의 버전에 대 한 핵심 Api를 포함 하는 Swagger 파일을 다운로드 합니다. 이 파일에는 REST 리소스 및 해당 리소스에 대해 호출 될 수 있는 작업의 목록을 정의 하는 Swagger 템플릿을 포함 합니다. 이 파일을 찾을 수 `https://microsoft.github.io/deployr-api-docs/swagger/<version>/rserver-swagger-<version>.json`여기서 `<version>` 3 자리 R 서버 버전 번호입니다. 

   예를 들어 서버 9.1 R에 대 한 사용자가 다운로드에서: https://microsoft.github.io/deployr-api-docs/9.1.0/swagger/rserver-swagger-9.1.0.json

3. 전달 하 여 정적으로 생성 하는 클라이언트 라이브러리를 생성 된 `rserver-swagger-<version>.json` Swagger 코드 생성기에 파일을 원하는 언어를 지정 합니다. 이 경우 Python을 지정 해야 합니다.  

    예를 들어 AutoRest Python 클라이언트 라이브러리를 사용 하면 것 같을 수 있습니다, 3 자리 숫자는 R 서버 버전 번호를 나타냅니다.
    
    `AutoRest.exe -Input rserver-swagger-9.1.0.json -CodeGenerator Python  -OutputDirectory C:\Users\rserver-user\Documents\Python`

4. 일부 사용자 지정 헤더를 제공 하 고 다른 변경 생성된 된 클라이언트를 사용 하기 전에 라이브러리 스텁 수도 있습니다. 참조는 [명령줄 인터페이스](https://github.com/Azure/autorest/blob/master/docs/user/cli.md) 대 한 다른 구성 옵션 및 네임 스페이스 이름 바꾸기와 같은 기본 설정에 대 한 자세한 내용은 GitHub에 대 한 설명서입니다.
   
5. 볼 수 있게 하 여 다양 한 API 호출 수는 핵심 클라이언트 라이브러리를 탐색 합니다. 

    예에서 Autorest 일부 디렉터리 및 Python 클라이언트 라이브러리에 대 한 로컬 시스템에서 파일을 생성 했습니다. 기본적으로 네임 스페이스 (및 디렉터리)은 `deployrclient` 및 다음과 같은 형식입니다.
   
   ![Autorest 출력 경로](./media/data-scientist-python-autorest.png)

    이 기본 네임 스페이스에 대 한 클라이언트 라이브러리 자체 라고 `deploy_rclient.py`합니다. 예: Visual Studio IDE에서이 파일을 열면 다음과 같이 나타납니다.
   
   ![Python 클라이언트 라이브러리](./media/data-scientist-python-client-library.png)


### <a name="step-2-add-authentication-and-header-logic"></a>2단계. 인증 및 헤더 논리 추가

모든 Api 인증이; 필요 않음을 염두에서에 둬야 API를 사용 하 여 호출을 만들 때 모든 사용자가 인증 해야 따라서는 `POST /login` API 또는 통해 Azure Active Directory (AAD). 

이 프로세스를 단순화 하려면 전달자 액세스 토큰을 사용자가 필요한 각 호출에 대 한 자격 증명을 제공 하지 않도록 발급 됩니다.  이 전달자 토큰은 보호 된 리소스에 대 한 "전달자" 액세스를 부여 하는 경량 보안 토큰:이 경우 서버는 컴퓨터 학습 Api입니다. 사용자가 인증 된 후 응용 프로그램은 의도 한 당사자에 대 한 인증에 성공적으로 확인 하는 사용자의 전달자 토큰을 확인 해야 합니다. 이러한 토큰을 관리 하는 방법에 대 한 자세한 참조 [보안 액세스 토큰](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens)합니다.

핵심 Api 상호 작용 하기 전에 먼저 인증, 전달자 액세스를 사용 하 여 토큰의 [인증 방법을](https://msdn.microsoft.com/microsoft-r/operationalize/security-authentication) 관리자가 구성 된 한 후 각 후속 요청에 대 한 각 헤더에 포함:

1. Jupyter, Visual Studio, VS Code 또는 iPython 같은 코드 편집기를 사용자 기본 Python에서 액세스할 수 있도록 설정 하는 클라이언트 라이브러리를 가져와서 시작 하세요.

   클라이언트 라이브러리의 부모 디렉터리를 지정 합니다. 이 예제에서 Autorest 생성 된 클라이언트 라이브러리에서는 `C:\Users\rserver-user\Documents\Python\deployrclient`:

   ```python
   # Import the generated client library
   import deployrclient
   ```

2. 서버를 학습 하는 컴퓨터에 로컬 컴퓨터에서 연결을 정의 자격 증명을 제공, 액세스 토큰을 캡처, 해당 토큰 헤더에 추가할 응용 프로그램에 인증 논리를 추가 합니다. 그런 다음 모든 후속 요청에 대 한 해당 헤더를 사용 합니다.  관리자가 정의 된 인증 방법을 사용: 기본 관리자 계정, Active Directory/LDAP (AD/LDAP) 또는 Azure Active Directory (AAD).

   **AD/LDAP 또는 `admin` 계정 인증**

   호출 된 `POST /login` 를 인증 하기 위해 API입니다. 전달 된 `username` 및 `password` 로컬 관리자에 대 한 또는 Active Directory를 사용 하는 경우 LDAP 계정 정보를 전달 합니다. 차례로 컴퓨터 학습 서버 전달자/액세스 토큰을 발급합니다. 인증 된 후 사용자 토큰은 여전히 유효 하 고 각 요청과 함께 전송 되는 헤더를 다시 자격 증명을 제공 하도록 더 이상 필요 합니다. 연결 설정의 알 수 없는 경우 관리자에 게 문의 하십시오.

   ```python
   #Using client library generated from Autorest
   #Create client instance and point it at an R Server. 
   #In this case, R Server is local.
   client = deployrclient.DeployRClient("http://localhost:12800")
   
   #Define the login request and provide credentials. 
   #Update values with the connection parameters from your admin.
   login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")
   #Make a call to the /login API. 
   #Store the returned an access token in a variable.
   token_response = client.login(login_request)
   ```

   **Azure Active Directory (AAD) 인증**

   AAD 자격 증명, 권한 및 클라이언트 ID를 전달 합니다. AAD 발급 차례로 [전달자 액세스 토큰](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens)합니다. 인증 된 후 사용자 토큰은 여전히 유효 하 고 각 요청과 함께 전송 되는 헤더를 다시 자격 증명을 제공 하도록 더 이상 필요 합니다. 연결 설정의 알 수 없는 경우 관리자에 게 문의 하십시오.

   ```python
   #Import the AAD authentication library
   import adal
   
   #Define the login request and provide credentials. 
   #Use the AAD connection parameters provided by your admin.
   url = "http://localhost:12800"
   authuri = https://login.windows.net,
   tenantid = "<<AAD_DOMAIN>>", 
   clientid = "<<NATIVE_APP_CLIENT_ID>>", 
   resource = "<<WEB_APP_CLIENT_ID>>", 
   
   #Acquire authentication token using AAD Device Code Login
   context = adal.AuthenticationContext(authuri+'/'+tenantid, api_version=None)
   code = context.acquire_user_code(resource, clientid)
   print(code['message'])
   token = context.acquire_token_with_device_code(resource, code, clientid)
   #The authentication code returned must be entered at https://aka.ms/devicelogin 
   ```     

3. 추가 `Bearer` 액세스 토큰 및 학습 서버 컴퓨터 현재 실행 되 고 있는지 확인 하십시오.  이 토큰 인증 동안 반환 된 및 **모든 후속 요청 헤더에 포함 되어야 합니다**합니다. 이 예제에서는 Autorest에 의해 생성 된 클라이언트 라이브러리를 사용 합니다.

   > [!IMPORTANT]
   > 모든 API 호출을 인증 되어야 합니다. 따라서 모든 단일 요청에 대 한 토큰을 가진 헤더를 포함 해야 합니다.

   ```python
   #Add the returned access token to the headers variable.
   headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}
   
   #Verify that the server is running.
   #Remember to include `headers` in every request!
   status_response = client.status(headers) 
   print(status_response.status_code)
   ```

### <a name="step-3-prepare-session-and-code"></a>3단계. 세션 및 코드를 준비 합니다.

인증을 받은 후 Python 세션을 시작 하 고 나중에 게시에 대 한 모델을 만들 수 있습니다. 웹 서비스에서 모든 Python 코드 또는 모델을 포함할 수 있습니다. 세션 환경을 설정한 후도 저장할 있습니다 것 스냅숏으로 전에 사용 했던 대로 세션을 다시 로드할 수 있습니다. 

> [!IMPORTANT]
> 포함 하십시오 `headers` 한 모든 요청에 있습니다.

1. R 서버에 Python 세션을 만듭니다. 이름 및 Python 언어를 지정 하십시오 (`runtime_type="Python"`).  오른쪽에 기본적으로 런타임 형식을 Python을 설정 하지

   다음은 Autorest에서 생성 된 클라이언트 라이브러리를 사용 하는 예의 연속입니다.

   ```python
   #Since already logged in, create a Python session.
   #Define session using name (`Session 1`) and `runtime_type="Python"`.
   #Remember to specify the Python runtime type.
   create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")
   
   #Make the call to start the session. 
   #Remember to include headers in every method call to the server.
   #Returns a session ID.
   response = client.create_session(create_session_request, headers) 
   
   #Store the session ID in a variable called `session_id` 
   #to be able to identify it later at execution time.
   session_id = response.session_id
   ```

2. 만들거나 웹 서비스로 게시할 수 있는 Python에서 모델을 호출

   이 예제에서는 SciKit 자세한 지원 벡터 컴퓨터 (SVM) 모델 학습 서버 컴퓨터의 원격 인스턴스에서 Iris 데이터 집합을 학습합니다.  이 데이터 집합에서 사용할 수 있는는 [scikit-사이트에 알아봅니다](http://scikit-learn.org/stable/auto_examples/datasets/plot_iris_dataset.html)합니다.

   ```python
   #Import SVM and datasets from the SciKit-Learn library
   execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define the untrained Support Vector Classifier (SVC) object
   #and the dataset to be preloaded.
   execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
   #Now, go create the object and preload Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define two rows from the Iris Dataset as a sample for scoring
   workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
   workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

   #Define how to train the classifier model; what to predict; what to return
   execute_request = deployrclient.models.ExecuteRequest(
       "clf.fit(iris.data, iris.target)\n"+
       "result=clf.predict(species_1)\n"+
       "other_result=clf.predict(species_2)",
       [workspace_object,workspace_object_2], #Input
       ["result", "other_result"]) #Output

   #Now, go train that model on the Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)

   #If successful, print name and result of each output parameter. Else, print error.
   if(execute_response.success):
       for result in execute_response.output_parameters:
           print("{0}: {1}".format(result.name,result.value))
   else:
       print (execute_response.error_message)
   ```

3. 스냅숏을 만들고이 Python의이 환경은 웹 서비스에 저장 되 고에서 재현 세션 시간을 소모 합니다. 스냅숏은 특정 라이브러리, 개체, 모델, 파일 및 아티팩트를 포함 하는 준비 환경을 할 때 유용 합니다. 스냅숏은 전체 작업 영역 및 작업 디렉터리에 저장합니다. 그러나를 게시할 때 사용자가 만든 스냅숏을 사용할 수 있습니다.

   ```python
   #Create a snapshot of the current session.
   response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
   
   #Return the snapshot ID for reference when you publish later.
   response.snapshot_id
   
   #If you forget the ID, list snapshots to get the ID again.
   for snapshot in client.list_snapshots(headers):
       print(snapshot)
   ```

  > [!NOTE] 
   > 스냅숏은 환경 종속성에 대 한 웹 서비스를 게시 하는 경우에 사용할 수 있습니다, 동안 소비 시간의 성능에 영향을 미칠 수입니다.  최적의 성능을 위해서는 스냅숏의 크기를 신중 하 게 고려 하 고 필요 하 고 나머지 제거 작업 영역 개체로 유지 하는 확인 합니다. 세션에서 Python을 사용할 수 있습니다 `del` 함수 또는 [는 `deleteWorkspaceObject` API 요청](https://microsoft.github.io/deployr-api-docs/#delete-workspace-object) 불필요 한 개체를 제거 합니다. 

### <a name="step-4-publish-the-model"></a>4단계. 모델 게시 

클라이언트 라이브러리 생성 된 응용 프로그램에 인증 논리를 작성 한 후 핵심 Python 세션을 만들고 모델을 만들 다음 해당 모델을 사용 하 여 웹 서비스를 게시 하는 Api와 상호 작용할 수 있습니다.

유의 해야 할 몇 가지 사항:

+ 모든 API 호출을 수행 하기 전에 사용자를 인증 해야 합니다. 따라서 포함 `headers` 모든 요청에서 합니다.
+ 웹 서비스는 Python 서비스로 등록 되어 있는지를 보장 하려면을 지정 해야 `runtime_type="Python"`합니다. 오른쪽에 기본적으로 런타임 형식을 Python을 설정 하지
+ 점수 매기기 sepal 길이, sepal 너비, 꽃잎 길이 및 꽃잎 너비를 사용 하 여 벡터를 필요

다음 코드는 Python 웹 서비스로 SVM 모델을 게시합니다. 이 웹 서비스에 전달 된 값을 기반으로 예측 된 범주를 생성 합니다.

```python
   #Set `flower_data` for the sepal and petal length and width
   flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
   #Set `iris_species` for the species of iris
   iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")
   
   #Define the publish request for the web service and its arguments.
   #Specify the code, inputs, outputs, and snapshot.
   #Don't forget to set runtime_type="Python"`.
   publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

   #Publish the service using the specified name (iris), version (V1.0)
   client.publish_web_service_version("Iris", "V1.0", publish_request, headers)
```

### <a name="step-5-consume-the-web-service"></a>5단계. 웹 서비스 사용

이 섹션에는 생성 된 위치에서 동일한 세션에 서비스를 사용 하는 방법을 보여 줍니다.

1. 동일한 세션에서 서비스에 대 한 서비스 지분 및 메타 데이터를 가져옵니다.

   ```python
   # Inspect holdings and metadata for service Iris V1.0.
   for service in client.get_web_service_version("Iris","V1.0", headers):
       #print service metadata (description, who published,...)
       print(service)
       #Print input and output parameters as defined in service definition object
       print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
       print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
   ```

2. 서비스 지분을 검사 하 고 사용 하도록 준비 합니다. 
   ```python
   #Import the requests library to make requests on the server
   import requests
   #Import the JSON library to use for pretty printing of json responses
   import json

   #Create a requests `Session` object.
   s = requests.Session()

   #Record the R Server endpoint URL hosting the web services you created
   url = "http://localhost:12800"

   #Include the request.Session object in the authentication headers.
   #By doing so, you don't need to repeat it with each request.
   s.headers = headers

   # Retrieve the service-specific Swagger file using the requests library.
   swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

   #You can download a service-specific Swagger file using the json library.
   with open('iris_swagger.json','w') as f:
      (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

   #Or, you can print just what you need from the Swagger file. 
   #This example gets the routing paths for the endpoints to be consumed.
   print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

   #You can also print input and output parameters as defined in the Swagger.io format
   print("Input")
   print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
   print("Output")
   print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))
   ```

3. 일부를 제공 하 여 서비스를 사용할 Iris 종 시점과 입력 합니다. 
   ```python
   #Make the request to consume the service using these flower_data inputs
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
   #Print the output
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))
   ```

## <a name="managing-the-services"></a>서비스 관리

웹 서비스를 만들었으므로 이제 업데이트를 삭제 하거나 해당 서비스를 다시 게시할 수 있습니다. R 서버 (또는 서버를 학습 하는 컴퓨터)를 사용 하 여 호스트 되는 모든 웹 서비스를 나열할 수 있습니다.

### <a name="update-a-web-service"></a>웹 서비스를 업데이트 합니다.

 이 예제에서는이 서비스를 사용할 수 있습니다 하는 사람에 게 유용한 설명을 추가 하려면 서비스를 업데이트 했습니다.

```python
#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)
```

코드, 모델, 설명, 입력, 출력을 변경 하려면 웹 서비스를 업데이트할 수 있습니다.

### <a name="publish-another-version"></a>다른 버전을 게시

이 예제에서는 서비스는 이제 반환 Iris 종 문자열 목록으로 대신 문자열입니다.

```python
#Publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))
```

동일한 웹 서비스의 여러 버전을 게시 하려면이 패턴을 사용할 수 있습니다. 

### <a name="list-services"></a>서비스 나열

이 샘플에는 다른 언어에서 또는 다른 사용자가 만든를 포함 하 여 모든 웹 서비스의 목록을 가져옵니다.

```python
#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
``` 

### <a name="delete-services"></a>서비스 삭제

이 예제에서는 방금 게시 하는 두 번째 웹 서비스 버전을 삭제 합니다.

```python
#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

만든 모든 서비스를 삭제할 수 있습니다. 적절 한 사용 권한을 가진 역할에 할당 된 경우에 다른 사용자의 서비스를 삭제할 수 있습니다.