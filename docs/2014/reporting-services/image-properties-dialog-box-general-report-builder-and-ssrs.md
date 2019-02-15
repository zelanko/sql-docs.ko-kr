---
title: 이미지 속성 대화 상자, 일반 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10051"
- sql12.rtp.rptdesigner.pictureproperties.general.f1
ms.assetid: c2218b93-f7fe-46ef-995f-d7dadf9752ec
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b229d54be6a785d145f33d36c7ce8bcc6d28af6f
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292941"
---
# <a name="image-properties-dialog-box-general-report-builder-and-ssrs"></a>이미지 속성 대화 상자, 일반(보고서 작성기 및 SSRS)
  **이미지 속성** 대화 상자에서 **일반** 을 선택하여 그림을 추가하고, 이미지의 기본 이름을 변경하고, 도구 설명 텍스트를 추가할 수 있습니다.  
  
## <a name="options"></a>변수  
 **이름**  
 항목의 이름을 입력합니다. 이름은 보고서 내에서 고유해야 합니다. 기본적으로 Image1 또는 Image2 같은 일반적인 이름이 할당됩니다.  
  
 **Tooltip**  
 도구 설명을 반환하는 식 또는 텍스트를 입력합니다. 식을 편집하려면 식(*fx*) 단추를 클릭합니다. HTML 보고서의 항목 위에 포인터를 놓으면 **도구 설명** 이 나타납니다.  
  
 **이미지 원본 선택**  
 보고서를 렌더링할 때 보고서 프로세서에서 이미지를 가져올 위치를 알 수 있도록 이미지가 저장되어 있는 위치를 가리킵니다.  
  
-   **외부** 보고서 서버 또는 웹 서버에서 이미지를 파일로 유지하려면 이 옵션을 선택합니다.  
  
-   **포함** 이미지를 보고서에 포함하려면 이 옵션을 선택합니다.  
  
-   **데이터베이스** 보고서에 포함할 이미지를 나타내는 데이터베이스 필드 이름을 포함하려면 이 옵션을 선택합니다.  
  
 **이 이미지 사용**  
 **포함** 또는 **외부** 옵션을 선택하면 이 옵션이 나타납니다.  
  
 이미지를 포함하려는 경우 드롭다운 목록에서 보고서에 추가할 이미지를 선택합니다. **가져오기** 단추를 클릭하여 드롭다운 목록에 이미지를 추가합니다.  
  
 **외부** 옵션을 선택할 경우 이미지의 URL을 입력합니다. 기본 모드로 구성된 보고서 서버에 게시된 보고서의 경우 전체 경로나 상대 경로를 사용합니다(예: 예를 들어, http://\<서버 이름 > / images/image1.jpg입니다. SharePoint 통합 모드로 구성된 보고서 서버에 게시된 보고서의 경우 정규화된 URL을 사용합니다(예: 예를 들어, http://\<*SharePointservername*>/\<*사이트*> / Documents/images/image1.jpg입니다.  
  
 **가져오기**  
 **이 이미지 사용** 드롭다운 목록에 이미지를 추가하려면 클릭합니다.  
  
 **이 필드 사용**  
 **데이터베이스** 옵션을 선택하면 이 옵션이 나타납니다. 필드 이름을 선택합니다.  
  
 **이 MIME 형식 사용**  
 데이터베이스에 포함된 이미지에 적합한 형식을 선택합니다(예: .bmp, .jpeg, .gif, .png, .x-png).  
  
## <a name="see-also"></a>관련 항목  
 [식 예&#40;보고서 작성기 및 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [이미지&#40;보고서 작성기 및 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [대화 상자, 창 및 마법사에 대한 보고서 작성기 도움말](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
