---
title: 외부 이미지 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 58875d6b3fd43962929096912d46f8157f02b77b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088782"
---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>외부 이미지 추가(보고서 작성기 및 SSRS)
  외부 이미지는 기본 모드나 SharePoint 통합 모드에 있는 보고서 서버 또는 다른 웹 사이트에 있을 수 있습니다. 보고서에 외부 이미지를 포함할 때는 해당 이미지가 존재하며 보고서를 읽는 사용자에게 해당 이미지에 액세스할 수 있는 권한이 있는지 확인해야 합니다. 자세한 내용은 [이미지&#40;보고서 작성기 및 SSRS&#41;](images-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>외부 이미지를 추가하려면  
  
1.  보고서 디자인 뷰의 **삽입** 탭에서 **이미지**를 클릭합니다.  
  
2.  디자인 화면에서 상자를 클릭한 다음 끌어 원하는 크기의 이미지를 만듭니다.  
  
3.  **이미지 속성** 대화 상자의 **일반** 탭에 있는 **이름** 입력란에 이름을 입력하거나 기본값을 적용합니다.  
  
4.  (옵션) **도구 설명** 입력란에서 HTML용으로 렌더링된 보고서에서 사용자가 마우스로 이미지를 가리킬 때 표시할 텍스트를 입력합니다.  
  
5.  **이미지 원본 선택**에서 **외부**를 선택합니다.  
  
     기본 모드의 보고서 서버에 있는 이미지를 지정하려면 **이 이미지 사용** 상자에 이미지의 상대 경로(예: ../images/image1.jpg)를 입력합니다.  
  
     SharePoint 통합 모드의 보고서 서버나 기타 웹 사이트에 있는 이미지를 지정하려면 **이 이미지 사용** 상자에 이미지의 전체 URL(예: http://\<SharePointservername>/\<site>/Documents/images/image1.jpg)을 입력합니다.  
  
     자세한 내용은 [외부 항목에 대한 경로 지정&#40;보고서 작성기 및 SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)을 참조하세요.  
  
6.  (옵션) **크기**, **표시 유형**, **동작**또는 **테두리** 를 클릭하여 이미지 보고서 항목의 추가 속성을 설정합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 이미지 포함 &#40;보고서 작성기 및 SSRS&#41;](embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [배경 이미지 추가&#40;보고서 작성기 및 SSRS&#41;](add-a-background-image-report-builder-and-ssrs.md)   
 [이미지 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  