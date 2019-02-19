---
title: 외부 이미지 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8264dcb68687979588a709445885fdb50addf549
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295241"
---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>외부 이미지 추가(보고서 작성기 및 SSRS)
  외부 이미지는 기본 모드나 SharePoint 통합 모드에 있는 보고서 서버 또는 다른 웹 사이트에 있을 수 있습니다. 보고서에 외부 이미지를 포함할 때는 해당 이미지가 존재하며 보고서를 읽는 사용자에게 해당 이미지에 액세스할 수 있는 권한이 있는지 확인해야 합니다. 자세한 내용은 [이미지&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>외부 이미지를 추가하려면  
  
1.  보고서 디자인 뷰의 **삽입** 탭에서 **이미지**를 클릭합니다.  
  
2.  디자인 화면에서 상자를 클릭한 다음 끌어 원하는 크기의 이미지를 만듭니다.  
  
3.  **이미지 속성** 대화 상자의 **일반** 탭에 있는 **이름** 입력란에 이름을 입력하거나 기본값을 적용합니다.  
  
4.  (옵션) **도구 설명** 입력란에서 HTML용으로 렌더링된 보고서에서 사용자가 마우스로 이미지를 가리킬 때 표시할 텍스트를 입력합니다.  
  
5.  **이미지 원본 선택**에서 **외부**를 선택합니다.  
  
     기본 모드의 보고서 서버에 있는 이미지를 지정하려면 **이 이미지 사용** 상자에 이미지의 상대 경로(예: ../images/image1.jpg)를 입력합니다.  
  
     SharePoint 통합 모드의 보고서 서버 또는 다른 웹 사이트에 있는 이미지를 지정하려면 **이 이미지 사용** 상자에 이미지의 전체 URL을 입력합니다(예: https://\<SharePointservername>/\<site>/Documents/images/image1.jpg).  
  
     자세한 내용은 [외부 항목에 대한 경로 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)을 참조하세요.  
  
6.  (옵션) **크기**, **표시 유형**, **동작**또는 **테두리** 를 클릭하여 이미지 보고서 항목의 추가 속성을 설정합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 이미지 포함&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [배경 이미지 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md)   
 [이미지 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](https://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
