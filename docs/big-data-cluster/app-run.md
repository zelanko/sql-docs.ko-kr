---
title: azdata를 사용하여 애플리케이션 실행
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터에서 azdata를 사용하여 애플리케이션을 실행합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 08/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e8c603040c0b5df9440e3aaabadac0d947315310
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88681083"
---
# <a name="run-apps-with-azdata---sql-server-big-data-clusters"></a>azdata를 사용하여 앱 실행 - SQL Server 빅 데이터 클러스터

이 문서에서는 SQL Server 빅 데이터 클러스터 내에서 애플리케이션을 실행하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [azdata 명령줄 유틸리티](deploy-install-azdata.md)

## <a name="capabilities"></a>기능

SQL Server 2019에서 애플리케이션을 만들고, 삭제, 설명, 초기화, 나열, 실행 및 업데이트할 수 있습니다. 다음 표에서는 **azdata**와 함께 사용할 수 있는 애플리케이션 배포 명령을 설명합니다.

|명령 |설명 |
|:---|:---|
|`azdata app describe` | 애플리케이션을 설명합니다. |
|`azdata app run` | 애플리케이션을 실행합니다. |


다음 섹션에서는 이러한 명령을 자세히 설명합니다.


## <a name="run-an-app"></a>앱 실행

앱이 `Ready` 상태이면 지정된 입력 매개 변수와 함께 실행하여 앱을 사용할 수 있습니다. 다음 구문을 사용하여 앱을 실행합니다.

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

다음 예제 명령은 run 명령을 보여 줍니다.

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

실행이 성공적으로 완료되면 앱을 만들 때 지정한 대로 출력됩니다. 다음은 출력 예제입니다.

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```


## <a name="describe-an-app"></a>앱 설명

describe 명령은 클러스터의 엔드포인트를 포함하여 앱에 대한 자세한 정보를 제공합니다. 이 정보는 일반적으로 앱 개발자가 Swagger 클라이언트 및 RESTful 방식으로 앱과 상호 작용하는 웹 서비스를 사용하여 앱을 빌드하는 데 사용됩니다. 자세한 내용은 [빅 데이터 클러스터에서 애플리케이션 사용](app-consume.md)을 참조하세요.

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
    "app": "https://10.1.1.3:30080/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30080/api/app/add-app/v1/swagger.json"
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

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 배포된 앱을 고유한 애플리케이션에 통합하는 방법을 살펴봅니다. 자세한 내용은 [빅 데이터 클러스터에서 애플리케이션 사용](app-consume.md)을 참조하세요. [앱 배포 샘플](https://aka.ms/sql-app-deploy)에서 추가 샘플을 확인할 수도 있습니다.

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
