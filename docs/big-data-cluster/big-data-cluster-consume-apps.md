---
title: 빅 데이터 클러스터에서 응용 프로그램 사용
titleSuffix: SQL Server big data clusters
description: RESTful 웹 서비스 (미리 보기)를 사용 하 여 SQL Server 2019 빅 데이터 클러스터에 배포 된 응용 프로그램을 사용 합니다.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a2135ef64fb17eba62eab75b81739eda047167ab
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419512"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>RESTful 웹 서비스를 사용 하 여 빅 데이터 클러스터 SQL Server에 배포 된 앱 사용

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 RESTful 웹 서비스 (미리 보기)를 사용 하 여 SQL Server 2019 빅 데이터 클러스터에 배포 된 앱을 사용 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [mssqlctl 명령줄 유틸리티](deploy-install-azdata.md)
- [Azdata](big-data-cluster-create-apps.md) 또는 [앱 배포 확장](app-deployment-extension.md) 중 하나를 사용 하 여 배포 된 앱

## <a name="capabilities"></a>Capabilities

SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 응용 프로그램을 배포한 후에는 RESTful 웹 서비스를 사용 하 여 해당 응용 프로그램에 액세스 하 고 해당 응용 프로그램을 사용할 수 있습니다. 이렇게 하면 해당 앱을 다른 응용 프로그램 또는 서비스 (예: 모바일 앱 또는 웹 사이트)와 통합할 수 있습니다. 다음 표에서는 **azdata** 에서 앱에 대 한 RESTful 웹 서비스에 대 한 정보를 가져오는 데 사용할 수 있는 응용 프로그램 배포 명령을 설명 합니다.

|Command |설명 |
|:---|:---|
|`azdata app describe` | 응용 프로그램을 설명 합니다. |

다음 예제와 같이 `--help` 매개 변수를 사용 하 여 도움을 받을 수 있습니다.

```bash
azdata app describe --help
```

다음 섹션에서는 응용 프로그램에 대 한 끝점을 검색 하는 방법 및 응용 프로그램 통합을 위해 RESTful 웹 서비스를 사용 하는 방법을 설명 합니다.

## <a name="retrieve-the-endpoint"></a>끝점 검색

**Azdata app 설명** 명령은 클러스터의 끝점을 포함 하 여 앱에 대 한 자세한 정보를 제공 합니다. 이는 일반적으로 앱 개발자가 swagger 클라이언트를 사용 하 여 앱을 빌드하고 RESTful 방식으로 앱과 상호 작용 하는 웹 서비스를 사용 하는 데 사용 됩니다.

다음과 비슷한 명령을 실행 하 여 앱을 설명 합니다.

```bash
azdata app describe --name addpy --version v1
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
    "app": "https://10.1.1.3:30777/api/app/addpy/v1",
    "swagger": "https://10.1.1.3:30777/api/app/addpy/v1/swagger.json"
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

출력의 IP 주소 (`10.1.1.3` 이 예에서는)와 포트 번호 (`30777`)를 적어둡니다.

## <a name="generate-a-jwt-access-token"></a>JWT 액세스 토큰 생성

배포한 앱에 대 한 RESTful 웹 서비스에 액세스 하려면 먼저 JWT 액세스 토큰을 생성 해야 합니다. 위의 `https://[IP]:[PORT]/api/docs/swagger.json` 명령을`describe` 실행 하 여 검색 한 IP 주소 및 포트를 사용 하 여 브라우저에서 다음 URL을 엽니다. 에 `azdata login`사용한 것과 동일한 자격 증명을 사용 하 여 로그인 해야 합니다.

의 내용을 `swagger.json` [Swagger 편집기](https://editor.swagger.io) 에 붙여넣어 사용할 수 있는 메서드를 이해 합니다.

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

GET 메서드 및 `token` POST 메서드를 확인 합니다. `app` 앱에 대 한 인증에서 JWT 토큰을 사용 하기 때문에 `token` 메서드에 대 한 POST 호출을 수행 하려면 선호 하는 도구를 사용 하 여 토큰을 받아야 합니다. [Postman](https://www.getpostman.com/)에서이 작업을 수행 하는 방법의 예는 다음과 같습니다.

![Postman 토큰](media/big-data-cluster-consume-apps/postman_token.png)

이 요청의 결과는 JWT `access_token`를 제공 하므로 앱을 실행 하기 위해 URL을 호출 해야 합니다.

## <a name="execute-the-app-using-the-restful-web-service"></a>RESTful 웹 서비스를 사용 하 여 앱 실행

> [!NOTE]
> 원하는 경우 브라우저에서 실행 `swagger` `azdata app describe --name [appname] --version [version]` 될 때 반환 된의 URL을 열 수 있습니다 `https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`.이 URL은와 유사 합니다. 에 `azdata login`사용한 것과 동일한 자격 증명을 사용 하 여 로그인 해야 합니다. 의 `swagger.json` 내용은 [Swagger 편집기](https://editor.swagger.io)에 붙여넣을 수 있습니다. 웹 서비스에서 메서드를 `run` 노출 하는 것을 볼 수 있습니다. 또한 맨 위에 기본 URL이 표시 됩니다.

자주 사용 하는 도구를 사용 하 여 `run` 메서드 (`https://[IP]:30778/api/app/[appname]/[version]/run`)를 호출 하 고 POST 요청의 본문에 있는 매개 변수를 json으로 전달할 수 있습니다. 이 예제에서는 [Postman](https://www.getpostman.com/)을 사용 합니다. 호출을 수행 하기 전에 `Authorization` 를로 `Bearer Token` 설정 하 고 이전에 검색 한 토큰에 붙여 넣어야 합니다. 이렇게 하면 요청에 헤더가 설정 됩니다. 아래 스크린샷을 참조 하세요.

![Postman 실행 헤더](media/big-data-cluster-consume-apps/postman_run_1.png)

그런 다음 요청 본문에서 호출 하는 앱에 매개 변수를 전달 하 고를로 `content-type` `application/json`설정 합니다.

![Postman 실행 본문](media/big-data-cluster-consume-apps/postman_run_2.png)

요청을 보낼 때 다음을 통해 `azdata app run`앱을 실행할 때와 같은 출력을 얻게 됩니다.

![Postman 실행 결과](media/big-data-cluster-consume-apps/postman_result.png)

이제 웹 서비스를 통해 응용 프로그램을 성공적으로 호출 했습니다. 비슷한 단계를 수행 하 여이 웹 서비스를 응용 프로그램에 통합할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[앱 배포 샘플](https://aka.ms/sql-app-deploy)에서 추가 샘플을 확인할 수도 있습니다.

빅 데이터 클러스터 SQL Server 하는 방법에 대 한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
