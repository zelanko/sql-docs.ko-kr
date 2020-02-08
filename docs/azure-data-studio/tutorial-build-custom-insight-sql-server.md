---
title: '자습서: 사용자 지정 인사이트 위젯 빌드'
titleSuffix: Azure Data Studio
description: 이 자습서에서는 사용자 지정 정보 위젯을 빌드하고 Azure Data Studio의 데이터베이스 및 서버 대시보드에 추가하는 방법을 보여 줍니다.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 34ee9c23569897247f05d6b9b5f9f2610f5d68fc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67959094"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>자습서: 사용자 지정 인사이트 위젯 빌드

이 자습서에서는 고유한 인사이트 쿼리를 사용하여 사용자 지정 인사이트 위젯을 빌드하는 방법을 보여 줍니다.

이 자습서에서는 다음 방법을 알아봅니다.
> [!div class="checklist"]
> * 사용자 고유의 쿼리를 실행하여 차트에서 보기
> * 차트에서 사용자 지정 인사이트 위젯 빌드
> * 서버 또는 데이터베이스 대시보드에 차트 추가
> * 사용자 지정 인사이트 위젯에 세부 정보 추가

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 SQL Server 또는 Azure SQL Database *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면 다음 빠른 시작 중 하나를 완료합니다.

- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 Azure SQL Database 연결 및 쿼리](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>사용자 고유의 쿼리를 실행하고 차트 보기에서 결과 보기
이 단계에서는 sql 스크립트를 실행하여 현재 활성 세션을 쿼리합니다.

1. 새 편집기를 열려면 **Ctrl+N**을 누릅니다. 

2. 연결 컨텍스트를 **TutorialDB**로 변경합니다.

3. 쿼리 편집기에 다음 쿼리를 붙여넣습니다.

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. 편집기의 쿼리를 \*.sql 파일로 저장합니다. 이 자습서에서는 스크립트를 *activeSession.sql*로 저장합니다.

5. 쿼리를 실행하려면 **F5** 키를 누릅니다.

6. 쿼리 결과가 표시되면 **차트로 보기**를 클릭하고 **차트 뷰어** 탭을 클릭합니다.

7. **차트 종류**를 **개수**로 변경합니다. 이러한 설정대로 개수 차트가 렌더링됩니다.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>데이터베이스 대시보드에 사용자 지정 인사이트 추가

1. 인사이트 위젯 구성을 열려면 *차트 뷰어*에서 **인사이트 만들기**를 클릭합니다.

   ![구성](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. 인사이트 구성(JSON 데이터)을 복사합니다. 

3. **Ctrl+,** 를 눌러 *사용자 설정*을 엽니다.

4. *설정 검색*에서 *대시보드*를 입력합니다.

5. *dashboard.database.widgets*에 대해 **편집**을 클릭합니다.

   ![대시보드 설정](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. 인사이트 구성 JSON을 *dashboard.database.widgets*에 붙여넣습니다. 데이터베이스 대시보드 설정은 다음과 같습니다.

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

7. *사용자 설정* 파일을 저장하고 *TutorialDB* 데이터베이스 대시보드를 열어 활성 세션 위젯을 표시합니다.

   ![activesession 인사이트](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>사용자 지정 인사이트에 세부 정보 추가

1. 새 편집기를 열려면 **Ctrl+N**을 누릅니다.

2. 연결 컨텍스트를 **TutorialDB**로 변경합니다.

3. 쿼리 편집기에 다음 쿼리를 붙여넣습니다.

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. 편집기의 쿼리를 \*.sql 파일로 저장합니다. 이 자습서에서는 스크립트를 *activeSessionDetail.sql*로 저장합니다.

5. **Ctrl+,** 를 눌러 *사용자 설정*을 엽니다.

6. 설정 파일에서 기존 *dashboard.database.widgets* 노드를 편집합니다.

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

7. *사용자 설정* 파일을 저장하고 *TutorialDB* 데이터베이스 대시보드를 엽니다. 세부 정보를 표시하려면 *My-Widget* 옆에 있는 줄임표(...) 단추를 클릭합니다.

    ![activesession 인사이트](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * 사용자 고유의 쿼리를 실행하여 차트에서 보기
> * 차트에서 사용자 지정 인사이트 위젯 빌드
> * 서버 또는 데이터베이스 대시보드에 차트 추가
> * 사용자 지정 인사이트 위젯에 세부 정보 추가

데이터베이스를 백업 및 복원하는 방법을 알아보려면 다음 자습서를 완료하세요.

> [!div class="nextstepaction"]
> [데이터베이스 백업 및 복원](tutorial-backup-restore-sql-server.md).
