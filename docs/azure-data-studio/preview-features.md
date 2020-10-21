---
title: Azure Data Studio의 미리 보기 기능
description: Azure Data Studio 미리 보기 기능과 이 기능을 사용하도록 설정하고 사용하는 방법을 자세히 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: hannahqin
ms.author: hanqin
ms.reviewer: maghan
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 8284300858be0dc8bcbf8bdf8f381e839fd7ae96
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060912"
---
# <a name="preview-features-in-azure-data-studio"></a>Azure Data Studio의 미리 보기 기능

Azure Data Studio에서는 새로운 기능과 개선 사항이 출시(GA)되기 전에 미리 보기 기능으로 처음 릴리스되는 경우가 많습니다. 기능이 미리 보기 상태로 유지되는 기간은 사용자 피드백, 품질 검사, 장기 로드맵에 따라 다를 수 있습니다. 미리 보기 기능을 사용하도록 설정하면 Azure Data Studio 기능에 대한 모든 권한과 초기 피드백을 제공할 기회를 얻을 수 있습니다.

## <a name="how-do-i-enable-preview-features"></a>미리 보기 기능을 사용하도록 설정하려면 어떻게 해야 하나요?

### <a name="on-first-launch"></a>처음 시작할 때

새 사용자인 경우 Azure Data Studio를 처음 시작할 때 미리 보기 기능을 옵트인할 수 있습니다. 시작 시 미리 보기 기능을 사용하거나 사용하지 않도록 설정하는 옵션을 제공하는 알림 메시지가 화면 오른쪽 아래에 표시됩니다. 미리 보기 기능을 사용하도록 설정하려면 **예(권장)** 를 선택합니다.

![처음 시작할 때 표시되는 미리 보기 알림 메시지](./media/getting-started/preview-toast-notification.png)

### <a name="in-settings"></a>설정에서

언제든지 설정에서 미리 보기 기능을 사용하거나 사용하지 않도록 설정할 수 있습니다.

1. 왼쪽 아래에 있는 **기어** 아이콘을 선택하고 상황에 맞는 메뉴에서 **설정**을 선택합니다. 설정 탭이 열립니다.

   ![ADS의 설정에 액세스하기 위한 기어 아이콘](./media/settings/open-settings-menu.png)

2. 검색 창에 “미리 보기 기능 사용”을 입력합니다.

3. 미리 보기 기능을 사용하도록 설정하려면 **Workbench: 미리 보기 기능 사용**에서 **릴리스되지 않은 미리 보기 기능 사용** 확인란을 선택합니다. 미리 보기 기능을 사용하지 않도록 설정하려면 확인란의 선택을 취소합니다.

   ![ADS의 미리 보기 기능 사용 설정](./media/settings/preview-features-settings.png)

## <a name="list-of-preview-features-in-azure-data-studio"></a>Azure Data Studio의 미리 보기 기능 목록

### <a name="general-features-in-preview"></a>미리 보기로 제공되는 일반 기능

* Azure Portal 통합
* 백업/복원
* 배포
    * SQL Edge
    * SQL Server 빅 데이터 클러스터
    * SQL Server 컨테이너 이미지
    * Windows의 SQL Server
* 기능 둘러보기
*  SQLCMD 모드
* 새 시작 페이지

### <a name="notebook-features-in-preview"></a>미리 보기로 제공되는 Notebook 기능

* dotnet 대화형 지원
* Markdown 도구 모음
*  새로운 Notebook 도구 모음
* Notebook 커널
    * Kusto
    * PowerShell
    * PySpark
    * Python
    * Spark | Scala
    * Spark | R
    * SQL
* 브라우저에서 Notebook 열기
* 고정된 Notebook
* Python 종속성 마법사

### <a name="first-party-extensions-in-preview"></a>미리 보기로 제공되는 Microsoft 확장

* SQL Server 관리 팩
* Azure SQL Data Warehouse Insights
* 중앙 관리 서버
* Windows용 데이터베이스 관리 도구 확장
* Kusto
* 언어 팩
* PostgreSQL
* PowerShell
* 쿼리 기록
* Azure Data Studio용 SandDance
* 서버 보고서
* SQL 평가
* SQL Server 에이전트
* SQL Server Profiler
* Machine Learning
* Managed Instance 대시보드
* Visual Studio IntelliCode
* whoisactive

## <a name="next-steps"></a>다음 단계

* [Azure Data Studio](what-is.md)
