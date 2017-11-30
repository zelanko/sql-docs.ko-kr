---
title: "데이터 바인딩된 이미지 추가(보고서 작성기 및 SSRS) | Microsoft Docs"
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
ms.assetid: df4c38d4-bfcc-41c4-aa6d-952ca6fd7a2e
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 17aa516d14553478e2659b96fe8108d7b985b42e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="add-a-data-bound-image-report-builder-and-ssrs"></a>데이터 바인딩된 이미지 추가(보고서 작성기 및 SSRS)
  데이터베이스에 저장된 이미지에 대한 참조를 보고서에 포함할 수 있습니다. 이러한 이미지를 *데이터 바인딩된 이미지*라고 합니다. 제품 목록에서 제품 이름과 함께 표시되는 그림을 예로 들 수 있습니다.  
  
 데이터 바인딩된 이미지를 페이지 머리글이나 페이지 바닥글에 추가하려면 별도의 단계가 필요합니다. 자세한 내용은 [페이지 머리글 및 바닥글&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-data-bound-image"></a>데이터 바인딩된 이미지를 추가하려면  
  
1.  보고서 디자인 뷰에서 데이터 원본 연결이 있는 테이블과 이진 이미지 데이터가 포함된 필드가 있는 데이터 집합을 만듭니다. 자세한 내용은 [테이블&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)을 참조하세요.  
  
2.  테이블에 열을 삽입합니다. 자세한 내용은 [열 삽입 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)를 참조하세요.  
  
3.  **삽입** 메뉴에서 **이미지**를 클릭한 다음 새 열의 데이터 행을 클릭합니다.  
  
4.  **이미지 속성** 대화 상자의 일반 페이지에 있는 **이름** 입력란에 이름을 입력하거나 기본값을 적용합니다.  
  
5.  (옵션) HTML용으로 렌더링된 보고서에서 사용자가 마우스로 이미지를 가리킬 때 표시할 텍스트를 **도구 설명** 입력란에 입력합니다.  
  
6.  **이미지 원본 선택**에서 **데이터베이스**를 선택합니다.  
  
7.  **이 필드 사용**에서 보고서의 이미지를 포함하는 필드를 선택합니다.  
  
8.  **이 MIME 형식 사용**에서 이미지의 MIME 형식 또는 파일 형식(예: bmp)을 선택합니다.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     이미지 자리 표시자가 보고서 디자인 화면에 나타납니다.  
  
## <a name="see-also"></a>관련 항목:  
 [이미지&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [보고서에 이미지 포함&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [외부 이미지 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [이미지 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
