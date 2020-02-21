---
title: SSMS 구성 요소 및 구성
description: SQL Server Management Studio 환경에 대한 구성 요소 및 기본 구성 옵션을 설명하는 자습서입니다.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
ms.openlocfilehash: fe7518959f62328e038e7afb619b79cf2acbda86
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247287"
---
# <a name="sql-server-management-studio-components-and-configuration"></a>SQL Server Management Studio 구성 요소 및 구성

이 자습서에서는 SSMS(SQL Server Management Studio)의 다양한 창 구성 요소 및 작업 영역에 대한 몇 가지 기본 구성 옵션을 설명합니다. 이 문서에서는 다음 방법을 설명합니다. 

> [!div class="checklist"]
> * SSMS 환경을 구성하는 구성 요소 식별
> * 환경 레이아웃 변경 및 기본값으로 다시 설정
> * 쿼리 편집기 최대화
> * 글꼴 변경
> * 시작 옵션 구성
> * 구성을 기본값으로 재설정

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 SQL Server Management Studio가 필요합니다.  

* [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.

## <a name="sql-server-management-studio-components"></a>SQL Server Management Studio 구성 요소

이 섹션에서는 작업 영역에서 지원되는 다양한 창 구성 요소 및 사용 방법을 설명합니다.

* 창을 닫으려면 제목 표시줄의 오른쪽 모서리에 있는 **X**를 선택합니다.
* 창을 다시 열려면 **보기** 메뉴에서 창을 선택합니다.

    ![보기 메뉴](media/ssms-configuration/viewmenu.png)

* **개체 탐색기**(F8): 개체 탐색기는 서버에 있는 모든 데이터베이스 개체의 트리 뷰로, 이 보기에는 SQL Server 데이터베이스 엔진, SQL Server Analysis Services, SQL Server Reporting Services 및 SQL Server Integration Services의 데이터베이스가 포함됩니다. 개체 탐색기에는 연결된 모든 서버에 대한 정보가 포함되어 있습니다. 

    ![개체 탐색기](media/ssms-configuration/objectexplorer.png)
* **쿼리 창**(Ctrl+N): **새 쿼리**를 선택한 후에 이 창에 Transact-SQL(T-SQL) 쿼리를 입력합니다. 쿼리 결과도 여기에 나타납니다.

    ![새 쿼리 창](media/ssms-configuration/newquery.png)

* **속성**(F4): 쿼리 창이 열려 있을 때 속성 보기를 볼 수 있습니다. 보기는 쿼리의 기본 속성을 표시합니다. 예를 들어 쿼리가 시작된 시간, 반환된 행 수 및 연결 세부 정보를 표시합니다.  

    ![속성](media/ssms-configuration/properties.png)

* **템플릿 탐색기**(Ctrl+Alt+T): 템플릿 탐색기에는 다양한 미리 작성된 T-SQL 템플릿이 있습니다. 이러한 템플릿을 사용하여 데이터베이스 만들기 또는 백업과 같은 다양한 기능을 수행할 수 있습니다. 

    ![템플릿 탐색기](media/ssms-configuration/templates.png)

* **개체 탐색기 정보**(F7): 이 보기는 개체 탐색기의 보기보다 더 세부적입니다. 개체 탐색기 정보를 사용하여 동시에 여러 개체를 조작할 수 있습니다. 예를 들어 이 창에서 여러 데이터베이스를 선택한 다음, 해당 데이터베이스를 삭제하거나 동시에 스크립팅할 수 있습니다. 

    ![개체 탐색기 정보](media/ssms-configuration/objectexplorerdetails.PNG) 

## <a name="change-the-environment-layout"></a>환경 레이아웃 변경 

이 섹션에서는 다양한 창을 이동하는 방법 등 환경 레이아웃을 변경하는 방법을 설명합니다. 

* 창을 이동하려면 제목을 누른 상태에서 창을 끌어옵니다. 
* 창을 고정하거나 고정을 해제하려면 제목 표시줄에서 압정 아이콘을 선택합니다.

    ![개체 고정](media/ssms-configuration/pushpin.png)

* 각 창 구성 요소에는 다양한 방법으로 창을 조작하는 데 사용할 수 있는 드롭다운 메뉴가 있습니다. 

    ![창 옵션](media/ssms-configuration/windowoptions.png)

* 두 개 이상의 쿼리 창을 열면 두 쿼리 창을 볼 수 있도록 해당 창을 세로 또는 가로로 탭할 수 있습니다. 탭된 창을 보려면 쿼리 제목을 마우스 오른쪽 단추로 클릭한 다음, 원하는 탭된 옵션을 선택합니다.

    ![쿼리 탭 옵션](media/ssms-configuration/querytabbedoptions.png)

    * 가로 탭 그룹은 다음과 같습니다.

      ![가로 탭 그룹의 예제](media/ssms-configuration/horizontaltab.png)

    * 세로 탭 그룹은 다음과 같습니다.

      ![세로 탭 그룹의 예제](media/ssms-configuration/verticaltabgroup.png)

    * 탭을 병합하려면 쿼리 제목을 마우스 오른쪽 단추로 클릭한 다음, **이전 탭 그룹으로 이동** 또는 **다음 탭 그룹으로 이동**을 선택합니다.

      ![쿼리 탭 병합](media/ssms-configuration/mergetabgroups.png)

* 기본 환경 레이아웃을 복원하려면 **창** 메뉴에서 **창 레이아웃 다시 설정**을 선택합니다.

    ![창 레이아웃 복원](media/ssms-configuration/resetwindowlayout.png)

## <a name="maximize-query-editor"></a>쿼리 편집기 최대화

쿼리 편집기를 전체 화면 모드로 최대화할 수 있습니다.

1. 쿼리 편집기 창의 아무 곳이나 클릭합니다.

2. Shift+Alt+Enter 키를 눌러 전체 화면 모드와 일반 모드로 전환합니다. 

이 바로 가기 키는 모든 문서 창에서 작동합니다. 

## <a name="change-basic-settings"></a>기본 설정 변경

이 섹션에서는 **도구** 메뉴의 SSMS에서 몇 가지 기본 설정을 수정하는 방법을 설명합니다.

  ![도구 메뉴](media/ssms-configuration/tools.png)

* 강조 표시된 도구 모음을 수정하려면 **도구** > **사용자 지정**을 선택합니다.

    ![도구 모음 사용자 지정](media/ssms-configuration/toolbar.png)

### <a name="change-the-font"></a>글꼴 변경

* 글꼴을 변경하려면 **도구** > **옵션** > **글꼴 및 색**을 선택합니다.

     ![글꼴 및 색 변경](media/ssms-configuration/fontsandcolors.png)

### <a name="change-startup-options"></a>시작 옵션 변경

* 시작 옵션은 SSMS를 처음 열 때 작업 영역의 모양을 결정합니다. 시작 옵션을 변경하려면 **도구** > **옵션** > **시작**을 선택합니다.

    ![시작 옵션 변경](media/ssms-configuration/startup.png)

### <a name="reset-settings-to-the-default"></a>설정을 기본값으로 다시 설정

* 메뉴에서 이러한 모든 설정을 내보내고 가져올 수 있습니다. 설정을 가져오거나 내보내고, 기본 설정을 복원하려면 **도구** > **설정 가져오기 및 내보내기**를 선택합니다. 

    ![설정 가져오기 및 내보내기](media/ssms-configuration/settings.png)

## <a name="next-steps"></a>다음 단계

실습을 통해 SSMS에 익숙해지는 것이 가장 좋습니다. 이러한 *자습서* 및 *방법* 문서에서는 SSMS 내에서 사용할 수 있는 다양한 기능에 관해 도움을 얻을 수 있습니다.  이러한 문서에서는 SSMS의 구성 요소를 관리하는 방법과 정기적으로 사용하는 기능을 찾는 방법을 알아봅니다.

* [인스턴스에 연결 및 쿼리](connect-query-sql-server.md)
* [스크립팅](scripting-ssms.md)
* [SSMS에서 템플릿 사용](../template/templates-ssms.md)
* [SSMS 사용을 위한 추가 팁과 요령](ssms-tricks.md)