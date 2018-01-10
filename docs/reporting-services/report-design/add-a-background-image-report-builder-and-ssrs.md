---
title: "배경 이미지 추가(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c777fefb-8695-44a7-b5cd-a18c587583f2
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 551533d6550ec0cb69e52e3cc34edeffca898567
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="add-a-background-image-report-builder-and-ssrs"></a>배경 이미지 추가(보고서 작성기 및 SSRS)
  사각형, 입력란, 목록, 행렬, 테이블 및 차트의 일부분과 같은 보고서 항목이나 페이지 머리글, 페이지 바닥글 또는 보고서 본문과 같은 보고서 섹션에 배경 이미지를 추가할 수 있습니다. 속성 창에 **BackgroundImage** 가 표시되는 보고서 디자인 화면의 모든 선택 항목에 대해 배경 이미지를 정의할 수 있습니다. 배경 이미지는 다른 이미지와 마찬가지로 보고서 서버의 이미지, 데이터 집합 필드의 이미지 또는 보고서 정의에 포함된 이미지에 대한 URL일 수 있습니다. 보고서에 포함된 이미지를 사용하려면 먼저 보고서 정의에 이미지를 추가해야만 디자인 화면에 이미지를 추가할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-the-report-definition"></a>보고서 정의에 이미지를 포함하려면  
  
1.  보고서 데이터 창에서 **이미지** 노드를 마우스 오른쪽 단추로 클릭한 다음 **이미지 추가**를 클릭합니다.  
  
    > [!NOTE]  
    >  보고서 데이터 창이 표시되지 않는 경우 **보기** 탭에서 **보고서 데이터**를 클릭합니다.  
  
2.  보고서 정의에 포함할 이미지를 탐색한 다음 **확인**을 클릭합니다.  
  
### <a name="to-add-a-background-image"></a>배경 이미지를 추가하려면  
  
1.  보고서 디자인 뷰에서 배경 이미지를 추가할 보고서 항목을 선택합니다.  
  
2.  속성 창이 표시되지 않으면 **보기** 탭에서 **속성**을 선택합니다.  
  
3.  속성 창에서 **BackgroundImage**를 확장하고 다음을 수행합니다.  
  
    -   포함 이미지의 경우  
  
         **Source** 를 **Embedded**로 설정합니다.  
  
         **값** 을 보고서에 포함된 이미지의 이름으로 설정합니다.  
  
    -   외부 이미지의 경우  
  
         **Source** 를 **External**로 설정합니다.  
  
         **값** 을 이미지에 대한 올바른 경로로 설정합니다. 이미지는 기본 모드나 SharePoint 통합 모드에 있는 보고서 서버 또는 다른 웹 사이트에 있을 수 있습니다. 자세한 내용은 [외부 이미지 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)를 참조하세요.  
  
    -   보고서 항목이 연결된 데이터베이스의 필드에 포함되어 있는 이미지의 경우  
  
         **Source** 를 **Database**로 설정합니다.  
  
         **값** 을 보고서 데이터 집합에 있는 필드의 이름으로 설정합니다. 자세한 내용은 [데이터 바인딩된 이미지 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-data-bound-image-report-builder-and-ssrs.md)를 참조하세요.  
  
         **MIMEType**또는 파일 형식에 대해 이미지에 해당하는 MIME 형식(예: .bmp)을 선택합니다.  
  
        > [!NOTE]  
        >  MIMEType은 **Source** 속성을 **Database**로 설정한 경우에만 적용됩니다. **원본** 속성을 **외부** 또는 **포함**으로 설정한 경우에는 **MIMEType** 값이 무시됩니다.  
  
    -   **BackgroundRepeat**에 대해 **Default**, **Repeat**, **RepeatX**, or **RepeatY**또는 **Clip**식을 선택합니다.  
  
         차트의 배경 이미지에 대해 **BackgroundRepeat** 를 **Default**, **Repeat**, **Fit**및 **Clip**으로 설정할 수 있지만 **RepeatX** 나 **RepeatY**로 설정할 수는 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [이미지&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [이미지 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
