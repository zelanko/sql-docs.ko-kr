---
title: 포함 또는 공유 데이터 원본 (SSRS) 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], creating
ms.assetid: b111a8d0-a60d-4c8b-b00a-51644b19c34b
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ff7f9c94aded21d70ea4b6ef6b31d2f8094f2592
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289811"
---
# <a name="create-an-embedded-or-shared-data-source-ssrs"></a>포함된 데이터 원본 또는 공유 데이터 원본 만들기(SSRS)
  보고서 데이터 원본은 이름 및 연결 정보를 지정합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 두 종류의 데이터 원본 지원 합니다: 포함 된 데이터 원본과 공유 합니다. 포함된 데이터 원본은 보고서 정의에서 정의되고 해당 보고서에서만 사용됩니다. 공유 데이터 원본은 개별 항목으로 정의되고 여러 보고서에서 사용될 수 있습니다. 자세한 내용은 [포함 및 공유 데이터 연결 또는 데이터 원본 &#40;보고서 작성기 및 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)합니다.  
  
 보고서 작성기에서 보고서 서버 또는 SharePoint 사이트를 찾은 다음 포함된 데이터 원본을 만들거나 데이터 원본을 선택합니다. 보고서 작성기에서는 공유 데이터 원본을 만들 수 없습니다.  
  
 보고서 디자이너에서는 공유 데이터 원본 또는 포함된 데이터 원본을 만들 수 있습니다. 보고서 데이터 창에서 데이터 원본 참조를 만들려면 시작 하 고 다음을 선택 합니다 **새로 만들기** 옵션입니다. 데이터 원본 참조를 만들고 나면 새 공유 데이터 원본은 솔루션 탐색기의 공유 데이터 원본 폴더에 자동으로 추가됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 공유 데이터 원본을 보고서 서버 또는 SharePoint 사이트에서 직접 만들 수도 있습니다. 자세한 내용은 [만들기, 삭제 또는 공유 데이터 원본을 수정 &#40;보고서 관리자&#41; ](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md) 하거나 [만들기 및 공유 데이터 원본 관리 &#40;&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
### <a name="to-create-an-embedded-or-shared-data-source"></a>포함된 데이터 원본 또는 공유 데이터 원본을 만들려면  
  
1.  보고서 데이터 창의 도구 모음에서 **새로 만들기** , **데이터 원본**을 차례로 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
    > [!NOTE]  
    >  보고서 데이터 창이 표시되지 않는 경우 **보기** 메뉴에서 **보고서 데이터** 를 클릭합니다.  
  
2.  **이름** 입력란에 데이터 원본 이름을 입력하거나 기본값을 적용합니다. 데이터 원본 이름은 보고서 내부에서만 사용됩니다. 의미를 명확하게 전달하려면 연결 문자열에서 지정된 데이터베이스의 이름을 데이터 원본 이름에 포함하는 것이 좋습니다.  
  
3.  포함 된 데이터 원본의 경우 있는지를 확인 **포함 된 연결** 을 선택 합니다.  
  
    1.  **유형** 드롭다운 목록에서 데이터 원본 유형(예: **Microsoft SQL Server** 또는 **OLE DB**)을 선택합니다.  
  
    2.  다음 대체 방법 중 하나를 사용하여 연결 문자열을 지정합니다.  
  
    -   **연결 문자열** 입력란에 연결 문자열을 직접 입력합니다. 연결 문자열 예 목록은 참조 하세요 [데이터 연결, 데이터 원본 및 보고서 작성기에서 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md) 또는 [데이터 연결, 데이터 원본 및 연결 Strings in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
    -   식 단추(**fx** )를 클릭하여 연결 문자열로 계산되는 식을 만듭니다. **식** 대화 상자의 식 창에 식을 입력합니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    -   2단계에서 선택한 데이터 원본 유형에 대해 **편집** 을 클릭하여 **연결 속성** 대화 상자를 엽니다.  
  
         **연결 속성** 대화 상자의 필드에 데이터 원본 유형에 대해 적합한 항목을 입력합니다. 연결 속성에는 데이터 원본 유형, 데이터 원본 이름 및 사용할 자격 증명이 포함됩니다. 이 대화 상자에서 값을 지정한 후 **연결 테스트** 를 클릭하여 데이터 원본이 사용 가능한지와 지정한 자격 증명이 올바른지 확인합니다. 특정 데이터 원본 유형에 대한 자세한 내용은 [외부 데이터 원본의 데이터 추가&#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md)의 항목을 참조하세요.  
  
4.  공유 데이터 원본에 대 한 있는지를 확인 **공유 데이터 원본 참조 사용** 을 선택 합니다.  
  
    1.  **새로 만들기**를 클릭합니다. **공유 데이터 원본** 속성 대화 상자에서 2단계 및 3단계를 수행하여 새 데이터 원본을 만듭니다.  
  
    2.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
         새 공유 데이터 원본이 솔루션 탐색기의 공유 데이터 원본 폴더에 나타납니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     데이터 원본이 보고서 데이터 창에 나타납니다. 보고서 데이터 창에서 공유 데이터 원본은 데이터 원본 정의를 가리킵니다. 보고서 작성기에서 데이터 원본 정의는 보고서 서버 또는 SharePoint 사이트에 있습니다. 보고서 디자이너에서 데이터 원본 정의는 솔루션 탐색기의 공유 데이터 원본 폴더에 있는 파일입니다.  
  
### <a name="to-import-an-existing-data-source-in-report-designer"></a>보고서 디자이너에서 기존 데이터 원본을 가져오려면  
  
1.  솔루션 탐색기의 보고서 서버 프로젝트에서 **공유 데이터 원본** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **기존 항목 추가**를 클릭합니다. **기존 항목 추가** 대화 상자가 열립니다.  
  
2.  보고서 정의 공유 데이터 원본 파일(rds)을 탐색한 다음 **열기**를 클릭합니다.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-convert-an-embedded-data-source-to-a-shared-data-source-in-report-designer"></a>보고서 디자이너에서 포함된 데이터 원본을 공유 데이터 원본으로 변환하려면  
  
-   보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭 하 고 클릭 **공유 데이터 원본으로 변환**합니다.  
  
### <a name="to-convert-a-shared-data-source-to-an-embedded-data-source-in-report-builder"></a>보고서 작성기에서 공유 데이터 원본을 포함된 데이터 원본으로 변환하려면  
  
-   보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭 하 고 엽니다 **데이터 원본 속성**합니다.  
  
-   클릭 **포함 된 연결** 하 고 이전 절차에서 설명한 대로 포함된 된 데이터 원본 만들기를 완료 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 데이터 원본에 자격 증명 저장](report-data/store-credentials-in-a-reporting-services-data-source.md)   
 [포함된 데이터 연결 및 공유 데이터 연결 또는 데이터 원본&#40;보고서 작성기 및 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [공유 데이터 원본에서 데이터 원본을 포함 하는 변환 &#40;보고서 작성기 및 SSRS&#41;](report-data/convert-data-sources-report-builder-and-ssrs.md)   
 [보고서 또는 모델을 공유 데이터 원본에 바인딩&#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [보고서의 데이터 원본 속성 구성&#40;보고서 관리자&#41;](report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
