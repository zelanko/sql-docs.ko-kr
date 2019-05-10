---
title: '자습서: 테이블 공간 사용량 샘플 정보 위젯 사용'
titleSuffix: Azure Data Studio
description: 이 자습서는 Azure Data Studio 데이터베이스 대시보드의 테이블 공간 사용량 샘플 정보 위젯을 사용 하도록 설정 하는 방법을 보여 줍니다.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 6594aea6a618e2b9c4bd28368462f85c94a5ff0a
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089681"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>자습서: 테이블 공간 사용량 정보 위젯 사용한 샘플을 사용 하도록 설정 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

이 자습서는 데이터베이스의 모든 테이블에 대 한 공간 사용량에 대 한에 요약 뷰를 제공, 데이터베이스 대시보드의 정보 위젯을 사용 하도록 설정 하는 방법에 설명 합니다. 이 자습에서 배울 내용:

> [!div class="checklist"]
> * 기본 제공 정보 위젯 예제를 사용 하는 정보 위젯 신속 하 게 설정
> * 테이블 공간 사용량 세부 정보를 보려면
> * 데이터를 필터링 하 고 정보 차트 레이블을 세부 정보를 보려면

## <a name="prerequisites"></a>필수 구성 요소

이 자습서에서는 SQL Server 또는 Azure SQL Database의 *TutorialDB*가 필요합니다. *TutorialDB* 데이터베이스를 만들려면, 다음 빠른 시작 중 하나를 수행합니다.

- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)를 사용하여 SQL Server에 연결 및 쿼리
- [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)를 사용하여 Azure SQL Database에 연결 및 쿼리


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>관리 정보를 설정 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 데이터베이스 대시보드
[!INCLUDE[name-sos](../includes/name-sos-short.md)] 데이터베이스의 테이블에서 사용 된 공간을 모니터링 하는 기본 제공 샘플 위젯 했습니다.

1. 엽니다 *사용자 설정* 키를 눌러 **Ctrl + Shift + P** 열려는 합니다 *명령 팔레트*합니다.
2. 형식 *설정을* 검색 상자에 선택 **기본 설정: 사용자 설정을 엽니다**합니다.
2. 형식 *대시보드* 찾아서 설정 검색에서 입력 상자 **dashboard.database.widgets**합니다.

3. 사용자 지정 하는 **dashboard.database.widgets** 편집 하는 데 필요한 설정을 **dashboard.database.widgets** 항목에는 **사용자 설정** 섹션 (열은 오른쪽에 있음)입니다. 없는 경우 없습니다 **dashboard.database.widgets** 에 **사용자 설정** 섹션을 마우스로 합니다 **dashboard.database.widgets** 클릭 및 기본 설정 열에 텍스트 클릭 확인 하 고 텍스트의 왼쪽에 나타나는 연필 아이콘 **설정 복사할**합니다. 팝업에 표시 되 면 **설정에서 대체**를 클릭 하지 않음. 로 이동 합니다 **사용자 설정** 오른쪽에 열을 찾아서를 **dashboard.database.widgets** 섹션 및 다음 단계로 이동 합니다.

4. 에 **dashboard.database.widgets** 섹션에서 다음을 추가 합니다.

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
합니다 **dashboard.database.widgets** 섹션은 다음 이미지와 비슷하게 표시 됩니다.

   ![검색 설정](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. 키를 눌러 **Ctrl + S** 설정을 저장 합니다.

6. 마우스 오른쪽 단추로 클릭 하 여 열려 있는 데이터베이스 대시보드 **TutorialDB** 누릅니다 **관리**합니다.

7. 보기는 *테이블 공간* 다음 이미지에 표시 된 대로 정보 위젯: 

   ![위젯](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Insight 차트 사용

[!INCLUDE[name-sos](../includes/name-sos-short.md)]정보 차트 필터링 및 마우스 커서를 놓으면 세부 정보를 제공 합니다. 다음 단계를 사용해:

1. 클릭 하 고 설정/해제 합니다 *row_count* 차트에서 범례. [!INCLUDE[name-sos](../includes/name-sos-short.md)] 표시 되 고 범례 켜기 또는 끄기로 전환 하는 대로 데이터 계열 숨겨집니다.
    
2. 차트 위로 마우스 포인터를 가져갑니다. [!INCLUDE[name-sos](../includes/name-sos-short.md)] 데이터 계열 레이블 및 다음 스크린샷에 표시 된 대로 해당 값에 대 한 자세한 정보가 표시 됩니다.

   ![차트 설정/해제 및 범례](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음과 같은 방법을 학습했습니다.
> [!div class="checklist"]
> * 기본 제공 정보 위젯 샘플을 사용 하는 정보 위젯 신속 하 게 설정 합니다.
> * 테이블 공간 사용량의 세부 정보를 봅니다.
> * 데이터를 필터링 하 고 정보 차트 레이블을 세부 정보를 보려면

사용자 지정 정보 위젯을 빌드하는 방법에 알아보려면 다음 자습서를 완료 합니다.

> [!div class="nextstepaction"]
> [빌드 사용자 지정 정보 위젯](tutorial-build-custom-insight-sql-server.md)합니다.
