---
title: "테이블 형식 모델 파티션 (SSAS 테이블 형식) 만들기 및 관리 | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09a6acec0d1ee91c553d748a334733faff36bc08
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-manage-tabular-model-partitions"></a>테이블 형식 모델 파티션 만들기 및 관리

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  파티션은 테이블을 논리적 부분으로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리(새로 고침)할 수 있습니다. 모델 제작 중에 모델에 대해 정의한 파티션은 배포된 모델에서 복제됩니다. 배포된 후에는 **의** 파티션 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하거나 스크립트를 사용하여 해당 파티션을 관리할 수 있습니다. 이 항목에서 제공하는 태스크에서는 배포된 모델에 대해 파티션을 만들고 관리하는 방법을 설명합니다.  
  
  > [!NOTE]  
>  1400 호환성 수준에서 만든 테이블 형식 모델에서 파티션은 M 쿼리 문을 사용 하 여 정의 됩니다. 자세한 내용은 참고 [M 참조](https://msdn.microsoft.com/library/mt211003.aspx)합니다. 
>
  
## <a name="tasks"></a>태스크  
 배포된 테이블 형식 모델 데이터베이스에 대해 파티션을 만들고 관리하려면 **의** 파티션 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 사용합니다. **파티션** 대화 상자를 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 테이블을 마우스 오른쪽 단추로 클릭한 다음 **파티션**을 클릭합니다.  
  
###  <a name="bkmk_create_new"></a> 새 파티션을 만들려면  
  
1.  **파티션** 대화 상자에서 **새로 만들기** 단추를 클릭합니다.  
  
2.  **파티션 이름**에 파티션의 이름을 입력합니다. 기본적으로 기본 파티션의 이름은 새 파티션마다 증분 번호로 지정됩니다.  
  
3.  **쿼리문을**, 입력 또는 열과 쿼리 창에는 파티션에 포함 시킬 절을 정의 하는 SQL 또는 M 쿼리 문을 붙여 넣습니다.  
  
4.  문의 유효성을 검사하려면 **구문 검사**를 클릭합니다.  
  
###  <a name="bkmk_copy"></a> 파티션을 복사하려면  
  
1.  **파티션** 대화 상자의 **파티션** 목록에서 복사할 파티션을 선택한 다음 **복사** 단추를 클릭합니다.  
  
2.  **파티션 이름**에 파티션의 새 이름을 입력합니다.  
  
3.  **쿼리문을**, 쿼리 문을 편집 합니다.  
  
###  <a name="bkmk_merge"></a> 두 개 이상의 파티션을 병합하려면  
  
-   **파티션** 대화 상자의 **파티션** 목록에서 Ctrl+클릭을 사용하여 병합할 파티션을 선택한 다음 **병합** 단추를 클릭합니다.  
  
> [!IMPORTANT]  
>  파티션을 병합해도 파티션 메타데이터가 업데이트되지는 않습니다. 처리 작업으로 병합 된 파티션의 모든 데이터가 처리 되도록 결과 파티션에 대 한 SQL 또는 M 문을 편집 해야 합니다.  
  
###  <a name="bkmk_delete"></a> 파티션을 삭제하려면  
  
-   **파티션** 대화 상자의 **파티션** 목록에서 삭제할 파티션을 선택한 다음 **삭제** 단추를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 형식 모델 파티션](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [테이블 형식 모델 파티션 처리](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  

