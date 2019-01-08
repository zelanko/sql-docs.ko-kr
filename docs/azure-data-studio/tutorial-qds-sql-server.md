---
title: '자습서: 5 개의 가장 느린 쿼리 샘플 위젯 사용'
titleSuffix: Azure Data Studio
description: 이 자습서에는 5 개의 가장 느린 쿼리 샘플 위젯을 데이터베이스 대시보드에서 사용할 수 있도록 하는 방법을 보여 줍니다.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 491e66ecc8b0dfb3024a2beb59cfefd3f8e0d28f
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030787"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>자습서: 추가 된 *느린 쿼리 5* 데이터베이스 대시보드 위젯의 샘플

이 자습서는 데이터베이스의 가장 느린 5개 쿼리를 빠르게 보기 위해 *데이터베이스 대시보드*에 [!INCLUDE[name-sos](../includes/name-sos-short.md)]에서 기본 제공되는 샘플 widget 중 하나를 추가하는 과정을 보여줍니다. 또한 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 기능을 사용해서 느린 쿼리의 세부 정보와 쿼리 계획을 보는 방법을 배웁니다. 이 자습에서 배울 내용:

> [!div class="checklist"]
> * 데이터베이스에서 쿼리 저장소를 사용하도록 설정
> * 데이터베이스 대시보드에 미리 작성된 insight 위젯을 추가
> * 데이터베이스의 가장 느린 쿼리에 대한 세부 정보 보기
> * 느린 쿼리에 대한 쿼리 실행 계획 보기

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 몇 가지 정보 위젯-의-기본을 포함합니다. 이 자습서에서는 추가 하는 방법을 보여 줍니다.는 *쿼리-데이터-저장소-db-insight* 위젯에서 있지만 단계는 기본적으로 모든 위젯 추가 대해 동일 합니다.

## <a name="prerequisites"></a>필수 구성 요소

이 자습서에서는 SQL Server 또는 Azure SQL Database의 *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면, 다음 빠른 시작 중 하나를 수행합니다.

- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)를 사용하여 SQL Server에 연결 및 쿼리
- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)를 사용하여 Azure SQL Database에 연결 및 쿼리



## <a name="turn-on-query-store-for-your-database"></a>데이터베이스에 대 한 쿼리 저장소 설정

이 예제에서 위젯이 필요 *쿼리 저장소* 사용 하도록 설정 합니다.

1. 마우스 오른쪽 단추로 클릭 합니다 **TutorialDB** 데이터베이스 (에 **서버** 사이드바) 선택한 **새 쿼리**합니다.
2. 쿼리 편집기에서 다음 TRANSACT-SQL (T-SQL) 문을 붙여넣고 클릭 **실행**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>데이터베이스 대시보드 느린 쿼리 위젯 추가

추가할 합니다 *느린 쿼리 위젯* 대시보드를 편집 합니다 *dashboard.database.widgets* 에서 설정에 *사용자 설정* 파일.

1. 엽니다 *사용자 설정* 키를 눌러 **Ctrl + Shift + P** 열려는 합니다 *명령 팔레트*합니다.
2. 형식 *설정을* 검색 상자에 선택 **기본 설정: 사용자 설정을 엽니다**합니다.

   ![미해결 사용자 설정 명령](./media/tutorial-qds-sql-server/open-user-settings.png)

2. 형식 *대시보드* 설정 검색에서 찾은 상자 **dashboard.database.widgets**합니다.

   ![검색 설정](./media/tutorial-qds-sql-server/search-settings.png)

3. 사용자 지정 하는 **dashboard.database.widgets** 편집 하는 데 필요한 설정을 **dashboard.database.widgets** 항목에는 **사용자 설정** 섹션 (열은 오른쪽에 있음)입니다. 없는 경우 없습니다 **dashboard.database.widgets** 에 **사용자 설정** 섹션을 마우스로 합니다 **dashboard.database.widgets** 클릭 및 기본 설정 열에 텍스트 클릭 확인 하 고 텍스트의 왼쪽에 나타나는 연필 아이콘 **설정 복사할**합니다. 팝업에 표시 되 면 **설정에서 대체**를 클릭 하지 않음. 로 이동 합니다 **사용자 설정** 오른쪽에 열을 찾아서를 **dashboard.database.widgets** 섹션 및 다음 단계로 이동 합니다.

4. 에 **dashboard.database.widgets** 섹션에서 다음을 추가 합니다.

   ```json
        {
            "name": "slow queries widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "query-data-store-db-insight": null
            }
        },
    ```

1. 이 처음으로 새로운 위젯을 추가 하는 경우는 **dashboard.database.widgets** 섹션은 다음과 유사 하 게 표시 됩니다.

   ```json
   "dashboard.database.widgets": [
       {
           "name": "slow queries widget",
           "gridItemConfig": {
               "sizex": 2,
               "sizey": 1
           },
           "widget": {
               "query-data-store-db-insight": null
           }
       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }
       }
   ]
   ```

1. 키를 눌러 **Ctrl + S** 수정 된 저장할 **사용자 설정**합니다.

6. 열기는 *데이터베이스 대시보드* 로 이동 하 여 **TutorialDB** 에 **서버** 세로 막대를 마우스 오른쪽 단추로 클릭 하 여 **관리**합니다.

   ![대시보드 열기](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 정보 위젯을 대시보드에 표시 됩니다. 

   ![QDS 위젯](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>자세한 내용은 insight 세부 정보 보기

1. insight 위젯에 대 한 추가 정보를 보려면 줄임표를 클릭 합니다. (**...** ) 선택 하 고 오른쪽 위에 있는 **세부 정보 표시**합니다.
2. 항목을 선택 하는 항목에 대 한 자세한 세부 정보를 표시 하려면 **차트 데이터** 목록입니다.

   ![세부 정보 대화 상자 정보](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. 오른쪽에 있는 셀을 마우스 오른쪽 단추로 클릭 **query_sql_txt** 에 **항목 세부 정보** 누릅니다 **셀 복사**합니다.

4. 닫기 합니다 **Insights** 창입니다.

## <a name="view-the-query-plan"></a>쿼리 계획을 보려면 

1. 키를 눌러 새 쿼리 편집기를 엽니다 **Ctrl + N**합니다.

2. 이전 단계에서 쿼리 텍스트를 편집기에 붙여 넣습니다.

3. 클릭 **설명**합니다.

   ![QDS 정보 설명](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. 쿼리 실행 계획을 보려면:

   ![실행 계획(showplan)](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>저장 및 쿼리 계획을 열려면 

1. Insight 세부 정보 대화 상자를 엽니다.
2. 쿼리 항목 중 하나를 선택 합니다.
2. 마우스 오른쪽 단추로 클릭 **query_plan** 선택한 값 **셀 복사**

   ![Insights QDS 계획](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. 키를 눌러 **Ctrl + N** 새 편집기를 엽니다.

4. 복사한 계획을 편집기에 붙여 넣습니다.

5. 키를 눌러 **Ctrl + S** 파일을 저장 하 고 파일 확장명을 변경 하려면 *.sqlplan*합니다. *.sqlplan* 이므로를 입력 합니다 파일 확장 드롭다운에 표시 되지 않습니다. 이 자습서에서는 파일의 이름을 *slowquery.sqlplan*합니다.

6. 쿼리 계획에서 열립니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 쿼리 계획 뷰어:

   ![Insights QDS 계획](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음과 같은 방법을 학습했습니다.
> [!div class="checklist"]
> * 데이터베이스에서 쿼리 저장소를 사용하도록 설정
> * 데이터베이스 대시보드 정보 위젯 추가
> * 데이터베이스의 가장 느린 쿼리에 대한 세부 정보 보기
> * 느린 쿼리에 대한 쿼리 실행 계획 보기


사용 하도록 설정 하는 방법을 알아보려면 합니다 **테이블 공간 사용량** 샘플 정보, 다음 자습서를 완료 합니다.

> [!div class="nextstepaction"]
> [테이블 공간 샘플 정보 위젯 사용](tutorial-table-space-sql-server.md)
