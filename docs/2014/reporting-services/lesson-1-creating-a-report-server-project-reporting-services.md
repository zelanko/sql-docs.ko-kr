---
title: '1단원: 보고서 서버 프로젝트 (Reporting Services) 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 48ad3fd25dd842ca1f4979a6875887d6ad656508
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56286471"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>1단원: 보고서 서버 프로젝트 만들기(Reporting Services)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 보고서를 만들려면 먼저 보고서 정의 파일(.rdl) 및 보고서에 필요한 다른 리소스 파일을 저장할 보고서 서버 프로젝트를 만들어야 합니다. 그런 다음 실제 보고서 정의 파일을 만들고 보고서에 대한 데이터 원본, 데이터 집합 및 보고서 레이아웃을 정의합니다. 보고서를 실행하면 실제 데이터가 검색되어 레이아웃과 결합된 후 해당 보고서를 내보내고 인쇄하고 저장할 수 있는 화면에 렌더링됩니다.  
  
 이 단원에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 보고서 서버 프로젝트를 만드는 방법을 설명합니다. 보고서 서버 프로젝트는 보고서 서버에서 실행되는 보고서를 만드는 데 사용됩니다.  
  
### <a name="to-create-a-report-server-project"></a>보고서 서버 프로젝트를 만들려면  
  
1.  클릭 **시작**, 가리킨 **모든 프로그램**를 가리킨 [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]를 클릭 하 고 **SQL Server Data Tools**. 처음으로이 경우 연 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], 클릭 **비즈니스 인텔리전스 설정** 기본 환경 설정에 대 한 합니다.  
  
2.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.  
  
3.  **설치된 템플릿** 목록에서 **비즈니스 인텔리전스**를 클릭합니다.  
  
4.  클릭 **보고서 서버 프로젝트**합니다.  
  
5.  **이름**에 **Tutorial**을 입력합니다.  
  
6.  **확인**을 클릭해 프로젝트를 만듭니다.  
  
     솔루션 탐색기에 Tutorial 프로젝트가 표시됩니다.  
  
### <a name="to-create-a-new-report-definition-file"></a>새 보고서 정의 파일을 만들려면  
  
1.  솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **보고서**를 가리키고 **추가**, 클릭 **새 항목**합니다.  
  
    > [!NOTE]  
    >  **솔루션 탐색기** 창이 표시되지 않으면 **보기** 메뉴에서 **솔루션 탐색기**를 클릭합니다.  
  
2.  에 **새 항목 추가** 대화 상자의 **템플릿**, 클릭 **보고서**합니다.  
  
3.  **이름**에 **Sales Orders.rdl** 을 입력한 후 **추가**를 클릭합니다.  
  
     보고서 디자이너가 열리고 새 .rdl 파일이 디자인 뷰에 표시됩니다.  
  
 보고서 디자이너는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 실행되는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]구성 요소로, 두 개의 뷰, 즉 **디자인** 하 고 **미리 보기**합니다. 뷰를 변경하려면 각 탭을 클릭해야 합니다.  
  
 **보고서 데이터** 창에서 데이터를 정의합니다. **디자인** 뷰에서는 보고서 레이아웃을 정의합니다. 보고서를 실행하고 **미리 보기** 뷰에서 보고서의 모양을 볼 수 있습니다.  
  
## <a name="next-task"></a>다음 태스크  
 "Tutorial" 보고서 프로젝트를 만들고 보고서 정의 파일(.rdl)을 보고서 프로젝트에 추가했습니다. 다음 단원에서는 보고서에 사용할 데이터 원본을 지정합니다. 참조 [2 단원: 연결 정보 지정 &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
