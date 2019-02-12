---
title: 보고서 프로젝트에 새 보고서 또는 기존 보고서 추가(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: bc714c2ffb7f4483823e7e49e9825c070a0b9672
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021414"
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>보고서 프로젝트에 새 보고서 또는 기존 보고서 추가(SSRS)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 보고서 마법사를 사용하거나 프로젝트에 새 보고서를 추가하여 새 보고서를 추가할 수 있습니다. 기본 보고서를 추가할 수도 있습니다. 보고서를 추가한 후 프로젝트의 **보고서** 폴더 아래에 나열된 보고서 이름을 볼 수 있습니다.  
  
> [!NOTE]  
>  기존 데이터 원본의 보고서를 미리 보려면 보고서 제작 클라이언트의 데이터 원본에 대한 사용 권한이 있어야 합니다. 자세한 내용은 [포함 또는 공유 데이터 원본 만들기 &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)합니다.  
  
 보고서를 추가한 후 데이터 원본 및 데이터 세트를 정의하고 보고서 레이아웃을 디자인할 수 있습니다. 시작하려면 [기본 테이블 보고서 만들기&#40;SSRS 자습서&#41;](../create-a-basic-table-report-ssrs-tutorial.md) 또는 [테이블&#40;보고서 작성기 및 SSRS&#41;](../report-design/tables-report-builder-and-ssrs.md)을 참조하세요.  
  
### <a name="to-add-a-new-report-using-the-report-wizard"></a>보고서 마법사를 사용하여 새 보고서를 추가하려면  
  
1.  솔루션 탐색기에서 보고서 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 보고서 추가**를 클릭합니다. **보고서 마법사** 대화 상자가 열립니다.  
  
     마법사는 데이터 원본을 만들고, 쿼리를 사용하여 데이터 세트를 만들고, 그룹을 정의하고, 레이아웃을 지정하고, 색 및 글꼴을 포함하는 스타일을 선택하고, 보고서를 만드는 단계를 안내합니다. 이 단계는 다음과 같습니다.  
  
    -   **데이터 원본 선택.** 보고서를 만드는 첫 번째 단계로 데이터 원본을 정의합니다. 보고서 마법사는 보고서 프로젝트의 전체 공유 데이터 원본 목록뿐만 아니라 새 데이터 원본을 만드는 옵션도 제공합니다.  
  
    -   **쿼리 디자인.** 두 번째 단계로 쿼리를 디자인합니다. 쿼리 문자열을 직접 입력하거나 쿼리 디자이너를 사용하여 작성하거나 다른 보고서에서 쿼리를 가져올 수 있습니다. 쿼리 디자이너에 대한 자세한 내용은 [Reporting Services Query Designers](../reporting-services-query-designers.md)를 참조하십시오.  
  
    -   **보고서 유형 선택.** 세 번째 단계로 원하는 보고서 유형을 선택합니다. 테이블 형식 보고서나 행렬 보고서를 선택할 수 있습니다. 테이블 형식 보고서의 열 수는 고정되어 있지만 행렬, 즉 크로스탭 보고서는 쿼리 결과에 따라 열 수가 달라집니다. 지도 보고서에는 지리적 배경과 함께 분석 데이터가 표시됩니다.  
  
    -   **스타일을 선택 합니다.** 다음 단계로 스타일 템플릿을 사용하여 보고서에 스타일을 적용합니다. 템플릿을 선택하여 글꼴, 색, 테두리 스타일 등의 스타일을 보고서에 적용합니다. 보고서 디자이너는 6개의 스타일 템플릿인 Slate, Forest, Corporate, Bold, Ocean 및 Generic을 제공합니다. 다른 스타일 템플릿을 추가할 수도 있습니다.  
  
        > [!NOTE]  
        >  기존 템플릿을 변경 하거나 \Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\Business Intelligence Wizards\Reports\Styles의에서 StyleTemplates.xml 파일을 편집 하 여 새 템플릿을 추가할 수 있습니다\\< l a n g\>폴더를 위치 \<l a n g >은 사용 중인 언어 (의 영어 버전을 사용 하는 경우에 예를 들어 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], 폴더 이름은 "EN"). 이 폴더는 보고서 디자이너가 설치된 컴퓨터에 있습니다. StyleTemplates.xml 파일에는 두 개의 복사본이 있습니다. 보고서 마법사를 통해 적용되는 스타일을 수정하려면 사용하는 언어에 대해 생성된 폴더에 있는 파일을 편집합니다.  
  
    -   **보고서 이름을 지정합니다.**  마지막 단계로 보고서의 이름을 지정하고 보고서에 포함할 필드를 확인합니다. 모든 단계가 완료되면 보고서 디자이너는 보고서를 만들어 보고서 서버 프로젝트에 추가합니다.  
  
### <a name="to-add-a-new-blank-report"></a>새 보고서를 추가하려면  
  
1.  **프로젝트** 메뉴에서 **새 항목 추가**를 클릭합니다.  
  
2.  **템플릿**에서 **보고서**를 클릭합니다.  
  
3.  **추가**를 클릭합니다.  
  
     새 보고서가 프로젝트에 추가되어 디자인 화면에 표시됩니다.  
  
### <a name="to-add-an-existing-report"></a>기존 보고서를 추가하려면  
  
1.  **프로젝트** 메뉴에서 클릭 **추가**를 차례로 **기존 항목**합니다.  
  
2.  .rdl 파일의 위치를 찾아서 파일을 선택한 다음 **추가**를 클릭합니다.  
  
     보고서가 **보고서** 폴더 아래의 프로젝트에 추가됩니다. 프로젝트를 닫고 다시 열면 보고서가 사전순으로 정렬됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services&#40;SSRS&#41; 자습서](../reporting-services-tutorials-ssrs.md)  
  
  
