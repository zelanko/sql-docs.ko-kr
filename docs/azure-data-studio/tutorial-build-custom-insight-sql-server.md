---
title: '자습서: Azure Data Studio 사용자 지정 정보 위젯을 빌드 | Microsoft Docs'
description: 이 자습서에는 사용자 지정 정보 위젯 빌드하고 Azure Data Studio의 데이터베이스 및 서버 대시보드에 추가 하는 방법을 보여 줍니다.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: caecf780f5c8cc656f6b0b2a95dd3d68c48355cb
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356344"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>자습서: 사용자 지정 정보 위젯 빌드

이 자습서에는 고유한 정보 쿼리를 사용하여 사용자 지정 정보 위젯을 빌드하는 방법을 보여줍니다.

이 자습서에서 다음과 같은 방법을 배웁니다.
> [!div class="checklist"]
> * 사용자 고유의 쿼리를 실행하고 차트 보기
> * 차트에서 사용자 지정 정보 위젯 빌드
> * 서버 또는 데이터베이스 대시보드에 차트를 추가
> * 사용자 지정 정보 위젯에 세부 정보 추가

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에서는 SQL Server 또는 Azure SQL Database의 *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면, 다음 빠른 시작 중 하나를 수행합니다.

- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)를 사용하여 SQL Server에 연결 및 쿼리
- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)를 사용하여 Azure SQL Database에 연결 및 쿼리


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>사용자 고유의 쿼리를 실행하고 차트 뷰에서 결과 보기
이 단계에서 현재 활성 세션을 쿼리하는 sql 스크립트를 실행합니다.

1. 새 편집기를 열려면 **Ctrl + N**을 누릅니다. 

2. 연결 컨텍스트를 **TutorialDB**로 변경합니다.

3. 쿼리 편집기에 다음 쿼리를 붙여 넣습니다.

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. 편집기에서 쿼리를 \*.sql 파일에 저장합니다. 이 자습서에서는 스크립트를 *activeSession.sql*로 저장합니다.

5. 쿼리를 실행하려면 **F5**키를 누릅니다.

6. 쿼리 결과가 표시되면 **차트 뷰로**를 클릭합니다 **차트 뷰어** 탭을 클릭합니다.

7. **차트 종류**를 **개수**로 변경합니다. 이러한 설정은 개수 차트를 렌더링합니다.

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

1. 새 편집기를 열려면 **Ctrl + N**을 누릅니다.

2. 연결 컨텍스트를 **TutorialDB**로 변경합니다.

3. 쿼리 편집기에 다음 쿼리를 붙여 넣습니다.

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. 편집기에서 쿼리를 \*.sql 파일에 저장합니다. 이 자습서에서는 스크립트를 저장할 *activeSessionDetail.sql*합니다.

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
> * 사용자 고유의 쿼리를 실행하고 차트 보기
> * 차트에서 사용자 지정 정보 위젯 빌드
> * 서버 또는 데이터베이스 대시보드에 차트를 추가
> * 사용자 지정 정보 위젯에 세부 정보 추가

데이터베이스 백업 및 복원 하는 방법에 알아보려면 다음 자습서를 완료 합니다.

> [!div class="nextstepaction"]
> [데이터베이스 백업 및 복원](tutorial-backup-restore-sql-server.md)합니다.
