---
title: 애플리케이션 사용
titleSuffix: SQL Server Big Data Clusters
description: RESTful 웹 서비스를 사용하여 SQL Server 빅 데이터 클러스터에 배포된 애플리케이션을 사용합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 307d1cf41c319debad4b0fc06b8ba0da516491bd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257323"
---
# <a name="consume-an-app-deployed-on-big-data-clusters-2019-using-a-restful-web-service"></a>RESTful 웹 서비스를 사용하여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 배포된 앱을 사용합니다.

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 RESTful 웹 서비스를 사용하여 SQL Server 빅 데이터 클러스터에 배포된 앱을 사용하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 빅 데이터 클러스터](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)
- [azdata](app-create.md) 또는 [앱 배포 확장](app-deployment-extension.md)을 사용하여 배포된 앱

> [!NOTE]
> 애플리케이션의 yaml 사양 파일에서 일정을 지정하는 경우 애플리케이션은 cron 작업을 통해 트리거됩니다. 빅 데이터 클러스터가 OpenShift에 배포되는 경우 cron 작업을 시작하려면 추가 기능이 필요합니다. 특정 지침은 [OpenShift의 보안 고려 사항](concept-application-deployment.md#app-deploy-security) 관련 세부 정보를 참조하세요.

## <a name="capabilities"></a>기능

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에 애플리케이션을 배포한 후에 RESTful 웹 서비스를 사용하여 해당 애플리케이션에 액세스하고 사용할 수 있습니다. 이 기능을 사용하면 다른 애플리케이션 또는 서비스(예: 모바일 앱 또는 웹 사이트)에서 해당 앱을 통합할 수 있습니다. 다음 표에서는 앱의 RESTful 웹 서비스에 대한 정보를 가져오기 위해 **azdata**와 함께 사용할 수 있는 애플리케이션 배포 명령을 설명합니다.

|명령 |설명 |
|:---|:---|
|`azdata app describe` | 애플리케이션을 설명합니다. |

다음 예제와 같이 `--help` 매개 변수를 사용하여 도움말을 볼 수 있습니다.

```bash
azdata app describe --help
```

다음 섹션에서는 애플리케이션의 엔드포인트를 검색하는 방법 및 애플리케이션 통합을 위해 RESTful 웹 서비스를 사용하는 방법을 설명합니다.

## <a name="retrieve-the-endpoint"></a>엔드포인트 검색

BDC(빅 데이터 클러스터)는 RESTful 웹 서비스를 사용하여 해당 애플리케이션에 액세스하고 사용할 수 있는 엔드포인트를 제공합니다. 기본 목적은 해당 마이크로 서비스 아키텍처에 보다 적극적으로 대응하여 다른 웹 또는 모바일 애플리케이션과의 상호 작용을 용이하게 만드는 것입니다. **azdata app describe** 명령은 클러스터의 엔드포인트를 포함하여 앱에 대한 자세한 정보를 제공합니다. 이 정보는 일반적으로 앱 개발자가 Swagger 클라이언트 및 RESTful 방식으로 앱과 상호 작용하는 웹 서비스를 사용하여 앱을 빌드하는 데 사용됩니다.

다음 예제와 비슷한 명령을 실행하여 앱을 설명합니다.

```bash
azdata app describe --name add-app --version v1
```

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/app/addpy/v1",
    "swagger": "https://10.1.1.3:30080/app/addpy/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

출력된 IP 주소(이 예제에서는 `10.1.1.3`)와 포트 번호(`30080`)를 적어 둡니다.

나열된 서비스의 엔드포인트를 찾을 수 있는 Azure Data Studio 서버에서 관리를 마우스 오른쪽 단추로 클릭해도 이 정보를 볼 수 있습니다.

![ADS 엔드포인트](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>JWT 액세스 토큰 생성

배포한 앱의 RESTful 웹 서비스에 액세스하려면 먼저 JWT 액세스 토큰을 생성해야 합니다. 액세스 토큰의 URL은 빅 데이터 클러스터의 버전에 따라 달라집니다. 

|버전 |URL|
|------------|------|
|GDR1|  `https://[IP]:[PORT]/docs/swagger.json`|
|CU1 이상| `https://[IP]:[PORT]/api/v1/swagger.json`|

 위의 예제에 나온 CU4 릴리스, 컨트롤러의 IP 주소(예에서는 10.1.1.3), 포트 번호(30080)의 출력에서 URL은 다음과 같습니다. 
 
 ```bash
    https://10.1.1.3 :30080/api/v1/swagger.json
```
 
> 버전 정보는 [릴리스 기록](release-notes-big-data-cluster.md#release-history)을 참조하세요.

위에서 [`describe`](#retrieve-the-endpoint) 명령을 실행하여 검색한 IP 주소와 포트를 사용해 브라우저에서 적절한 URL을 엽니다. `azdata login`에 사용한 것과 동일한 자격 증명으로 로그인합니다.

`swagger.json`의 내용을 [Swagger 편집기](https://editor.swagger.io)에 붙여넣어 사용할 수 있는 메서드를 파악합니다.

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

`app`은 GET 메서드이며 `token`을 가져오려면 POST 메서드를 사용합니다. 앱 인증에서 JWT 토큰을 사용하기 때문에 `token` 메서드에 대한 POST 호출을 수행하려면 원하는 도구를 사용하여 토큰을 가져와야 합니다. 동일한 예제에서 JWT 토큰을 가져오는 URL은 다음과 같습니다.

 ```bash
    https://10.1.1.3 :30080/api/v1/token
```


다음은 [Postman](https://www.getpostman.com/)에서 이 작업을 수행하는 방법의 예제입니다.

![Postman 토큰](media/big-data-cluster-consume-apps/postman_token.png)


이 요청의 출력을 통해 앱을 실행하기 위해 URL을 호출하는 데 필요한 JWT `access_token`을 얻을 수 있습니다.

## <a name="execute-the-app-using-the-restful-web-service"></a>RESTful 웹 서비스를 사용하여 앱 실행

BDC에서 앱을 사용하는 다양한 방법이 있습니다. [azdata 앱 실행 명령](app-create.md)을 사용하도록 선택할 수 있습니다. 이 섹션에서는 Postman 같은 일반적인 개발자 도구를 사용하여 앱을 실행하는 방법을 보여 줍니다. 

브라우저에서 `azdata app describe --name [appname] --version [version]`을 실행했을 때 반환된 `swagger`의 URL을 열 수 있습니다. 이 URL은 `https://[IP]:[PORT]/app/[appname]/[version]/swagger.json`과 유사합니다. 

> [!NOTE]
> `azdata login`에 사용한 것과 동일한 자격 증명으로 로그인해야 합니다. 동일한 예에서 명령은 다음과 같습니다.

 ```bash
    azdata app describe --name add-app --version v1
```

`swagger.json`의 내용을 [Swagger 편집기](https://editor.swagger.io)에 붙여넣을 수 있습니다. 웹 서비스가 `run` 메서드를 노출하고 그 아래로 애플리케이션 프록시를 통과했음을 확인할 수 있습니다. 애플리케이션 프록시는 사용자를 인증한 후 요청을 애플리케이션으로 라우팅하는 웹 API입니다. 맨 위에 기준 URL이 표시됩니다. 원하는 도구를 통해 `run` 메서드(`https://[IP]:30778/api/app/[appname]/[version]/run`)를 호출하고 POST 요청의 본문에 있는 매개 변수를 json으로 전달할 수 있습니다. 


이 예제에서는 [Postman](https://www.getpostman.com/)을 사용합니다. 호출하기 전에 `Authorization`을 `Bearer Token`으로 설정하고 앞에서 검색한 토큰을 붙여넣어야 합니다. 이렇게 하면 요청에 헤더가 설정됩니다. 아래 스크린샷을 참조하세요.

![Postman 실행 헤더](media/big-data-cluster-consume-apps/postman_run_1.png)

다음으로, 요청 본문에서 호출하는 앱에 매개 변수를 전달하고 `content-type`을 `application/json`으로 설정합니다.

![Postman 실행 본문](media/big-data-cluster-consume-apps/postman_run_2.png)

요청을 보내면 `azdata app run`을 통해 앱을 실행했을 때와 동일한 출력이 표시됩니다.

![Postman 실행 결과](media/big-data-cluster-consume-apps/postman_result.png)

이제 웹 서비스를 통해 앱을 성공적으로 호출했습니다. 비슷한 단계를 수행하여 이 웹 서비스를 애플리케이션에 통합할 수 있습니다.


## <a name="next-steps"></a>다음 단계

[빅 데이터 클러스터에서 애플리케이션을 모니터링](app-monitor.md)하는 방법을 자세히 알아봅니다. [앱 배포 샘플](https://aka.ms/sql-app-deploy)에서 추가 샘플을 확인할 수도 있습니다.

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요](big-data-cluster-overview.md)를 참조하세요.