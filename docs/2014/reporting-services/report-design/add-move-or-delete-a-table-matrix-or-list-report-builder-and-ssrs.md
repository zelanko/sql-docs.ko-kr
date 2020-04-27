---
title: 테이블, 행렬 또는 목록 추가, 이동 또는 삭제(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4b97c470-cde0-4bb1-a46e-5f5f5553feaa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b3e98a5c49877f6bc94e9e3ac1e880c90229cd3c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106596"
---
# <a name="add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs"></a>테이블, 행렬 또는 목록 추가, 이동 또는 삭제(보고서 작성기 및 SSRS)
  데이터 영역은 보고서 데이터 세트의 데이터를 표시합니다. 데이터 영역에는 테이블, 행렬, 목록, 차트 및 계기가 있습니다. 한 데이터 영역을 다른 데이터 영역 안에 중첩시키려면 각 데이터 영역을 개별적으로 추가한 다음 자식 데이터 영역을 부모 데이터 영역 안으로 끕니다.  
  
 보고서에 테이블 또는 행렬 데이터 영역을 추가하는 가장 간단한 방법은 새 테이블 또는 새 행렬 마법사를 실행하는 것입니다. 이러한 마법사는 데이터 원본 연결을 선택하고, 필드를 정렬하고, 레이아웃과 스타일을 선택하는 과정을 안내합니다.  
  
> [!NOTE]  
>  마법사는 보고서 작성기에서만 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-table-or-matrix-to-a-report-by-using-the-new-table-or-new-matrix-wizard"></a>새 테이블 또는 새 행렬 마법사를 사용하여 보고서에 테이블 또는 행렬을 추가하려면  
  
1.  **삽입** 탭에서 **테이블** 또는 **행렬**을 클릭한 다음 **테이블 마법사** 또는 **행렬 마법사**를 클릭합니다.  
  
2.  **NewTable** 또는 **새 행렬** 마법사의 단계를 따릅니다.  
  
3.  **홈** 탭에서 **실행** 을 클릭하여 렌더링된 보고서를 표시합니다.  
  
4.  **실행** 탭에서 **디자인** 을 클릭하여 보고서에 대한 작업을 진행합니다.  
  
### <a name="to-add-a-data-region"></a>데이터 영역을 추가하려면  
  
1.  **리본**의 **데이터 영역** 그룹에서 추가할 데이터 영역을 클릭합니다.  
  
2.  디자인 화면을 클릭한 다음 끌어 원하는 크기의 데이터 영역 상자를 만듭니다.  
  
3.  보고서 데이터 창에서 데이터 영역 셀로 보고서 데이터 세트 필드를 끕니다. 이제 데이터 영역이 보고서 데이터 세트의 데이터에 바인딩됩니다.  
  
### <a name="to-select-a-data-region"></a>데이터 영역을 선택하려면  
  
-   테이블릭스 데이터 영역의 경우 모퉁이 핸들을 마우스 오른쪽 단추로 클릭하고 차트 또는 계기 데이터 영역의 경우 데이터 영역을 클릭합니다.  
  
     선택 핸들 및 8개의 크기 조정 핸들이 나타납니다.  
  
     중첩된 데이터 영역의 경우 중첩된 데이터 영역을 마우스 오른쪽 단추로 클릭하고 **선택**을 클릭한 다음 원하는 보고서 항목을 선택합니다. 선택된 보고서 항목을 확인하려면 속성 창을 사용합니다. 디자인 화면에서 선택한 항목의 이름이 속성 창의 도구 모음에 나타납니다.  
  
### <a name="to-move-a-data-region"></a>데이터 영역을 이동하려면  
  
-   데이터 영역을 이동하려면 데이터 영역의 선택 핸들을 클릭하여 끕니다. 맞춤선을 사용하여 데이터 영역을 기존 보고서 항목에 맞춥니다.  
  
     눈금자가 표시되지 않으면 보기 탭을 클릭하고 **눈금자** 옵션을 선택합니다.  
  
     또는 화살표 키를 사용하여 디자인 화면에서 선택한 데이터 영역을 이동합니다.  
  
### <a name="to-delete-a-data-region"></a>데이터 영역을 삭제하려면  
  
-   데이터 영역을 선택하고 데이터 영역을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블릭스 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [테이블 &#40;보고서 작성기 및 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [행렬 &#40;보고서 작성기 및 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [&#40;보고서 작성기 및 SSRS를 나열&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
