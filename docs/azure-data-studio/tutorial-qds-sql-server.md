---
title: '자습서: 5개의 가장 느린 쿼리 샘플 위젯 사용'
titleSuffix: Azure Data Studio
description: 이 자습서에서는 데이터베이스 대시보드에서 5개의 가장 느린 쿼리 샘플 위젯을 사용하도록 설정하는 방법을 보여 줍니다.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 08/02/2019
ms.openlocfilehash: 576e175e8135808a4221e96085e39e9c0850190b
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810882"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>자습서: 데이터베이스 대시보드에 *5개의 가장 느린 쿼리* 샘플 위젯 추가

이 자습서에서는 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 기본 제공 샘플 위젯 중 하나를 ‘데이터베이스 대시보드’에 추가하여 데이터베이스의 가장 느린 5개 쿼리를 빠르게 확인하는 프로세스를 보여 줍니다.  또한 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 기능을 사용하여 느린 쿼리 및 쿼리 계획의 세부 정보를 보는 방법도 알아봅니다. 이 자습서에서는 다음 방법을 알아봅니다.

> [!div class="checklist"]
> * 데이터베이스에서 쿼리 저장소 사용
> * 미리 작성된 인사이트 위젯을 데이터베이스 대시보드에 추가
> * 데이터베이스의 가장 느린 쿼리에 대한 세부 정보 보기
> * 느린 쿼리에 대한 쿼리 실행 계획 보기

[!INCLUDE[name-sos](../includes/name-sos-short.md)]에는 기본 제공되는 몇 가지 인사이트 위젯이 있습니다. 이 자습서에서는 *query-data-store-db-insight* 위젯을 추가하는 방법을 보여 주지만, 위젯을 추가하는 단계는 기본적으로 동일합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 SQL Server 또는 Azure SQL Database *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면 다음 빠른 시작 중 하나를 완료합니다.

* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 SQL Server 연결 및 쿼리](quickstart-sql-server.md)

* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 Azure SQL Database 연결 및 쿼리](quickstart-sql-database.md)

## <a name="turn-on-query-store-for-your-database"></a>데이터베이스의 쿼리 저장소 설정

이 예제의 위젯을 사용하려면 ‘쿼리 저장소’를 사용하도록 설정해야 합니다. 

1. **서버** 사이드바에서 **TutorialDB** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

2. 다음 Transact-SQL(T-SQL) 문을 쿼리 편집기에 붙여넣고 **실행**을 클릭합니다.

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>데이터베이스 대시보드에 느린 쿼리 위젯 추가

대시보드에 ‘느린 쿼리 위젯’을 추가하려면 ‘사용자 설정’ 파일에서 *dashboard.database.widgets* 설정을 편집합니다.  

1. **Ctrl+Shift+P**를 눌러 ‘명령 팔레트’를 열고 ‘사용자 설정’을 엽니다.  

2. 검색 상자에 ‘설정’을 입력하고 **기본 설정:  사용자 설정 열기**를 선택합니다.

   ![사용자 설정 열기 명령](./media/tutorial-qds-sql-server/open-user-settings.png)

3. 설정 검색 상자에 ‘대시보드’를 입력하고 **dashboard.database.widgets**로 이동하여 ‘settings.json에서 편집’을 클릭합니다.  

   ![설정 검색](./media/tutorial-qds-sql-server/search-settings.png)

4. settings.json에서 다음 코드를 추가합니다.

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

5. **Ctrl+S**를 눌러 수정한 **사용자 설정**을 저장합니다.

6. **서버** 사이드바의 **TutorialDB**로 이동하여 ‘데이터베이스 대시보드’를 열고 마우스 오른쪽 단추를 클릭한 후 **관리**를 선택합니다. 

   ![대시보드 열기](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 인사이트 위젯이 대시보드에 표시됩니다.

   ![QDS 위젯](./media/tutorial-qds-sql-server/insight-qds-result.png)

## <a name="view-insight-details-for-more-information"></a>자세한 내용은 인사이트 세부 정보 보기

1. 인사이트 위젯에 대한 추가 정보를 보려면 오른쪽 상단의 줄임표( **...** )를 클릭하고 **세부 정보 표시**를 선택합니다.

2. 항목의 세부 정보를 보려면 **차트 데이터** 목록에서 항목을 선택합니다.

   ![인사이트 세부 정보 대화 상자](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. **항목 세부 정보**에서 **query_sql_txt** 오른쪽에 있는 셀을 마우스 오른쪽 단추로 클릭하고 **셀 복사**를 클릭합니다.

4. **인사이트** 창을 닫습니다.

## <a name="view-the-query-plan"></a>쿼리 계획 보기

1. **TutorialDB**를 마우스 오른쪽 단추로 클릭하고 *관리*를 선택합니다.

2. **저속 쿼리 위젯**에서 인사이트 위젯에 대한 추가 정보를 보려면 오른쪽 상단의 줄임표( *...* )를 클릭하고 **쿼리 실행**를 선택합니다.

    ![쿼리 실행](media/tutorial-qds-sql-server/run-query.png)

3. 이제 결과가 포함된 새 쿼리 창이 표시됩니다.

    ![쿼리 결과 실행](media/tutorial-qds-sql-server/run-query-results.png)

4. **설명**을 클릭합니다.

   ![인사이트 QDS 설명](./media/tutorial-qds-sql-server/insight-qds-explain.png)

5. 쿼리의 실행 계획 보기:

   ![실행 계획(showplan)](./media/tutorial-qds-sql-server/showplan.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * 데이터베이스에서 쿼리 저장소 사용
> * 인사이트 위젯을 데이터베이스 대시보드에 추가
> * 데이터베이스의 가장 느린 쿼리에 대한 세부 정보 보기
> * 느린 쿼리에 대한 쿼리 실행 계획 보기

**테이블 공간 사용량** 샘플 인사이트를 사용하도록 설정하는 방법을 알아보려면 다음 자습서를 완료합니다.

> [!div class="nextstepaction"]
> [테이블 공간 샘플 인사이트 위젯 사용](tutorial-table-space-sql-server.md)