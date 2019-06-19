---
title: Specify an Image as a Pointer on 계기 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c7a57987a5d1cd0ac7984db3b716521d9c7a09af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101153"
---
# <a name="specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs"></a>이미지를 계기의 포인터로 지정(보고서 작성기 및 SSRS)
  계기에는 포인터의 모양을 사용자 지정하는 데 사용할 수 있는 세 가지 기본 제공 스타일이 들어 있습니다. 방사형 계기의 경우 기본 제공된 스타일은 다음과 같습니다. 니 들, 표식 및 막대를 선택 합니다. 선형 계기의 경우 기본 제공 스타일은 표식, 막대 및 온도계입니다. 고유한 포인터가 필요한 경우 모든 기능을 갖춘 포인터로 사용할 수 있는 이미지를 만들어 지정할 수 있습니다.  
  
 포인터의 이미지를 지정할 경우 이미지는 다음 사양을 충족해야 합니다.  
  
-   포인터의 원점 또는 회전의 중심은 이미지의 위쪽에 있어야 합니다.  
  
-   포인터의 끝은 아래쪽을 향하고 있어야 합니다.  
  
 포인터의 모양은 불규칙적이므로 이미지의 필요하지 않은 부분을 숨기려면 투명 색을 지정해야 합니다. 지정된 색은 계기에 나타나지 않으므로 계기에 일반적으로 표시되지 않는 색을 투명 색으로 사용하는 것이 좋습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-an-image-as-a-pointer-on-the-gauge"></a>이미지를 계기의 포인터로 지정하려면  
  
1.  디자인 뷰에서 계기의 포인터를 클릭합니다.  
  
2.  (선택 사항) 계기에 포인터가 없는 경우, 마우스 오른쪽 단추로 클릭 선택한 계기 **포인터 추가**합니다. 포인터가 계기에 추가됩니다.  
  
3.  클릭 합니다 **삽입** 리본의 탭 및 이미지 아이콘을 두 번 클릭 합니다. **이미지 속성** 대화 상자가 열립니다.  
  
4.  보고서에 이미지를 추가합니다. 자세한 내용은 [보고서에 이미지 포함 &#40;보고서 작성기 및 SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)합니다.  
  
5.  속성 창을 엽니다.  
  
6.  디자인 화면에서 포인터를 클릭합니다. 포인터의 속성이 속성 창에 표시됩니다.  
  
7.  PointerImage 노드를 확장 합니다.  
  
8.  **소스**를 선택 **Embedded** 드롭 다운 목록에서.  
  
    > [!NOTE]  
    >  이미지를 데이터베이스 또는 웹에 저장한 경우 이 속성에 적절한 옵션을 지정할 수 있습니다. 자세한 내용은 [이미지 속성 대화 상자, 일반 &#40;보고서 작성기 및 SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)합니다.  
  
9. **값**, 드롭 다운 목록에서 이미지의 이름을 선택 합니다.  
  
10. **TransparentColor**, 이미지에서 제거할 색 값을 선택 합니다. 이렇게 하면 계기에 포인터의 모양이 깔끔하게 만들어집니다.  
  
## <a name="see-also"></a>관련 항목  
 [계기의 포인터 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [보고서에 계기 추가 &#40;보고서 작성기 및 SSRS&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [선, 색 및 이미지 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [계기&#40;보고서 작성기 및 SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
