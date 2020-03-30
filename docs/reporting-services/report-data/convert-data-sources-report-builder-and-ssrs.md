---
title: 데이터 원본 변환(보고서 작성기) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 05aee467c3e69c115bedfa498a546a4e1664ba71
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081753"
---
# <a name="convert-data-sources-report-builder-and-ssrs"></a>데이터 원본 변환(보고서 작성기 및 SSRS)
  보고서 데이터 창의 각 데이터 원본은 보고서에 관련 및 포함되거나 공유됩니다. 보고서 작성기에서 공유 데이터 원본은 보고서 서버 또는 SharePoint 사이트의 게시된 공유 데이터 원본을 가리킵니다. 보고서 디자이너에서 공유 데이터 원본은 솔루션 탐색기의 **공유 데이터 원본** 폴더에 있는 공유 데이터 원본을 가리킵니다.  
  
 포함된 데이터 원본과 공유 데이터 원본의 차이점에 대한 자세한 내용은 [포함된 데이터 연결 및 공유 데이터 연결 또는 데이터 원본&#40;보고서 작성기 및 SSRS&#41;](https://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56)을 참조하세요.  
  
 공유 데이터 원본을 만드는 방법에 대한 자세한 내용은 [포함된 데이터 원본 또는 공유 데이터 원본 만들기&#40;SSRS&#41;](https://msdn.microsoft.com/library/b111a8d0-a60d-4c8b-b00a-51644b19c34b)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>보고서 디자이너  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>포함된 데이터 원본에서 공유 데이터 원본으로 변환  
  
-   보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음 **공유 데이터 원본으로 변환**을 클릭합니다.  
  
    > [!NOTE]  
    >  보고서 데이터 창이 표시되지 않는 경우 **보기** 메뉴에서 **보고서 데이터**를 클릭하세요. 해당 창이 부동 창으로 열리는 경우 도킹할 수 있습니다. 자세한 내용은 [보고서 디자이너에서 보고서 데이터 창 도킹&#40;SSRS&#41;](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md)을 참조하세요.  
  
     보고서 데이터 창에서 데이터 원본 아이콘이 공유 데이터 원본 아이콘으로 변경됩니다. 솔루션 탐색기의 **공유 데이터 원본** 폴더에 같은 이름의 공유 데이터 원본이 나타납니다.  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>공유 데이터 원본에서 포함된 데이터 원본으로 변환  
  
-   보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭하여 **데이터 원본 속성** 대화 상자를 열고 **포함된 연결**을 클릭합니다. 필요한 정보를 입력합니다.  
  
     보고서 데이터 창에서 데이터 원본 아이콘이 공유 데이터 원본 아이콘으로 변경됩니다.  
  
## <a name="report-builder"></a>보고서 작성기  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>포함된 데이터 원본에서 공유 데이터 원본으로 변환  
  
-   보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭하여 **데이터 원본 속성** 대화 상자를 열고 **포함된 연결**을 클릭합니다. 필요한 정보를 입력합니다.  
  
     보고서 데이터 창에서 데이터 원본 아이콘이 공유 데이터 원본 아이콘으로 변경됩니다.  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>공유 데이터 원본에서 포함된 데이터 원본으로 변환  
  
-   보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭하여 **데이터 원본 속성** 대화 상자를 열고 **포함된 연결**을 클릭합니다. 필요한 정보를 입력합니다.  
  
     보고서 데이터 창에서 데이터 원본 아이콘이 공유 데이터 원본 아이콘으로 변경됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 데이터 원본 관리](../../reporting-services/report-data/manage-report-data-sources.md)   
 [데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
