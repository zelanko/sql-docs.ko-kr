---
title: Insights 및 SQL 작업 Studio (미리 보기)의 일반적인 작업을 신속 하 게 액세스할 | Microsoft Docs
description: SQL 작업 Studio (미리 보기)에서 통찰력 위젯을 표시 하는 방법을 알아봅니다.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 1b457f1794f902de047f68be2d8b3d672cf5c6ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>대시보드 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

대시보드, 마우스 오른쪽 단추로 클릭 한 서버 또는 데이터베이스를 표시 하 고 선택 **관리**합니다.

![샘플 대시보드](media/dashboards/sample-dashboard.png)

**서버 속성** 버전, 버전, 컴퓨터 이름 및 OS 버전을 포함 하는 서버의 속성을 포함 합니다.

**작업** commons 복원 하며 새 쿼리 등의 작업을 포함 합니다.

**데이터베이스 검색** 테이블을 포함 하는 서버에 저장 된 기존 데이터베이스를 쉽게 조회 합니다.

**백업 상태** 기존 데이터베이스에 대 한 백업 상태를 쉽게 조회 합니다.

## <a name="configuring-insight-widgets"></a>통찰력 위젯 구성
찾을 수 있는 대시보드를 설정 하기 위한 자습서를 따르는 것이 좋습니다 [여기](tutorial-build-custom-insight-sql-server.md)합니다.

또한, 체크 아웃 해야는 [위젯에 대 한 정보를 구성 하는 방법에 방법 도움말]()합니다.

이 자습서에 읽은 다음 자습서에서 다루지 않는 특정 위젯에 대해 알아봅니다.

## <a name="insight-detail"></a>세부 정보
통찰력 세부 정보 플라이 아웃 관련된 통찰력 위젯에 대 한 자세한 정보를 제공합니다. 
- 통찰력 위젯 수, 선, 차트 등에서 요약 요약 뷰는 렌더링합니다. 
- 통찰력 세부 정보 플라이 아웃 "드릴" 세부 정보를 나열 하는 높은 수준의 통찰력 위젯에 나열 된 각 항목에 대 한 심층적인 데이터 통찰력을 제공 합니다. 
  - 세부 정보 플라이 아웃 내용은 주 위젯의 쿼리 하는 별도 SQL 쿼리로 정의 됩니다. 

통찰력 세부 정보 쿼리를 사용 하는 집합 요구 않으며 레이아웃은 표준입니다.
- 보기의 위쪽 절반은 항상 2 열 "요약" 보기입니다. 사용할 열을 JSON 구성의 "label" 및 "value" 속성에 정의 된
- 요약 테이블에서 행을 클릭 아래쪽 절반 플라이 아웃 됩니다 목록의 전체 집합을 해당 행에 대 한 열 정보입니다.

### <a name="insight-detail-configuration-in-packagejson"></a>Package.json의 세부 구성 정보

샘플 세부 정보 통찰력 플라이 아웃 구성
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
|자세히|json 개체|||필수 속성의 구조 내 통찰력 세부 정의 정의 하려면||
|queryFile|string|||통찰력 세부 sql 쿼리 파일 경로 및 package.json의 위치에 상대적인 파일 이름||
|레이블|json 개체|||요약 목록 보기에 각 항목을 정의 하는 필수 속성|나중에 'summaryList'와 같은 변경 하려면이 속성의 이름|
|아이콘|string|||각 요약 목록 보기 항목에 대 한 reder에 아이콘 이름을 표시 합니다.|지원 되는 아이콘 목록 (tbd) 문서화 됩니다.|
|column|string|||쿼리 결과 집합에서 요약 목록 보기에서 첫 번째 열의 이름을 표시합니다|보다 알기 쉬운 이름으로이 속성의 이름을 변경할 수는 나중에|
|value|string|||쿼리 결과 집합에서 요약 목록 보기에서 두 번째 열의 이름을 표시 합니다. 이 열의 값은 조건을 확인 하 고 각 요약 목록 뷰 항목 색 점에 대 한 색을 설정 하는 데 사용 됩니다.|나중에이 속성의 이름을 보다 직관적인 값으로 변경 됩니다.|
|condition(조건)|json 개체|||열 값에 대 한 조건 검사를 정의 하 고 각 요약 목록 보기 항목에 대 한 색을 결정||
|if|string|항상, equals, notEquals, 보다 큼, lessThan, greaterThanOrEqauls, lessThanOrEquals||조건 확인 연산자|같음 연산자는 속성 이름을 나중에 변경 됩니다.|
|equals|string|||조건 값 확인|'value' 하도록이 속성 이름이 변경 되는 나중에|

## <a name="insight-actions"></a>정보 작업
통찰력 위젯와 통찰력 세부 정보를 쉽게 문제를 완화 하거나 관리 하기 위한 실행 계획을 가져올 수 있습니다. 예를 들어 됩니다 DBCC CHECKDB를 실행 해도 생각 하면, 오류 로그를 읽을 또는 데이터베이스가 복구 보류 상태에 있을 때 데이터베이스를 복원 합니다. 또는 수행 하려는 작업 중 하나일 수 있습니다.

사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 통찰력 동작 구성, 복원 또는 sql 스크립트를 사용 하 여 정의 자신의 작업을 표시와 같은 기본 제공 작업에 매핑할 수 있습니다.

> Sql 스크립트를 사용 하 여 사용자 지정 동작의 구성 개발 중 이며 아직 비공개 미리 보기 빌드에 사용할 수 없는 합니다.

## <a name="sample-insight-action-definition"></a>샘플 통찰력 동작 정의

```"actions"{}``` 통찰력 동작을 정의합니다. 와 같은 특정 범위에 대해 정의할 수 동작 ```"server"```, ```"database"``` 등 및 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 동작에 현재 연결 컨텍스트 정보를 전달 합니다. 

예를 들어 복원 작업 시작 시 WideWorldImporters 데이터베이스에 대 한 ```"database": "${Database}"``` 정의 전달할 나타냅니다 ```Database``` 복원 작업에 쿼리 결과에 열 값입니다. 다음 데이터베이스에 대 한 복원 작업이 시작 됩니다. ```"types"``` json 배열 및 배열에 여러 작업을 나열 될 수 있습니다. 상황에 맞는 메뉴를 기본적으로 데이터베이스가 통찰력 세부 정보 대화 상자에서 해당 사용자 수를 클릭 한 작업을 수행 합니다. 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] 미리 보기 0.17.1 "backup", "restore", "새 쿼리" 및 "새 데이터베이스" 동작 유형으로 설정 했습니다.

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
