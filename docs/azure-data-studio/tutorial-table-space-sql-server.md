---
title: 테이블 공간 사용량 샘플 인사이트 위젯 사용
description: 이 자습서에서는 Azure Data Studio 데이터베이스 대시보드에서 테이블 공간 사용량 샘플 인사이트 위젯을 사용하도록 설정하는 방법을 보여 줍니다.
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/10/2019
ms.openlocfilehash: 8d2be24a72c098c5a6a0b5e3ecefbde9bbe39cd5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726702"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-azure-data-studio"></a>자습서: Azure Data Studio를 사용하여 테이블 공간 사용량 샘플 인사이트 위젯 사용

이 자습서에서는 데이터베이스 대시보드에서 인사이트 위젯을 사용하도록 설정하여 데이터베이스에 있는 모든 테이블의 공간 사용량을 한눈에 볼 수 있게 하는 방법을 보여 줍니다. 이 자습서에서는 다음 방법을 알아봅니다.

> [!div class="checklist"]
> * 기본 제공 인사이트 위젯 예제를 사용하여 인사이트 위젯 빠르게 켜기
> * 테이블 공간 사용량 세부 정보 보기
> * 인사이트 차트의 데이터 필터링 및 레이블 세부 정보 보기

## <a name="prerequisites"></a>필수 구성 요소

이 자습서를 완료하려면 SQL Server 또는 Azure SQL Database *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면 다음 빠른 시작 중 하나를 완료합니다.

* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 SQL Server 연결 및 쿼리](quickstart-sql-server.md)
* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 사용하여 Azure SQL Database 연결 및 쿼리](quickstart-sql-database.md)

## <a name="turn-on-a-management-insight-on-azure-data-studios-database-dashboard"></a>Azure Data Studio의 데이터베이스 대시보드에서 관리 인사이트 켜기

Azure Data Studio에는 데이터베이스 테이블에서 사용되는 공간을 모니터링하는 기본 제공 샘플 위젯이 있습니다.

1. **Ctrl+Shift+P**를 눌러 ‘명령 팔레트’를 열고 ‘사용자 설정’을 엽니다. 

2. 검색 상자에 ‘설정’을 입력하고 **기본 설정: 사용자 설정 열기**를 선택합니다.

3. 설정 검색 입력 상자에 ‘대시보드’를 입력하고 **dashboard.database.widgets**를 찾습니다.

4. **dashboard.database.widgets** 설정을 사용자 지정하려면 **사용자 설정** 섹션에서 **dashboard.database.widgets** 항목을 편집해야 합니다.

   ![설정 검색](media/tutorial-table-space-sql-server/search-settings.png)

   **사용자 설정** 섹션에 **dashboard.database.widgets**가 없으면 기본 설정 열의 **dashboard.database.widgets** 텍스트를 마우스로 가리킨 다음, 텍스트 왼쪽에 나타나는 *톱니* 아이콘을 클릭하고 **JSON 설정으로 복사**를 클릭합니다. 팝업에 **설정에서 바꾸기**가 표시되면 클릭하지 않습니다. 오른쪽의 **사용자 설정** 열로 이동하여 **dashboard.database.widgets** 섹션을 찾고 다음 단계를 진행합니다.

5. **dashboard.database.widgets** 섹션에서 다음 줄을 추가합니다.

   ```json
        {
            "name": "Space Used by Tables",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "table-space-db-insight": null
            }
        },
    ```

   **dashboard.database.widgets** 섹션이 다음 그림과 같이 표시됩니다.

    ![설정 검색](./media/tutorial-table-space-sql-server/insight-table-space.png)

6. **Ctrl+S**를 눌러 설정을 저장합니다.

7. **TutorialDB**를 마우스 오른쪽 단추로 클릭하고 **관리**를 클릭하여 데이터베이스 대시보드를 엽니다.

8. 다음 그림과 같이 ‘테이블 공간’ 인사이트 위젯을 봅니다.

   ![위젯](./media/tutorial-table-space-sql-server/insight-table-space-result.png)

## <a name="working-with-the-insight-chart"></a>인사이트 차트 작업

Azure Data Studio의 인사이트 차트는 필터링 및 마우스 가리키기 세부 정보를 제공합니다. 다음 단계를 수행합니다.

1. 차트에서 *row_count* 범례를 클릭하고 토글합니다. 범례를 켜거나 끄면 Azure Data Studio에서 데이터 계열을 표시하거나 숨깁니다.

2. 차트를 마우스 포인터로 가리킵니다. 다음 스크린샷과 같이 Azure Data Studio에서 데이터 계열 레이블 및 해당 값에 대한 자세한 정보를 표시합니다.

   ![차트 토글 및 범례](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * 기본 제공 인사이트 위젯 샘플을 사용하여 인사이트 위젯 빠르게 켜기
> * 테이블 공간 사용량 세부 정보 보기
> * 인사이트 차트의 데이터 필터링 및 레이블 세부 정보 보기

사용자 지정 인사이트 위젯을 빌드하는 방법을 알아보려면 다음 자습서를 완료합니다.

> [!div class="nextstepaction"]
> [사용자 지정 인사이트 위젯 빌드](tutorial-build-custom-insight-sql-server.md)
