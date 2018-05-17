---
Title: 'Tutorial: SQL Server Management Studio Components and Configuration'
description: SQL Server Management Studio 환경에 대한 구성 요소 및 기본 구성 옵션을 설명하는 자습서입니다.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 51fb197c3b5177c699134a48fc4888cd134e1711
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="tutorial-sql-server-management-studio-components-and-configuration"></a>자습서: SQL Server Management Studio 구성 요소 및 구성
이 자습서에서는 SSMS(SQL Server Management Studio) 내의 다양한 창 구성 요소 및 작업 영역에 대한 몇 가지 기본 구성 옵션을 설명합니다. 이 문서에서는 다음을 알아봅니다. 

> [!div class="checklist"]
> * SSMS 환경을 구성하는 다양한 구성 요소
> * 환경 레이아웃 변경 및 기본값으로 다시 설정
> * 쿼리 편집기 최대화
> * 글꼴 변경 
> * 시작 옵션 구성 
> * 구성을 기본값으로 다시 설정 

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio가 필요합니다.  

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.

## <a name="sql-server-management-studio-components"></a>SQL Server Management Studio 구성 요소
이 섹션에서는 작업 영역에서 사용할 수 있는 다양한 창 구성 요소 및 해당 용도를 다룹니다. 

- 모든 창 구성 요소는 제목 표시줄의 모서리에 있는 X를 눌러 닫은 다음, 주 메뉴의 **보기** 드롭다운에서 다시 열 수 있습니다. 

    ![보기 메뉴](media/ssms-configuration/viewmenu.png)

- **개체 탐색기**(F8): 개체 탐색기는 서버에 있는 모든 데이터베이스 개체의 트리 뷰입니다. 이는 SQL Server 데이터베이스 엔진, Analysis Services, Reporting Services 및 Integration Services의 데이터베이스를 포함할 수 있습니다. 개체 탐색기에는 연결된 모든 서버에 대한 정보가 포함되어 있습니다. 
    
    ![개체 탐색기](media/ssms-configuration/objectexplorer.png)
- **쿼리 창**(Ctrl + N): **새 쿼리**를 클릭하면 T-SQL(Transact-SQL) 쿼리를 입력하는 창입니다. 쿼리의 결과를 여기에서도 볼 수 있습니다.
    
    ![새 쿼리 창](media/ssms-configuration/newquery.png)

- **속성**(F4): **쿼리 창**이 열려 있으면 볼 수 있으며 쿼리의 기본 속성을 표시합니다. 예를 들어 쿼리가 시작된 시간, 반환된 행 수 및 연결 세부 정보를 표시합니다.  

    ![속성](media/ssms-configuration/properties.png)

- **템플릿 탐색기**(Ctrl + Alt + T): 템플릿 탐색기에서 찾을 수 있는 미리 빌드된 다양한 T-SQL 템플릿이 있습니다. 이러한 템플릿을 사용하여 데이터베이스 만들기 또는 백업과 같은 다양한 기능을 수행할 수 있습니다. 

    ![템플릿 탐색기](media/ssms-configuration/templates.png)

- **개체 탐색기 정보**(F7): 개체 탐색기에서 볼 수 있는 더욱 세분화된 보기이며 한 번에 여러 개체를 조작할 수 있습니다. 예를 들어 개체 탐색기 정보 창을 통해 여러 데이터베이스를 동시에 선택하고 삭제하거나 스크립팅할 수 있습니다. 

    ![개체 탐색기 정보](media/ssms-configuration/objectexplorerdetails.PNG) 
 

    

## <a name="change-the-environmental-layout"></a>환경 레이아웃 변경 
이 섹션에서는 다양한 창 이동과 같은 환경 레이아웃 조작을 설명합니다. 

-  제목을 누른 채로 창을 끌어 각 창 구성 요소를 이동할 수 있습니다. 
- 제목 표시줄에서 압정 아이콘을 선택하여 각 창 구성 요소를 고정하고 고정 해제할 수 있습니다.
    
    ![개체 고정](media/ssms-configuration/pushpin.png)

- 각 창 구성 요소에는 다양한 방법으로 창을 조작할 수 있는 드롭다운 화살표가 있습니다. 

    ![창 옵션](media/ssms-configuration/windowoptions.png)

- 두 개 이상의 쿼리 창을 열면 두 쿼리 창을 한 번에 볼 수 있도록 세로 또는 가로로 탭할 수 있습니다. 이를 위해 쿼리의 제목을 마우스 오른쪽 단추로 클릭하고 원하는 탭된 옵션을 선택합니다. 
 
    ![쿼리 탭 옵션](media/ssms-configuration/querytabbedoptions.png)

    - 이는 **가로 탭 그룹**입니다. ![가로 탭 그룹](media/ssms-configuration/horizontaltab.png)     
    
    - 이는 **세로 탭 그룹**입니다.  
        ![세로 탭 그룹](media/ssms-configuration/verticaltabgroup.png)
        

    - 탭을 다시 병합하려면 쿼리 제목을 마우스 오른쪽 단추로 다시 클릭하고 **다음 탭 그룹으로 이동**하거나 **이전 탭 그룹으로 이동**합니다.
    
        ![쿼리 탭 병합](media/ssms-configuration/mergetabgroups.png)

- 기본 환경 레이아웃을 복원하려면 **창 메뉴** > **창 레이아웃 다시 설정**을 클릭합니다.
 
    ![창 레이아웃 복원](media/ssms-configuration/resetwindowlayout.png)
    
## <a name="maximize-query-editor"></a>쿼리 편집기 최대화
쿼리 편집기를 전체 화면 모드로 최대화할 수 있습니다.

1. 쿼리 편집기 창 내의 아무 곳이나 클릭합니다.
2. SHIFT + ALT + ENTER 키를 눌러 전체 화면 모드와 일반 모드 사이를 전환합니다. 

이 바로 가기 키는 모든 문서 창에서 작동합니다. 



## <a name="change-basic-settings"></a>기본 설정 변경
이 섹션에서는 SSMS 내의 몇 가지 기본 설정을 수정하는 방법을 설명합니다. 이러한 옵션은 **도구** 메뉴 옵션 내에 있습니다.

  ![도구 메뉴](media/ssms-configuration/tools.png)


- 메뉴: **도구** > **사용자 지정**으로 이동하여 강조 표시된 도구 모음을 수정할 수 있습니다.

    ![도구 모음 사용자 지정](media/ssms-configuration/toolbar.png)

### <a name="change-the-font"></a>글꼴 변경
- 메뉴: **도구** > **옵션** > **글꼴 및 색**에서 글꼴을 변경할 수 있습니다.

     ![글꼴 및 색](media/ssms-configuration/fontsandcolors.png)

### <a name="change-the-startup-options"></a>시작 옵션 변경
- 시작 옵션은 SSMS를 처음 시작할 때 작업 영역의 모양을 결정합니다. 메뉴: **도구** > **옵션** > **시작**에서 구성할 수 있습니다.
 
    ![시작 옵션](media/ssms-configuration/startup.png)

### <a name="reset-settings-to-default"></a>설정을 기본값으로 다시 설정
- 메뉴: **도구** > **설정 가져오기 및 내보내기**에서 이러한 모든 설정을 내보내고 가져올 수 있습니다. 

    ![가져오기 + 내보내기 설정](media/ssms-configuration/settings.png)
    - 여기에서 모든 설정을 기본값으로 다시 설정할 수도 있습니다. 


## <a name="next-steps"></a>다음 단계
다음 아티클에서는 SQL Server 오류 로그 및 SQL 인스턴스 이름 찾기 등 SSMS를 사용하는 몇 가지 추가 팁과 요령을 설명합니다. 

자세히 알아보려면 다음 문서로 진행합니다.
> [!div class="nextstepaction"]
> [다음 단계 단추](ssms-tricks.md)
 
 




