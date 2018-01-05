---
title: "자습서: SQL 작업 Studio (미리 보기)에서 테이블 공간 사용량 샘플 통찰력 위젯을 사용 하도록 설정 | Microsoft Docs"
description: "이 자습서에는 테이블 공간 사용량 샘플 통찰력 위젯 SQL 작업 Studio (미리 보기) 데이터베이스를 사용 하도록 설정 하는 방법을 보여 줍니다."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c51c7d1804baa490e665d316a08d911038c9f11
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>자습서: 테이블 공간 사용량 통찰력 위젯 사용한 샘플을 사용 하도록 설정[!INCLUDE[name-sos](../includes/name-sos-short.md)]

이 자습서에서는 데이터베이스의 모든 테이블에 대 한 공간 사용에 대 한 프로그램에서 요약 보기를 제공 하는 데이터베이스 대시보드에서 통찰력 위젯 사용 하도록 설정 하는 방법을 설명 합니다. 이 자습서는 방법을 배웁니다 하는 방법:

> [!div class="checklist"]
> * 기본 제공 통찰력 위젯 예제를 사용 하 여 통찰력 위젯은 신속 하 게 설정
> * 테이블 공간 사용량 정보 보기
> * 데이터를 필터링 하 고 통찰력 차트에서 레이블 내용을 보려면

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에서는 SQL Server 또는 Azure SQL 데이터베이스 *TutorialDB*합니다. 만들려는 *TutorialDB* 데이터베이스에서 다음 퀵 스타트 중 하나를 완료 합니다.

- [연결 및 SQL Server를 사용 하 여 쿼리[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [연결 및 Azure SQL 데이터베이스를 사용 하 여 쿼리[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>관리 정보를 설정 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 데이터베이스 대시보드
[!INCLUDE[name-sos](../includes/name-sos-short.md)]에 기본 제공 샘플 위젯을 데이터베이스의 테이블에서 사용 하는 공간을 모니터링 합니다.

1. 열고 **사용자 설정** 키를 눌러 **Ctrl + Shift + P** 열려는 *명령 팔레트*, 형식 *설정을* 선택 고검색상자 **기본 설정: 사용자 설정 열기**합니다.

   ![열기 사용자 설정 명령](./media/tutorial-table-space-sql-server/open-user-settings.png)

2. 형식 *대시보드* 찾은 설정 검색 입력 상자 **dashboard.database.widgets**합니다.

   ![검색 설정](./media/tutorial-table-space-sql-server/search-settings.png)

3. 사용자 지정 하는 **dashboard.database.widgets** 의 왼쪽에 있는 연필 아이콘 위에 마우스를 가져가고 설정을 **dashboard.database.widgets** 텍스트를 클릭 하 여 **편집**  >  **설정 복사**합니다.

4. 사용 하 여 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 통찰력 설정은 IntelliSense, 구성 *이름* 위젯 제목에 대 한 *gridItemConfig* 위젯 크기에 대 한 및 *위젯* 선택 하 여 **테이블 공간-db 통찰력** 다음 스크린샷에 표시 된 것 처럼 드롭 다운 목록에서:

   ![정보 설정](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. 키를 눌러 **Ctrl + S** 설정을 저장할 수 있습니다.

6. 마우스 오른쪽 단추로 클릭 하 여 열려 있는 데이터베이스 대시보드 **TutorialDB** 클릭 **관리**합니다.

   ![대시보드 열기](./media/tutorial-table-space-sql-server/insight-open-dashboard.png)

7. 보기 *테이블에서 사용 되는 공간* 다음 스크린샷에 표시 된 것 처럼: 

   ![위젯](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>작업에 대 한 정보 차트

[!INCLUDE[name-sos](../includes/name-sos-short.md)]통찰력 차트 필터링 및 마우스 호버 세부 정보를 제공 합니다. 다음 단계를 수행해:

1. 클릭 하 고 설정/해제는 *row_count* 차트의 범례입니다. [!INCLUDE[name-sos](../includes/name-sos-short.md)]표시 하 고 켜거나 범례를 전환할 때 데이터 계열을 숨깁니다.
    
2. 차트 위로 마우스 포인터를 가져갑니다. [!INCLUDE[name-sos](../includes/name-sos-short.md)]데이터 계열 레이블 및 다음 스크린샷에 표시 된 대로 해당 값에 대 한 자세한 정보가 표시 됩니다.

   ![차트 설정/해제 및 범례](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>다음 단계
이 자습서에서는 알아보았습니다 하는 방법:
> [!div class="checklist"]
> * 기본 제공 통찰력 위젯 샘플을 사용 하 여 통찰력 위젯은 신속 하 게 설정 합니다.
> * 테이블 공간 사용량의 세부 정보를 봅니다.
> * 데이터를 필터링 하 고 통찰력 차트에서 레이블 내용을 보려면

사용자 지정 통찰력 위젯 빌드하는 방법을 알아보려면 다음 자습서를 완료 합니다.

> [!div class="nextstepaction"]
> [빌드 사용자 지정 통찰력 위젯](tutorial-build-custom-insight-sql-server.md)합니다.