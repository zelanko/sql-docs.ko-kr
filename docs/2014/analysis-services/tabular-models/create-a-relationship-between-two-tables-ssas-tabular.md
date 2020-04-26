---
title: 두 테이블 간에 관계 만들기 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.managereldb.f1
- sql12.asvs.bidtoolset.createrelatdb.f1
ms.assetid: 052d77b7-7922-408a-a200-786016ee4d15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98bd7f6c904207aa6d38f2ae756a207f128707a4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067535"
---
# <a name="create-a-relationship-between-two-tables-ssas-tabular"></a>두 테이블 간에 관계 만들기(SSAS 테이블 형식)
  데이터 원본의 테이블에 기존 관계가 없거나 새 테이블을 추가하는 경우 모델 디자이너의 도구를 사용하여 새 관계를 만들 수 있습니다. 테이블 형식 모델에서 관계를 사용하는 방법에 대한 자세한 내용은 [관계&#40;SSAS 테이블 형식&#41;](relationships-ssas-tabular.md)를 참조하세요.  
  
## <a name="create-a-relationship-between-two-tables"></a>두 테이블 간에 관계 만들기  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-click-and-drag"></a>다이어그램 뷰에서 두 테이블 간의 관계를 만들려면(클릭하여 끌기)  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭하고 **모델 뷰**를 클릭한 다음 **다이어그램 뷰**를 클릭합니다.  
  
2.  테이블 내의 열을 클릭한 채로 커서를 관련 조회 테이블의 관련 조회 열로 끌어다 놓으면 관계가 올바른 순서로 자동으로 만들어집니다.  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-right-click"></a>다이어그램 뷰에서 두 테이블 간의 관계를 만들려면(마우스 오른쪽 단추 클릭)  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭하고 **모델 뷰**를 클릭한 다음 **다이어그램 뷰**를 클릭합니다.  
  
2.  테이블 머리글 또는 열을 마우스 오른쪽 단추로 클릭하고 **관계 만들기**를 클릭합니다.  
  
3.  **관계 만들기** 대화 상자의 **테이블**에서 아래쪽 화살표를 클릭하고 드롭다운 목록에서 테이블을 선택합니다.  
  
     "일 대 다" 관계에서 이 테이블은 "다" 쪽에 있어야 합니다.  
  
4.  **열**에서 **관련 조회 열**과 관련된 데이터가 들어 있는 열을 선택합니다. 관계를 만들기 위해 열을 마우스 오른쪽 단추로 클릭하면 열이 자동으로 선택됩니다.  
  
5.  **테이블**에서 방금 선택한 테이블과 관련된 데이터 열이 하나 이상 있는 테이블을 **관련 조회 테이블**에서 선택합니다.  
  
     "일 대 다" 관계에서 이 테이블은 "일" 쪽에 있어야 하므로 선택한 열에 중복 값이 포함되지 않습니다. 잘못된 순서(다 대 일 대신 일 대 다)로 관계를 만들려고 하면 **관련 조회 열** 필드 옆에 아이콘이 나타납니다. 순서를 반대로 하여 유효한 관계를 만듭니다.  
  
6.  **열**에서 선택한 열의 값과 일치하는 고유 값이 있는 열을 **관련 조회 열**에서 선택합니다.  
  
7.  **만들기**를 클릭합니다.  
  
#### <a name="to-create-a-relationship-between-two-tables-in-data-view"></a>데이터 뷰에서 두 테이블 간의 관계를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **테이블** 메뉴를 클릭한 다음 **관계 만들기**를 클릭합니다.  
  
2.  **관계 만들기** 대화 상자의 **테이블**에서 아래쪽 화살표를 클릭하고 드롭다운 목록에서 테이블을 선택합니다.  
  
     "일 대 다" 관계에서 이 테이블은 "다" 쪽에 있어야 합니다.  
  
3.  **열**에서 **관련 조회 열**과 관련된 데이터가 들어 있는 열을 선택합니다.  
  
4.  **테이블**에서 방금 선택한 테이블과 관련된 데이터 열이 하나 이상 있는 테이블을 **관련 조회 테이블**에서 선택합니다.  
  
     "일 대 다" 관계에서 이 테이블은 "일" 쪽에 있어야 하므로 선택한 열에 중복 값이 포함되지 않습니다. 잘못된 순서(다 대 일 대신 일 대 다)로 관계를 만들려고 하면 **관련 조회 열** 필드 옆에 아이콘이 나타납니다. 순서를 반대로 하여 유효한 관계를 만듭니다.  
  
5.  **열**에서 선택한 열의 값과 일치하는 고유 값이 있는 열을 **관련 조회 열**에서 선택합니다.  
  
6.  **만들기**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSAS 테이블 형식&#41;&#40;관계 삭제](delete-relationships-ssas-tabular.md)   
 [관계&#40;SSAS 테이블 형식&#41;](relationships-ssas-tabular.md)  
  
  
