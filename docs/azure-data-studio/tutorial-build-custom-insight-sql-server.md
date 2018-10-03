---
title: '자습서: Azure Data Studio 사용자 지정 정보 위젯을 빌드 | Microsoft Docs'
description: 이 자습서에는 사용자 지정 정보 위젯 빌드하고 Azure Data Studio의 데이터베이스 및 서버 대시보드에 추가 하는 방법을 보여 줍니다.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d14c8d9e4a17782464e13b380334c85c9ee1036c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "48039097"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>자습서: 빌드 사용자 지정 정보 위젯

이 자습서에는 고유한 정보 쿼리를 사용 하 여 사용자 지정 정보 위젯 빌드 방법을 보여 줍니다.

이 자습서에 대해 알아봅니다 방법:
> [!div class="checklist"]
> * 사용자 고유의 쿼리를 실행 하 고 차트 보기
> * 빌드 차트에서 사용자 지정 정보 위젯
> * 서버 또는 데이터베이스 대시보드에 차트를 추가
> * 사용자 지정 정보 위젯을에 세부 정보 추가

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에서는 SQL Server 또는 Azure SQL Database *TutorialDB*합니다. 만들려면 합니다 *TutorialDB* 데이터베이스, 다음 빠른 시작 중 하나를 수행 합니다.

- [연결 및 SQL Server를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [연결 및 Azure SQL Database를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>사용자 고유의 쿼리를 실행 하 고 차트 뷰에서 결과
이 단계에서 현재 활성 세션을 쿼리 하는 sql 스크립트를 실행 합니다.

1. 새 편집기를 열려면 누릅니다 **Ctrl + N**합니다. 

2. 연결 컨텍스트를 변경 **TutorialDB**합니다.

3. 쿼리 편집기에 다음 쿼리를 붙여 넣습니다.

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. 쿼리 편집기에서 저장 한 \*.sql 파일입니다. 이 자습서에서는 스크립트를 저장할 *activeSession.sql*합니다.

5. 쿼리를 실행 하려면 키를 누릅니다 **F5**합니다.

6. 쿼리 결과 표시 되 면 클릭 **차트 뷰로**를 클릭 합니다 **차트 뷰어** 탭 합니다.

7. 변경 **차트 종류** 하 **개수**합니다. 이러한 설정을 수 차트를 렌더링합니다.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>데이터베이스 대시보드를 사용자 지정 정보 추가

1. 위젯 구성 정보를 열려면 **만들 Insight** 에 *차트 뷰어*:

   ![구성](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. 정보 활용 구성 (JSON 데이터)를 복사 합니다. 

3. 키를 눌러 **Ctrl + 쉼표** 열려는 *사용자 설정*합니다.

4. 형식 *대시보드* 에 *검색 설정*합니다.

5. 클릭 **편집할** 에 대 한 *dashboard.database.widgets*합니다.

   ![대시보드 설정](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. 정보 활용 구성 JSON를 붙여로 *dashboard.database.widgets*합니다. 데이터베이스 대시보드 설정은 다음과 같습니다.

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

7. 저장 된 *사용자 설정* 파일을 찾아서 엽니다는 *TutorialDB* 활성 세션 위젯을 확인 하려면 데이터베이스 대시보드:

   ![activesession 정보](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>세부 정보를 사용자 지정 정보 추가

1. 새 편집기를 열려면 누릅니다 **Ctrl + N**합니다.

2. 연결 컨텍스트를 변경 **TutorialDB**합니다.

3. 쿼리 편집기에 다음 쿼리를 붙여 넣습니다.

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. 쿼리 편집기에서 저장 한 \*.sql 파일입니다. 이 자습서에서는 스크립트를 저장할 *activeSessionDetail.sql*합니다.

5. 키를 눌러 **Ctrl + 쉼표** 열려는 *사용자 설정*합니다.

6. 기존 편집할 *dashboard.database.widgets* 설정 파일에는 노드:

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

7. 저장 된 *사용자 설정* 파일을 찾아서 엽니다는 *TutorialDB* 데이터베이스 대시보드. 옆에 있는 줄임표 (...) 단추를 클릭 *위젯 내* 정보를 표시 합니다.

    ![activesession 정보](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서는 학습 하는 방법.
> [!div class="checklist"]
> * 사용자 고유의 쿼리를 실행 하 고 차트 보기
> * 빌드 차트에서 사용자 지정 정보 위젯
> * 서버 또는 데이터베이스 대시보드에 차트를 추가
> * 사용자 지정 정보 위젯을에 세부 정보 추가

데이터베이스 백업 및 복원 하는 방법에 알아보려면 다음 자습서를 완료 합니다.

> [!div class="nextstepaction"]
> [데이터베이스 백업 및 복원](tutorial-backup-restore-sql-server.md)합니다.
