---
title: 테이블 형식 모델 파티션 (SSAS 테이블 형식)를 처리 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6c498d2b-22d6-4661-bc21-2ee708336c8b
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e3329eb6e7f003f3e43407aa6948b844c3bfda27
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185480"
---
# <a name="process-tabular-model-partitions-ssas-tabular"></a>테이블 형식 모델 파티션 처리(SSAS 테이블 형식)
  파티션은 테이블을 논리적 부분으로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리(새로 고침)할 수 있습니다. 이 항목의 태스크에서는 **의** 파티션 처리 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 사용하여 model 데이터베이스에서 파티션을 처리하는 방법을 설명합니다.  
  
###  <a name="bkmk_create_new"></a> 파티션을 처리하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 처리할 파티션이 있는 테이블을 마우스 오른쪽 단추로 클릭한 다음 **파티션**을 클릭합니다.  
  
2.  **파티션** 대화 상자의 **파티션**에서 처리 단추를 클릭합니다.  
  
3.  **파티션 처리** 대화 상자의 **모드** 목록 상자에서 다음 처리 모드 중 하나를 선택합니다.  
  
    |모드|Description|  
    |----------|-----------------|  
    |**기본값 처리**|파티션 개체의 처리 상태를 검색하고 필요한 처리를 수행하여 처리되지 않거나 부분적으로 처리된 파티션 개체를 완전히 처리된 상태로 전달합니다. 빈 테이블 및 파티션에 대한 데이터를 로드하고 계층, 계산 열 및 관계를 작성 또는 다시 작성합니다.|  
    |**전체 처리**|파티션 개체와 여기에 포함된 모든 개체를 처리합니다. 이미 처리된 개체에 대해 전체 처리를 실행하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 개체의 모든 데이터를 삭제한 다음 개체를 처리합니다. 개체에 구조적 변경이 발생한 경우 이러한 종류의 처리가 필요합니다.|  
    |**데이터 처리**|계층 또는 관계를 다시 작성하거나 계산 열 및 측정값을 다시 계산하지 않고 파티션 또는 테이블에 데이터를 로드합니다.|  
    |**지우기 처리**|파티션에서 모든 데이터를 제거합니다.|  
    |**증분 처리**|새 데이터로 파티션을 증분 업데이트합니다.|  
  
4.  **처리** 확인란 열에서 선택된 모드로 처리할 파티션을 선택한 후 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 형식 모델 파티션 &#40;SSAS 테이블 형식&#41;](partitions-ssas-tabular.md)   
 [테이블 형식 모델 파티션 만들기 및 관리 &#40;SSAS 테이블 형식&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  