---
title: 빅 데이터 클러스터에 응용 프로그램 사용
titleSuffix: SQL Server big data clusters
description: RESTful 웹 서비스 (미리 보기)를 사용 하 여 SQL Server 2019 빅 데이터 클러스터에 배포 된 응용 프로그램을 사용 합니다.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: jroth
manager: jroth
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a3894ccbd8ffda7cfe00d61a7a47622f7f481c8b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801895"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>RESTful 웹 서비스를 사용 하 여 SQL Server 빅 데이터 클러스터에 배포 된 앱 사용

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에는 RESTful 웹 서비스 (미리 보기)를 사용 하는 SQL Server 2019 빅 데이터 클러스터에 배포 된 앱을 사용 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [mssqlctl 명령줄 유틸리티](deploy-install-mssqlctl.md)
- 앱 중 하나를 사용 하 여 배포할 [ `mssqlctl` ](big-data-cluster-create-apps.md) 또는 [확장 앱 배포](app-deployment-extension.md)

## <a name="capabilities"></a>Capabilities

SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 응용 프로그램을 배포한 후에 액세스 하 고 RESTful 웹 서비스를 사용 하 여 해당 응용 프로그램을 사용할 수 있습니다. 이 통해 다른 응용 프로그램 또는 서비스 (예: 모바일 앱 또는 웹 사이트)에서 해당 앱의 통합. 다음 표에서 사용할 수 있는 응용 프로그램 배포 명령을 **mssqlctl** RESTful 웹 서비스 앱에 대 한 정보를 가져옵니다.

|Command |Description |
|:---|:---|
|`mssqlctl app describe` | 응용 프로그램에 설명 합니다. |

사용 하 여 도움말을 볼 수는 `--help` 다음 예제와 같이 매개 변수:

```bash
mssqlctl app describe --help
```

다음 섹션에서는 응용 프로그램에 대 한 끝점을 검색 하는 방법 및 응용 프로그램 통합에 대 한 RESTful 웹 서비스를 사용 하는 방법을 설명 합니다.

## <a name="retrieve-the-endpoint"></a>끝점 검색

합니다 **mssqlctl 앱 설명** 명령은 클러스터의 끝점을 포함 하 여 앱에 대 한 자세한 정보를 제공 합니다. 일반적으로 swagger 클라이언트 및 웹 서비스를 사용 하 여 RESTful 방식으로 앱과 상호 작용 하는 앱을 빌드하는 앱 개발자가 사용 됩니다.

다음과 유사한 명령을 실행 하 여 앱을 설명 합니다.

```bash
mssqlctl app describe --name addpy --version v1
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

IP 주소를 적어둡니다 (`10.1.1.3` 이 예에서) 및 포트 번호 (`30777`) 출력에서 합니다.

## <a name="generate-a-jwt-access-token"></a>JWT 액세스 토큰을 생성 합니다.

배포한 경우 앱에 대 한 RESTful 웹 서비스에 액세스 하려면 먼저 JWT 액세스 토큰을 생성 해야 합니다. 다음 URL을 브라우저에서 엽니다. `https://[IP]:[PORT]/api/docs/swagger.json` IP 주소 및 포트 실행 검색을 사용 하 여는 `describe` 위의 명령입니다. 에 사용한 동일한 자격 증명을 사용 하 여 로그인 해야 `mssqlctl login`합니다.

내용을 붙여 합니다 `swagger.json` 에 [Swagger 편집기](https://editor.swagger.io) 어떤 메서드를 사용할 수를 이해 하려면:

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

표시 된 `app` GET 메서드 뿐만 `token` POST 메서드. 토큰을 가져올 내를 사용 하 여 선호 하는 도구에 대 한 POST 호출 해야 하므로 JWT 토큰을 사용 하 여 앱에 대 한 인증을 `token` 메서드. 는 작업을 수행 하는 방법의 예로 [Postman](https://www.getpostman.com/):

![Postman 토큰](media/big-data-cluster-consume-apps/postman_token.png)

이 요청의 결과 알려는 JWT `access_token`에 앱을 실행 하는 URL을 호출 해야 합니다.

## <a name="execute-the-app-using-the-restful-web-service"></a>RESTful 웹 서비스를 사용 하 여 앱 실행

> [!NOTE]
> 원하는 경우에 대 한 URL을 열 수 있습니다는 `swagger` 실행 했을 때 반환 않은 `mssqlctl app describe --name [appname] --version [version]` 브라우저에서는 비슷해야 `https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`. 에 사용한 동일한 자격 증명을 사용 하 여 로그인 해야 `mssqlctl login`합니다. 콘텐츠를 `swagger.json` 붙여넣을 수 있습니다 [Swagger 편집기](https://editor.swagger.io)합니다. 웹 서비스를 노출 하는 표시 됩니다는 `run` 메서드. 또한 note 위쪽에 표시 되는 기본 URL입니다.

선호 하는 도구를 사용 하 여 호출 하는 `run` 메서드 (`https://[IP]:30778/api/app/[appname]/[version]/run`)를 json으로 POST 요청의 본문에 매개 변수를 전달 합니다. 이 예제에서는 사용 하 여 [Postman](https://www.getpostman.com/)합니다. 호출 하기 전에 설정 해야 합니다는 `Authorization` 에 `Bearer Token` 앞서 검색 한 토큰에 붙여넣습니다. 요청에서 헤더를 설정 합니다. 아래 스크린샷을 참조 하세요.

![Postman 실행 헤더](media/big-data-cluster-consume-apps/postman_run_1.png)

다음으로, 요청 본문에 매개 변수를 전달할를 호출 하 고 설정 앱에는 `content-type` 에 `application/json`:

![Postman 본문 실행](media/big-data-cluster-consume-apps/postman_run_2.png)

요청을 보내면 하면 동일한 출력을 통해 앱을 실행 했을 때 수행한 것 처럼 `mssqlctl app run`:

![Postman 실행 결과](media/big-data-cluster-consume-apps/postman_result.png)

이제 웹 서비스를 통해 앱을 성공적으로 호출 했습니다. 응용 프로그램에서이 웹 서비스를 통합 하는 유사한 단계를 따르면 됩니다.

## <a name="next-steps"></a>다음 단계

추가 샘플에서 확인할 수 있습니다 [응용 프로그램 배포 샘플](https://aka.ms/sql-app-deploy)합니다.

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
