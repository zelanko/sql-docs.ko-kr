---
title: '자습서: SQL 작업 Studio (미리 보기)에서 사용자 지정 통찰력 위젯을 빌드할 | Microsoft Docs'
description: 이 자습서에는 사용자 지정 통찰력은 widget을 작성할 SQL 작업 Studio (미리 보기)의 데이터베이스 및 서버 대시보드에 추가 하는 방법을 보여 줍니다.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe4ec372ada626ab1dd05981d9ffa3217eb46bd5
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="tutorial-build-a-custom-insight-widget"></a>자습서: 빌드 사용자 지정 통찰력 위젯

이 자습서에서는 사용자 지정 통찰력 위젯을 빌드할 사용자 고유의 대 한 정보 쿼리를 사용 하는 방법을 설명 합니다.

이 자습서에서 자세한 내용은 방법:
> [!div class="checklist"]
> * 사용자 고유의 쿼리를 실행 하 고 차트에서 보기
> * 차트에서 사용자 지정 통찰력 위젯 빌드
> * 서버 또는 데이터베이스 대시보드로 차트를 추가 합니다.
> * 세부 정보를 사용자 지정 통찰력 위젯 추가

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에서는 SQL Server 또는 Azure SQL 데이터베이스 *TutorialDB*합니다. 만들려는 *TutorialDB* 데이터베이스에서 다음 퀵 스타트 중 하나를 완료 합니다.

- [연결 및 SQL Server를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [연결 및 Azure SQL 데이터베이스를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>사용자 고유의 쿼리를 실행 하 고 차트 보기에서 결과 보려면
이 단계에서는 현재 활성 세션을 쿼리 하는 sql 스크립트를 실행 합니다.

1. 새 편집기를 열려면 **Ctrl + N**합니다. 

2. 연결 컨텍스트를 변경 **TutorialDB**합니다.

3. 쿼리 편집기에 다음 쿼리를 붙여 넣습니다.

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. 쿼리 편집기에서 저장 한 \*.sql 파일입니다. 이 자습서에 대 한 스크립트를 저장 *activeSession.sql*합니다.

5. 키를 눌러 쿼리를 실행 하려면 **F5**합니다.

6. 쿼리 결과 표시 되 면 클릭 **차트 보기**, 클릭는 **차트 뷰어에** 탭 합니다.

7. 변경 **차트 종류** 를 **count**합니다. 이러한 설정은 계산 차트를 렌더링합니다.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>데이터베이스 대시보드를 사용자 지정 정보 추가

1. 위젯 구성 정보를 열려면 **만들 통찰력** 에 *차트 뷰어에*:

   ![구성](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. 통찰력 구성 (JSON 데이터)를 복사 합니다. 

3. 키를 눌러 **Ctrl + 쉼표** 열려는 *사용자 설정*합니다.

4. 형식 *대시보드* 에 *검색 설정*합니다.

5. 클릭 **편집** 에 대 한 *dashboard.database.widgets*합니다.

   ![대시보드 설정](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. 붙여 통찰력 구성 JSON에 *dashboard.database.widgets*합니다. 데이터베이스 대시보드 설정 하면 다음과 같이 표시 합니다.

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
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
            }
        }
    ]
   ```

7. 저장 된 *사용자 설정* 파일을 열고는 *TutorialDB* 데이터베이스 대시보드를 보려면 활성 세션 위젯:

   ![activesession 통찰력](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>사용자 지정 통찰력에 세부 정보 추가

1. 새 편집기를 열려면 **Ctrl + N**합니다.

2. 연결 컨텍스트를 변경 **TutorialDB**합니다.

3. 쿼리 편집기에 다음 쿼리를 붙여 넣습니다.

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. 쿼리 편집기에서 저장 한 \*.sql 파일입니다. 이 자습서에 대 한 스크립트를 저장 *activeSessionDetail.sql*합니다.

5. 키를 눌러 **Ctrl + 쉼표** 열려는 *사용자 설정*합니다.

6. 기존 편집 *dashboard.database.widgets* 설정 파일에 있는 노드:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql",
                    "details": {
                        "queryFile": "{your file folder}/activeSessionDetail.sql",
                        "label": "SID",
                        "value": "Login Name"
                    }
                }
            }
        }
    ]
   ```

7. 저장 된 *사용자 설정* 파일을 열고는 *TutorialDB* 데이터베이스 대시보드 합니다. 옆에 있는 줄임표 (...) 단추를 클릭 *위젯 내* 정보를 표시 하도록 합니다.

    ![activesession 통찰력](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서는 알아보았습니다 하는 방법:
> [!div class="checklist"]
> * 사용자 고유의 쿼리를 실행 하 고 차트에서 보기
> * 차트에서 사용자 지정 통찰력 위젯 빌드
> * 서버 또는 데이터베이스 대시보드로 차트를 추가 합니다.
> * 세부 정보를 사용자 지정 통찰력 위젯 추가

데이터베이스 백업 및 복원 하는 방법을 알아보려면 다음 자습서를 완료 합니다.

> [!div class="nextstepaction"]
> [데이터베이스 백업 및 복원](tutorial-backup-restore-sql-server.md)합니다.