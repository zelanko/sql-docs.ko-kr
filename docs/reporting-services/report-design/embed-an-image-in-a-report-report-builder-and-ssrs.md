---
title: "(보고서 작성기 및 SSRS) 보고서에 이미지 포함 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.embeddedimages.f1
- "10060"
ms.assetid: aed77345-5eeb-41f0-96c9-db6b4a11ec6f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a1825a28cd9939228a73c1a4a6269c717b691ab2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="embed-an-image-in-a-report-report-builder-and-ssrs"></a>보고서에 이미지 포함(보고서 작성기 및 SSRS)
  보고서에 포함 이미지를 포함할 수 있습니다. 이미지를 포함하면 보고서에서 항상 이미지를 사용할 수 있지만 보고서 정의 즉, 보고서를 정의하는 파일의 크기도 늘어납니다. 보고서에 포함된 이미지는 보고서 데이터 창에 나열됩니다.  
  
 디자인 화면에 이미지를 추가하기 전에 보고서 정의에 이미지를 포함할 수 있습니다. 자세한 내용은 [배경 이미지 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-a-report"></a>보고서에 이미지를 포함하려면  
  
1.  보고서 디자인 뷰의 **삽입** 탭에서 **이미지**를 클릭합니다.  
  
2.  디자인 화면에서 상자를 클릭한 다음 끌어 원하는 크기의 이미지를 만듭니다.  
  
3.  **이미지 속성** 대화 상자의 **일반** 페이지에 있는 **이름** 입력란에 이름을 입력하거나 기본값을 적용합니다.  
  
4.  (옵션) 렌더링된 보고서에서 사용자가 마우스로 이미지를 가리킬 때 표시할 텍스트를 **도구 설명** 입력란에 입력합니다.  
  
5.  **이미지 원본 선택**에서 **포함**을 선택합니다.  
  
6.  **이 이미지 사용** 입력란 옆의 **가져오기** 단추를 클릭합니다.  
  
7.  **파일 형식**에서 이미지 파일 형식을 선택하고 파일을 탐색한 다음 **열기**를 클릭합니다.  
  
8.  **이미지 속성** 대화 상자에서 **확인**을 클릭합니다.  
  
     디자인 화면에 그린 상자에 이미지가 표시되고 보고서 데이터 창의 이미지 폴더 아래에 파일이 표시됩니다.  
  
    > [!NOTE]  
    >  이미지를 가져오면 MIME 형식(예: bmp)도 자동으로 파생됩니다. MIME 형식을 변경하려면 다음 절차를 참조하십시오.  
  
### <a name="optional-to-change-the-mime-type-of-an-imported-image"></a>가져온 이미지의 MIME 형식을 변경하려면(옵션)  
  
1.  디자인 뷰에서 보고서를 엽니다.  
  
2.  디자인 화면에서 이미지를 선택합니다. **속성** 창에 이미지 속성이 표시됩니다.  
  
    > [!NOTE]  
    >  속성 창이 표시되지 않으면 **보기** 탭에서 **속성**을 클릭합니다.  
  
3.  **MIMEType** 속성 옆의 입력란을 클릭하고 드롭다운 목록에서 새 MIME 형식을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [이미지 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [데이터 바인딩된 이미지 &#40; 추가 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/add-a-data-bound-image-report-builder-and-ssrs.md)   
 [이미지 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
