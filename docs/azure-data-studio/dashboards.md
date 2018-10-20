---
title: Insights 및 Azure Data Studio의 일반적인 작업에 빠르게 액세스 | Microsoft Docs
description: Azure Data Studio 통찰력 있는 위젯을 표시 하는 방법을 알아봅니다.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: b163d110353d07811f0feb991772c90053651659
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356196"
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>대시보드 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

대시보드, 마우스 오른쪽 단추로 클릭은 서버 또는 데이터베이스를 표시 하 고 선택 **관리**합니다.

![샘플 대시보드](media/dashboards/sample-dashboard.png)

**서버 속성** 버전, 버전, 컴퓨터 이름 및 OS 버전을 포함 하 여 서버 속성을 포함 합니다.

**작업** commons 작업 복원 등 새 쿼리를 포함 합니다.

**데이터베이스 검색** 쉽게 테이블을 포함 하 여 서버에 저장 된 기존 데이터베이스를 조회 합니다.

**백업 상태** 쉽게 기존 데이터베이스에 대 한 백업 상태를 조회 합니다.

## <a name="configuring-insight-widgets"></a>정보 위젯 구성
대시보드를 찾을 수 있는 설정에 대 한 자습서를 따르는 것이 좋습니다 [여기](tutorial-build-custom-insight-sql-server.md)합니다.

또한 체크 아웃 해야 합니다 [정보 위젯 구성에서 방법]()합니다.

이 자습서에서는 다음에 읽은 후에 대해 자세히 알아보려면 자습서에서 다루지 않는 특정 위젯입니다.

## <a name="insight-detail"></a>세부 정보
Insight 세부 정보 플라이 아웃 관련된 정보 위젯에 대 한 자세한 정보를 제공합니다. 
- 에 대 한 정보 위젯 개수, 선, 차트 등을 일목요연 요약 보기를 렌더링합니다. 
- Insight 세부 정보 플라이 아웃 "드릴" 세부 정보를 나열 하는 높은 수준의 정보 위젯에 나열 된 각 항목에 대 한 더 심층적인 데이터 통찰력을 제공 합니다. 
  - 세부 정보 플라이 아웃 내용은 기본 위젯의 쿼리를 별도 SQL 쿼리를 사용 하 여 정의 됩니다. 

Insight 세부 정보 쿼리를 사용 하는 집합 않아도 이지만 레이아웃 표준입니다.
- 보기의 위쪽 절반은 항상 2 열 "요약" 뷰입니다. JSON 구성의 "레이블" 및 "value" 속성으로 정의 된 열을 사용 하 여
- 요약 테이블에서 행을 클릭 하 여, 아래쪽 플라이 아웃의 절반 표시 전체 집합을 해당 행에 대 한 열 정보입니다.

### <a name="insight-detail-configuration-in-packagejson"></a>Package.json에서 정보 활용 세부 정보 구성

샘플 정보 정보 플라이 아웃 구성
```json
"details": {
    "queryFile": "./relative_path_to_sqlfile_from_package_json_file.sql",
    "label": {
        "icon": "database",
        "column": "first_column_name_for_summary_list_view",
        "state": [
            {
                "condition": {
                    "if": "equals",
                    "equals": "0"
                },
                "color": "red"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "1"
                },
                "color": "orange"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "2"
                },
                "color": "green"
            }
        ]
    },
    "value": "second_column_and_condition_check_value_column_for_summary_list_view",
```
|속성|유형|value|기본값|description|comment|
|:---|:---|:---|:---|:---|:---|
|자세히|json 개체|||해당 구조 내에서 세부 정보 정의 대 한 정보를 정의 하는 필수 속성||
|queryFile|string|||insight 세부 정보 sql 쿼리 파일 경로 및 package.json의 위치에 상대적인 파일 이름||
|레이블|json 개체|||각 품목 요약 목록 뷰에서 정의할 필수 속성|나중에 'summaryList'와 같은 변경 하려면이 속성의 이름|
|아이콘|string|||각 요약 목록 보기 항목에 대 한 reder 아이콘 이름을 나타냅니다.|지원 되는 아이콘 목록 (tbd) 문서화 됩니다.|
|column|string|||쿼리 결과 집합에서 요약 목록 보기에서 첫 번째 열의 이름을 나타냅니다.|이 속성의 이름은 보다 알기 쉬운 이름으로 변경 됩니다 나중에|
|value|string|||쿼리 결과 집합에서 요약 목록 보기에서 두 번째 열의 이름을 표시 합니다. 이 열의 값은 조건을 확인 하 고 각 요약 목록 뷰 항목의 색 점 색을 설정 하는 데 사용 됩니다.|직관적으로이 속성의 이름이 변경 되는 나중에|
|condition(조건)|json 개체|||열 값에 대 한 조건 검사를 정의 하 고 각 요약 목록 보기 항목에 대 한 색을 결정||
|if|string|항상 equals, notEquals, greaterThan, lessThan, greaterThanOrEqauls, lessThanOrEquals||조건 확인 연산자|운영자에 게 속성 이름이 변경 되는 나중에|
|equals|string|||조건 확인 값|이 속성 이름 'value'으로 변경 됩니다 나중에|

## <a name="insight-actions"></a>Insight 작업
정보 위젯 및 insight 세부 정보를 사용 하 여 쉽게 문제를 완화 하거나 관리 하는 작업 계획을 가져올 수 있습니다. 예를 들어는 DBCC CHECKDB를 실행 생각할 오류 로그를 읽을 또는 데이터베이스를 복구 보류 중 상태인 경우 데이터베이스를 복원 합니다. 또는 수행 하려는 작업 중 하나일 수 있습니다.

사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 Insight 작업 구성을 복원 하거나 sql 스크립트를 사용 하 여 정의 된 고유한 동작을 제공 하는 등 기본 제공 작업을 매핑할 수 있습니다.

> Sql 스크립트를 사용 하 여 사용자 지정 작업의 구성을 개발 중 이며 아직 비공개 미리 보기 빌드에 사용할 수 없는 합니다.

## <a name="sample-insight-action-definition"></a>샘플 정보 작업 정의

```"actions"{}``` insight 작업을 정의합니다. 작업을 특정 범위에 대해 같은 정의할 수 있습니다 ```"server"```, ```"database"``` 등 및 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 동작에 현재 연결 컨텍스트 정보를 전달 합니다. 

복원 작업 WideWorldImporters 데이터베이스에 대 한 시작 될 때에 예를 들어 ```"database": "${Database}"``` 전달할 정의 나타냅니다 ```Database``` 복원 작업에 쿼리 결과의 열 값입니다. 그러면 데이터베이스에 대 한 복원 작업 시작합니다. ```"types"``` json 배열 및 배열에 여러 작업을 나열할 수 있습니다. 상황에 맞는 메뉴를 기본적으로 되기 Insight 세부 정보 대화 상자에서 해당 사용자 수 클릭 하 고 작업을 수행 합니다. 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] "백업", "restore", "새 쿼리" 및 "새 데이터베이스" 작업 유형으로 미리 보기 0.17.1 있었습니다.

```json
"details": {
    "queryFile": "./sql/database_state_detail.sql",
    "label": {...},
    "value": "state",
    "actions": {
        "database": "${Database}",
        "types": ["restore"]
    }
}
```
