---
title: 프로젝트 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- vs.newproject
- vs.addnewproject
helpviewer_keywords:
- projects [SQL Server Management Studio], creating
ms.assetid: 7897be19-365b-4b06-bcf0-8a669f67a673
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 693989d4a1dddd812d3f96279b23cd2218f2078c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182763"
---
# <a name="create-a-project"></a>프로젝트 만들기
  기존 솔루션 내에 하나 이상의 프로젝트를 만들 수 있습니다.  
  
### <a name="to-create-a-new-project-and-add-it-to-a-solution"></a>새 프로젝트를 만들어 솔루션에 추가하려면  
  
1.  솔루션 탐색기에서 솔루션을 선택합니다.  
  
2.  **파일** 메뉴에서 **추가**를 가리키고 **새 프로젝트**를 클릭합니다.  
  
3.  **새 프로젝트** 대화 상자에서 프로젝트의 유형을 클릭합니다.  
  
     **템플릿**  
     **템플릿** 상자에서 템플릿을 선택합니다. 선택한 프로젝트 템플릿에 대한 간략한 설명이 **템플릿** 상자 아래에 나타납니다.  
  
     **이름**  
     만들려는 스크립트 프로젝트의 이름을 입력합니다. **위치** 필드에 표시된 위치에 프로젝트와 동일한 이름을 가진 폴더도 생성됩니다. 일부 프로젝트의 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 원본 파일과 기타 지원 파일을 만들어 새 프로젝트 파일에 추가합니다.  
  
    > [!NOTE]  
    >  일부 프로젝트 유형의 경우 위치를 지정하면 이름이 설정되기 때문에 **이름** 입력란을 사용할 수 없습니다. 예를 들어 웹 애플리케이션과 웹 서비스는 웹 서버에 있으며 해당 서버에서 지정한 가상 디렉터리로부터 이름이 파생됩니다.  
  
     이름은 다음 문자를 포함할 수 없습니다.  
  
    -   파운드(#)  
  
    -   백분율(%)  
  
    -   앰퍼샌드 (&)  
  
    -   별표(*)  
  
    -   세로 막대(|)  
  
    -   백슬래시(\\)  
  
    -   콜론(:)  
  
    -   따옴표(")  
  
    -   보다 작음(\<)  
  
    -   보다 큼(>)  
  
    -   물음표(?)  
  
    -   슬래시(/)  
  
    -   선행 또는 후행 공백(' ')  
  
    -   Microsoft Windows 또는 MS-DOS에 예약된 이름(예: "nul", "aux", "con", "com1", "lpt1" 등)  
  
     **위치**  
     프로젝트를 만들 위치를 입력하거나 목록에서 선택합니다.  
  
     **찾아보기**  
     프로젝트를 저장할 새 디렉터리로 이동할 수 있는 **프로젝트 위치** 대화 상자를 표시합니다.  
  
     **해결 방법**  
     솔루션 탐색기에서 솔루션을 만들려면 **새 솔루션 만들기** 를 선택합니다. 현재 솔루션 탐색기에 열려 있는 솔루션에 새 프로젝트를 추가하려면 **솔루션에 추가** 를 선택합니다.  
  
     **솔루션용 디렉터리 만들기**  
     **(솔루션) 이름** 입력란을 활성화하려면 선택합니다. 이 옵션은 프로젝트 및 솔루션 이름으로 선택한 것과 같은 이름으로 새 디렉터리를 만듭니다.  
  
     **솔루션 이름**  
     프로젝트를 만들 새 솔루션의 이름을 입력합니다. 기본적으로 이 필드에서는 **이름** 필드에 입력한 것과 동일한 이름을 사용합니다.  
  
     **참고** 이 옵션에 액세스하려면 **솔루션** 에서 **새 솔루션 만들기** 확인란을 선택해야 하며 **솔루션용 디렉터리 만들기** 확인란도 선택해야 합니다. 웹 애플리케이션 등 일부 프로젝트 템플릿에서는 이 옵션이 지원되지 않습니다.  
  
     **소스 제어에 추가**  
     이 확인란을 선택한 경우 **확인**을 클릭하면 원본 제어 애플리케이션이 열립니다. 계속하려면 원본 제어 애플리케이션에 필요한 모든 정보를 입력합니다. 이 옵션을 사용하려면 원본 제어 클라이언트 애플리케이션이 설치되어 있어야 합니다.  
  
4.  **확인**을 클릭합니다.  
  
 스크립트 프로젝트의 이름을 설정할 수 있지만 폴더 이름은 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에 의해 설정되며 변경할 수 없습니다. **새 프로젝트 추가** 대화 상자를 사용하여 공통 폴더 집합에 대한 드라이브 및 경로 지정을 구성할 수 있습니다. **솔루션 탐색기**에서 솔루션 아이콘을 마우스 오른쪽 단추로 클릭한 다음 **추가**를 클릭합니다. 스크립트 프로젝트 폴더에 대한 기본 위치는 C:\Documents and Settings\\*username*\My Documents\SQL Server Management Studio\Projects\\입니다.  
  
## <a name="see-also"></a>관련 항목  
 [솔루션 탐색기](solution-explorer.md)   
 [솔루션에 기존 프로젝트 추가](add-an-existing-project-to-a-solution.md)   
 [프로젝트에 새 항목 추가](add-new-items-to-a-project.md)   
 [프로젝트에 기존 항목 추가](add-existing-items-to-a-project.md)   
 [프로젝트에 대 한 기본 위치 변경](change-the-default-location-for-projects.md)   
 [항목이 나 프로젝트 제거 또는 삭제](remove-or-delete-an-item-or-project.md)   
 [솔루션 삭제](delete-a-solution.md)  
  
  
