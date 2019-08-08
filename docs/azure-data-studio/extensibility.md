---
title: 확장성을 통해 추가 기능 추가
titleSuffix: Azure Data Studio
description: Azure Data Studio의 기능을 확장하기 위한 확장성 모델 및 핵심 확장 영역에 대해 알아보세요.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 20158894567c1452a8d605f5cec84354654c5e96
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959595"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] 확장 시작

[!INCLUDE[name-sos](../includes/name-sos.md)]에는 사용자 환경을 사용자 지정하고 해당 사용자 지정을 전체 사용자 커뮤니티에서 사용할 수 있도록 하는 여러 확장성 메커니즘이 있습니다. 핵심 [!INCLUDE[name-sos](../includes/name-sos.md)] 플랫폼은 Visual Studio Code를 토대로 구축되므로 대부분의 Visual Studio Code 확장성 API를 사용할 수 있습니다. 또한 데이터 관리 관련 활동에 대한 추가 확장 지점도 제공했습니다.

몇 가지 주요 확장 지점은 다음과 같습니다.

- Visual Studio Code 확장성 API
- Azure Data Studio 확장 작성 도구
- 대시보드 탭 패널 기여 관리
- 작업 환경을 포함하는 인사이트
- Azure Data Studio 확장성 API
- 사용자 지정 데이터 공급자 API

## <a name="visual-studio-code-extensibility-apis"></a>Visual Studio Code 확장성 API

핵심 [!INCLUDE[name-sos](../includes/name-sos.md)] 플랫폼은 Visual Studio Code를 토대로 구축되었으므로 Visual Studio Code 확장성 API에 대한 자세한 내용은 Visual Studio Code 웹 사이트의 [확장 작성](https://code.visualstudio.com/docs/extensions/overview) 및 [확장 API](https://code.visualstudio.com/docs/extensionAPI/overview) 설명서에 제공됩니다.

## <a name="manage-dashboard-tab-panel-contributions"></a>대시보드 탭 패널 기여 관리

자세한 내용은 [기여 지점](#contribution-points) 및 [컨텍스트 변수](#context-variables)를 참조하세요.

## <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 확장성 API

자세한 내용은 [확장성 API](extensibility-apis.md)를 참조하세요.


## <a name="contribution-points"></a>기여 지점

이 섹션에서는 package.json 확장 매니페스트에 정의된 다양한 기여 지점에 대해 설명합니다.

IntelliSense는 azuredatastudio 내에서 지원됩니다.

## <a name="contributes-dashboard"></a>기여 대시보드

대시보드에 탭, 컨테이너, 인사이트 위젯을 기여합니다.

![대시보드](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.tabs는 대시보드 페이지 내에 탭 섹션을 만듭니다. 개체 또는 개체 배열이 필요합니다.  

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

대시보드 컨테이너를 인라인으로(dashboard.tab 내에서) 지정하는 대신, dashboard.containers를 사용하여 컨테이너를 등록할 수 있습니다. 개체 또는 개체 배열을 수락합니다.

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

등록된 컨테이너를 참조하려면 컨테이너의 ID를 지정합니다.

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

dashboard.insights를 사용하여 인사이트를 등록할 수 있습니다. 이것은 [자습서: 사용자 지정 인사이트 위젯 빌드](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)와 비슷합니다.

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

현재 다음과 같은 4가지 컨테이너 유형이 지원됩니다.

1. `widgets-container`

    ![위젯 컨테이너](media/extensibility/widgets-container.png)

    컨테이너에 표시될 위젯 목록입니다. 흐름 레이아웃입니다. 위젯 목록을 허용합니다.

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

    ![웹 보기 컨테이너](media/extensibility/webview-container.png)

    웹 보기는 전체 컨테이너에 표시됩니다. 웹 보기 ID는 탭 ID와 동일해야 합니다.

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![그리드 컨테이너](media/extensibility/grid-container.png)

   그리드 레이아웃에 표시될 위젯 또는 웹 보기 목록입니다.

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

    ![탐색 섹션](media/extensibility/nav-section.png)

    탐색 섹션이 컨테이너에 표시됩니다.

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

Visual Studio Code 및 이후에 제공된 Azure Data Studio의 컨텍스트에 대한 일반 정보는 [확장성](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example)을 참조하세요.

Azure Data Studio에서 확장에 데이터베이스 연결과 관련된 특정 컨텍스트를 사용할 수 있습니다.

### <a name="dashboard"></a>대시보드

대시보드에서는 다음 컨텍스트 변수를 제공합니다.

|컨텍스트 변수| description|
|:---|:---|
|`connectionProvider` | 현재 연결 공급자의 식별자 문자열입니다. 예: `connectionProvider == 'MSSQL'`입니다.|
|`serverName`|현재 연결의 서버 이름 문자열입니다. 예: `serverName == 'localhost'`입니다.|
|`databaseName` | 현재 연결의 데이터베이스 이름 문자열입니다. 예: `databaseName == 'master'`입니다.|
|`connection` | 현재 연결의 전체 연결 프로필 개체(IConnectionProfile)입니다.|
|`dashboardContext` | 대시보드의 페이지 컨텍스트 문자열이 현재 설정되어 있습니다. 'database' 또는 'server'입니다. 예: `dashboardContext == 'database'`|
