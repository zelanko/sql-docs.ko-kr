---
title: 확장성을 통해 추가 기능 추가
titleSuffix: Azure Data Studio
description: 확장성 모델 및 Azure Data Studio의 기능을 확장 하는 것에 대 한 핵심 확장 영역에 대해 알아봅니다
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b595a353859ed7d69ccb6ad61ef6e5dc2a7073f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238989"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>시작 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 확장성

[!INCLUDE[name-sos](../includes/name-sos.md)] 사용자 환경을 사용자 지정 하 여 전체 사용자 커뮤니티에 게 사용자 지정 항목을 제공 하는 몇 가지 확장성 메커니즘에 있습니다. 핵심 [!INCLUDE[name-sos](../includes/name-sos.md)] 플랫폼이 대부분의 Visual Studio Code 확장성 Api 사용할 수 있도록 Visual Studio 코드를 기반으로 빌드됩니다. 또한 데이터 관리 관련 활동에 대 한 추가 확장성 지점을 제공 했습니다.

핵심 확장 요소는 다음과 같습니다.

- Visual Studio Code 확장성 Api
- Azure Data Studio 확장 제작 도구
- 대시보드 탭 패널 기여를 관리 합니다.
- 작업 환경 사용 하 여 정보
- Azure Data Studio 확장성 Api
- 사용자 지정 데이터 공급자 Api

## <a name="visual-studio-code-extensibility-apis"></a>Visual Studio Code 확장성 Api

때문에 핵심 [!INCLUDE[name-sos](../includes/name-sos.md)] Visual Studio Code 기반 플랫폼, Visual Studio Code 확장 Api에 대 한 자세한 내용은 합니다 [확장 제작](https://code.visualstudio.com/docs/extensions/overview) 하 고 [확장 API](https://code.visualstudio.com/docs/extensionAPI/overview) Visual Studio Code 웹 사이트에 대 한 설명서입니다.

## <a name="manage-dashboard-tab-panel-contributions"></a>대시보드 탭 패널 기여를 관리 합니다.

세부 정보를 참조 하세요 [기여 지점을](#contribution-points) 하 고 [컨텍스트 변수](#context-variables)합니다.

## <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 확장성 Api

자세한 내용은 참조 하세요 [확장성 Api](extensibility-apis.md)합니다.


## <a name="contribution-points"></a>기여 지점

이 섹션에서는 package.json 확장 매니페스트에 정의 된 다양 한 기여 지점에 설명 합니다.

IntelliSense는 azuredatastudio 내에서 지원 됩니다.

## <a name="contributes-dashboard"></a>대시보드를 제공합니다.

탭, 컨테이너, 대시보드에 대 한 정보 위젯 영향을 줍니다.

![대시보드](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.tabs는 대시보드 페이지에 있는 탭 섹션을 만듭니다. 개체 또는 개체의 배열을 것으로 예상 합니다.  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        ...
    }
}
]
```

`dashboard.containers`

대신 (내부 dashboard.tab) 대시보드 컨테이너 인라인을 지정 합니다. Dashboard.containers를 사용 하 여 컨테이너를 등록할 수 있습니다. 개체 또는 개체의 배열을 수락합니다.

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        ...
    }
},
{
    "id": "innerTab2",
    "container": {
       ...
    }
}
]
```

등록 된 컨테이너를 참조 하려면 컨테이너의 id를 지정 합니다.

```json
"dashboard.tabs": [
{
    ...
    "container": {
        "innerTab1": {             
        }
    }
}
]

```

`dashboard.insights`

Insights dashboard.insights를 사용 하 여 등록할 수 있습니다. 이 비슷합니다 [자습서: 빌드 사용자 지정 정보 위젯](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

```json
"dashboard.insights": {
"id": "my-widget"
"type": {
    "count": {
        "dataDirection": "vertical",
        "dataType": "number",
        "legendPosition": "none",
           "labelFirstColumn": false,
        "columnsAsLabels": false
       }
   },
   "queryFile": "{your file folder}/activeSession.sql"
}
```


### <a name="dashboard-container-types"></a>대시보드 컨테이너 유형

현재 네 가지 지원 되는 컨테이너 유형:

1. `widgets-container`

    ![위젯 컨테이너](media/extensibility/widgets-container.png)

    목록 컨테이너에 표시 되는 위젯입니다. 선형 레이아웃의 경우 위젯 목록을 허용합니다.

    ```json
    "container": {
        "widgets-container": [
        {
            "widget": {
                "query-data-store-db-insight": {
                }
            }
        },
        {
            "widget": {
                "explorer-widget": {
                }
            }
        }
      ]
    }
    ```

2. `webview-container`

    ![webview 컨테이너](media/extensibility/webview-container.png)

    Webview 전체 컨테이너에 표시 됩니다. Webview id 탭 ID가 동일한 것으로 예상

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![표 컨테이너](media/extensibility/grid-container.png)

   위젯 또는 표 레이아웃에 표시 되는 웹 보기로 목록

    ```json
    "container": {
        "grid-container": [
        {
            "name": "widget 1",
            "widget": {
                "explorer-widget": {
                }
            },
            "row":0,
            "col":0
        },
        {
            "name": "widget 2",
            "widget": {
                "tasks-widget": {
                    "backup", 
                    "restore",
                    "configureDashboard",
                    "newQuery"
                }
            },
            "row":0,
            "col":1
        },
        {
            "name": "Webview 1",
            "webview": {
                "id": "google"
            },
            "row":1,
            "col":0,
            "colspan":2
        },
        {
            "name": "widget 3",
            "widget": {
                "explorer-widget": {}
            },
            "row":0,
            "col":3,
            "rowspan":2
        },
    ]
    ```

4.  `nav-section`

    ![nav 섹션](media/extensibility/nav-section.png)

    컨테이너에 표시할 탐색 섹션

    ```json
    "container": {
        "nav-section": [
            {
                "id": "innerTab1",
                "title": "inner-tab1",
                "icon": {
                    "light": "./icons/tab1Icon.svg",
                    "dark": "./icons/tab1Icon_dark.svg"
                }
                "container": {
                    ...
                }
            },
            {
                "id": "innerTab2",
                "title": "inner-tab2",
                "icon": {
                    "light": "./icons/tab2Icon.svg",
                    "dark": "./icons/tab2Icon_dark.svg"
                }
                "container": {
                    ...
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>컨텍스트 변수

Visual Studio Code 및 Azure Data Studio 이후에 컨텍스트에 대 한 일반적인 정보를 참조 하세요 [확장성](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example)합니다.

Azure Data Studio 확장에 대 한 사용 가능한 데이터베이스 연결에 대 한 특정 상황에 맞는 했습니다.

### <a name="dashboard"></a>대시보드

대시보드에서 다음 상황에 맞는 변수를 제공합니다.

|컨텍스트 변수| description|
|:---|:---|
|`connectionProvider` | 문자열은 현재 연결의 공급자에 대 한 식별자입니다. 예: `connectionProvider == 'MSSQL'`에서 분할된 테이블 또는 인덱스를 만들 수 있습니다.|
|`serverName`|문자열은 현재 연결의 서버 이름입니다. 예: `serverName == 'localhost'`에서 분할된 테이블 또는 인덱스를 만들 수 있습니다.|
|`databaseName` | 문자열의 현재 연결 데이터베이스 이름입니다. 예: `databaseName == 'master'`에서 분할된 테이블 또는 인덱스를 만들 수 있습니다.|
|`connection` | 현재 연결 (IConnectionProfile)에 대 한 전체 연결 프로필 개체|
|`dashboardContext` | 대시보드 페이지의 컨텍스트 문자열에서 현재은. 'Database' 또는 'server '입니다. 예: `dashboardContext == 'database'`|
