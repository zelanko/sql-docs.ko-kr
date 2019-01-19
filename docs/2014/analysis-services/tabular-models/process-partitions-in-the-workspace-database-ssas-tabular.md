---
title: 작업 영역 데이터베이스 (SSAS 테이블 형식)에서 파티션을 처리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 3a369705-43fa-4961-9045-32e06fbdde33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af0534e049c5038676849f40178d865e9f15de61
ms.sourcegitcommit: 2e8783e6bedd9597207180941be978f65c2c2a2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2019
ms.locfileid: "54405893"
---
# <a name="process-partitions-in-the-workspace-database-ssas-tabular"></a>작업 영역 데이터베이스 (SSAS 테이블 형식)에서 파티션 처리
  파티션은 테이블을 논리적 부분으로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리(새로 고침)할 수 있습니다. 이 항목의 태스크에서는 **의** 파티션 처리 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]대화 상자를 사용하여 모델 작업 영역 데이터베이스에서 파티션을 처리하는 방법을 설명합니다.  
  
 다른 Analysis Services 인스턴스로 모델을 배포한 후 데이터베이스 관리자는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 스크립트 또는 IS 패키지를 사용하여 (배포된) 모델에서 파티션을 만들고 관리할 수 있습니다. 자세한 내용은 [테이블 형식 모델 파티션 만들기 및 관리&#40;SSAS 테이블 형식&#41;](partitions-ssas-tabular.md)를 참조하세요.  
  
###  <a name="bkmk_create_new"></a> 파티션을 처리하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **처리** (새로 고침) 및 **파티션 처리**를 차례로 클릭합니다.  
  
2.  **모드** 목록 상자에서 다음 처리 모드 중 하나를 선택합니다.  
  
    |모드|Description|  
    |----------|-----------------|  
    |**기본값 처리**|파티션 개체의 처리 상태를 검색하고 필요한 처리를 수행하여 처리되지 않거나 부분적으로 처리된 파티션 개체를 완전히 처리된 상태로 전달합니다. 빈 테이블 및 파티션에 대한 데이터를 로드하고 계층, 계산 열 및 관계를 작성 또는 다시 작성합니다.|  
    |**전체 처리**|파티션 개체와 여기에 포함된 모든 개체를 처리합니다. 이미 처리된 개체에 대해 전체 처리를 실행하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 개체의 모든 데이터를 삭제한 다음 개체를 처리합니다. 개체에 구조적 변경이 발생한 경우 이러한 종류의 처리가 필요합니다.|  
    |**데이터 처리**|계층 또는 관계를 다시 작성하거나 계산 열 및 측정값을 다시 계산하지 않고 파티션 또는 테이블에 데이터를 로드합니다.|  
    |**지우기 처리**|파티션에서 모든 데이터를 제거합니다.|  
    |**증분 처리**|새 데이터로 파티션을 증분 업데이트합니다.|  
  
3.  **처리** 확인란 열에서 선택된 모드로 처리할 파티션을 선택한 후 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [파티션&#40;SSAS 테이블 형식&#41;](partitions-ssas-tabular.md)   
 [작업 영역 데이터베이스에서 파티션 만들기 및 관리&#40;SSAS 테이블 형식&#41;](workspace-database-ssas-tabular.md)  
  
  
