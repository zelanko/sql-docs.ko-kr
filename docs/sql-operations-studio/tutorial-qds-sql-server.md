---
title: '자습서: 가장 느린 쿼리 5 개의 사용 샘플 위젯-SQL 작업 Studio (미리 보기) | Microsoft Docs'
description: 이 자습서에서는 5 개의 가장 느린 쿼리 샘플 위젯 데이터베이스 대시보드를 사용 하도록 설정 하는 방법을 설명 합니다.
ms.custom: tools|sos
ms.date: 03/15/2018
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c0597adca9897d69503bba3d08d9cdafd859c1c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>자습서: 추가 된 *가장 느린 쿼리 5* 데이터베이스 대시보드에 위젯을 샘플

이 자습서 중 하나를 추가 하는 과정을 보여 줍니다. [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 기본 제공 샘플 widget을는 *데이터베이스 대시보드* 신속 하 게 데이터베이스의 가장 느린 쿼리 5를 볼 수 있습니다. 느린 쿼리 세부 정보를 보려면 하는 방법도 알아볼 수 및 사용 하 여 쿼리 계획 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 기능입니다. 이 자습서는 방법을 배웁니다 하는 방법:

> [!div class="checklist"]
> * 데이터베이스에서 쿼리 저장소를 사용 하도록 설정
> * 데이터베이스 대시보드 미리 작성 된 통찰력 위젯 추가
> * 데이터베이스의 가장 느린 쿼리 하는 방법에 대 한 세부 정보 보기
> * 느린 쿼리에 대 한 쿼리 실행 계획 보기

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 여러 통찰력 위젯-의-기본을 포함합니다. 추가 하는 방법을 보여 주는이 자습서는 *쿼리-데이터-저장소-db-통찰력* 위젯, 있지만 실행 단계가 기본적으로 모든 위젯 추가 대해 동일 합니다.

## <a name="prerequisites"></a>필수 구성 요소

이 자습서에서는 SQL Server 또는 Azure SQL 데이터베이스 *TutorialDB*합니다. 만들려는 *TutorialDB* 데이터베이스에서 다음 퀵 스타트 중 하나를 완료 합니다.

- [연결 및 SQL Server를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [연결 및 Azure SQL 데이터베이스를 사용 하 여 쿼리 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>데이터베이스에 대 한 쿼리 저장소를 켜기

이 예에서 위젯 필요 *쿼리 저장소* 가능 하도록 합니다.

1. 마우스 오른쪽 단추로 클릭는 **TutorialDB** 데이터베이스 (에 **서버** 세로 막대)를 선택 하 고 **새 쿼리**합니다.
2. 쿼리 편집기에서 다음 TRANSACT-SQL (T-SQL) 문을 붙여 넣고 클릭 **실행**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>데이터베이스 대시보드 느린 쿼리 위젯 추가

추가 하는 *쿼리 위젯에 대 한 느린* 편집 하 여 대시보드에 *dashboard.database.widgets* 에서 설정 프로그램 *사용자 설정* 파일입니다.

1. 열고 *사용자 설정* 키를 눌러 **Ctrl + Shift + P** 열려는 *명령 팔레트*합니다.
2. 형식 *설정* 고 검색 상자에서 **기본 설정: 사용자 설정 열기**합니다.

   ![열기 사용자 설정 명령](./media/tutorial-qds-sql-server/open-user-settings.png)

2. 형식 *대시보드* 설정 검색에서 찾은 상자 **dashboard.database.widgets**합니다.

   ![검색 설정](./media/tutorial-qds-sql-server/search-settings.png)

3. 사용자 지정 하는 **dashboard.database.widgets** 편집 하는 데 필요한 설정을 **dashboard.database.widgets** 항목에는 **사용자 설정** 섹션 (열에는 오른쪽에 있음)입니다. 없는 경우 없는 **dashboard.database.widgets** 에 **사용자 설정** 섹션에서 위로 마우스를 가져가고는 **dashboard.database.widgets** 클릭 및 기본 설정 열에는 텍스트 누른 텍스트의 왼쪽에 표시 되는 연필 아이콘 **설정 복사**합니다. 팝업이 표시 되 면 **설정에서 바꾸기**, 클릭 하지 말고! 이동 하는 **사용자 설정** 오른쪽 열을 찾습니다는 **dashboard.database.widgets** 섹션 및 다음 단계로 진행 합니다.

4. 에 **dashboard.database.widgets** 섹션에서 다음 코드를 추가 합니다.

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

1. 이 처음으로 새로운 위젯을 추가 하는 경우는 **dashboard.database.widgets** 섹션은 다음과 유사 하 게 같아야 합니다.:

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

6. 열기는 *데이터베이스 대시보드* 로 이동 하 여 **TutorialDB** 에 **서버** 사이드바, 마우스 선택 **관리**합니다.

   ![대시보드 열기](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 통찰력 위젯을 대시보드에 표시 됩니다. 

   ![QDS 위젯](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>자세한 내용은 통찰력 세부 정보 보기

1. 통찰력 위젯에 대 한 추가 정보를 보려면 줄임표 (**...** ) 선택 하 고 오른쪽 위에 있는 **자세한 정보 표시**합니다.
2. 항목을 선택 하는 항목에 대 한 자세한 세부 정보를 표시 하려면 **차트 데이터** 목록입니다.

   ![통찰력 세부 정보 대화 상자](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. 오른쪽에 있는 셀을 마우스 오른쪽 단추로 클릭 **query_sql_txt** 에 **항목 정보** 클릭 **셀 복사**합니다.

4. 닫기는 **Insights** 창.

## <a name="view-the-query-plan"></a>쿼리 계획 보기 

1. 키를 눌러 새 쿼리 편집기를 열고 **Ctrl + N**합니다.

2. 이전 단계에서 쿼리 텍스트를 편집기에 붙여 넣습니다.

3. 클릭 **설명**합니다.

   ![QDS 통찰력 설명](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. 쿼리 실행 계획을 보려면:

   ![실행 계획(showplan)](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>저장 하 고 쿼리 계획을 열려면 

1. 통찰력 세부 정보 대화 상자를 엽니다.
2. 쿼리 항목 중 하나를 선택 합니다.
2. 마우스 오른쪽 단추로 클릭 **query_plan** 값 및 선택 **셀 복사**

   ![Insights QDS 계획](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. 키를 눌러 **Ctrl + N** 새 편집기를 엽니다.

4. 복사한 계획을 편집기에 붙여 넣습니다.

5. 키를 눌러 **Ctrl + S** 파일을 저장 하 고 파일 확장명을 변경 하려면 *.sqlplan*합니다. *.sqlplan* 되었으므로에 직접 입력, 파일 확장명 드롭다운에 표시 되지 않습니다. 이 자습서에 대 한 파일 이름을 *slowquery.sqlplan*합니다.

6. 쿼리 계획 열립니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 쿼리 계획 뷰어:

   ![Insights QDS 계획](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>다음 단계
이 자습서에서는 알아보았습니다 하는 방법:
> [!div class="checklist"]
> * 데이터베이스에서 쿼리 저장소를 사용 하도록 설정
> * 데이터베이스 대시보드 통찰력 위젯 추가
> * 데이터베이스의 가장 느린 쿼리 하는 방법에 대 한 세부 정보 보기
> * 느린 쿼리에 대 한 쿼리 실행 계획 보기


사용 하도록 설정 하는 방법에 알아보려면는 **테이블 공간 사용량** 샘플 통찰력, 다음 자습서를 완료:

> [!div class="nextstepaction"]
> [테이블 공간 샘플 통찰력 위젯 사용](tutorial-table-space-sql-server.md)