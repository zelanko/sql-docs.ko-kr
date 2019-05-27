---
title: 데이터베이스, 테이블 또는 파티션 처리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMS.PARTITIONS.PROCESSINGOPTIONS.IMBI.F1
ms.assetid: 307d69c3-cabb-4dfa-b90c-9852492c1213
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ea2d05c2862445737ea544fdab9c4ca8fc5e6c76
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66066852"
---
# <a name="process-database-table-or-partition"></a>데이터베이스, 테이블 또는 파티션 처리
  이 항목의 태스크를 사용 하 여 테이블 형식 모델 데이터베이스, 테이블 또는 파티션을 수동으로 처리 하는 방법에 설명 합니다 **프로세스 \<개체 >** 대화 상자 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
 테이블 형식 모델 처리에 대한 자세한 내용은 [데이터 처리&#40;SSAS 테이블 형식&#41;](../process-data-ssas-tabular.md)를 참조하세요.  
  
##  <a name="bkmk_process_tasks"></a> 작업  
  
###  <a name="bkmk_process_db"></a> 데이터베이스를 처리하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 처리할 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 처리**를 클릭합니다.  
  
2.  **데이터베이스 처리** 대화 상자의 **모드** 목록 상자에서 다음 처리 모드 중 하나를 선택합니다.  
  
    |모드|Description|  
    |----------|-----------------|  
    |**기본값 처리**|데이터베이스 개체의 처리 상태를 검색하고 필요한 처리를 수행하여 처리되지 않거나 부분적으로 처리된 개체를 완전히 처리된 상태로 전달합니다. 빈 테이블 및 파티션에 대한 데이터를 로드하고 계층, 계산 열 및 관계를 작성 또는 다시 작성(다시 계산)합니다.|  
    |**전체 처리**|데이터베이스 및 이 데이터베이스에 포함된 모든 개체를 처리합니다. 이미 처리된 개체에 대해 전체 처리를 실행하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 개체의 모든 데이터를 삭제한 다음 개체를 처리합니다. 개체에 구조적 변경이 발생한 경우 이러한 종류의 처리가 필요합니다. 이 옵션에 가장 많은 리소스가 필요합니다.|  
    |**지우기 처리**|데이터베이스 개체에서 모든 데이터를 제거합니다.|  
    |**다시 계산 처리**|계층, 관계 및 계산 열을 업데이트하고 다시 계산합니다.|  
  
3.  **처리** 확인란 열에서 선택된 모드로 처리할 파티션을 선택한 후 **확인**을 클릭합니다.  
  
###  <a name="bkmk_process_table"></a> 테이블을 처리하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 처리할 테이블이 포함된 테이블 형식 model 데이터베이스의 **테이블** 노드를 확장하고 처리할 테이블을 마우스 오른쪽 단추로 클릭한 다음 **테이블 처리**를 클릭합니다.  
  
2.  **테이블 처리** 대화 상자의 **모드** 목록 상자에서 다음 처리 모드 중 하나를 선택합니다.  
  
    |모드|Description|  
    |----------|-----------------|  
    |**기본값 처리**|테이블 개체의 처리 상태를 검색하고 필요한 처리를 수행하여 처리되지 않거나 부분적으로 처리된 개체를 완전히 처리된 상태로 전달합니다. 빈 테이블 및 파티션에 대한 데이터를 로드하고 계층, 계산 열 및 관계를 작성 또는 다시 작성(다시 계산)합니다.|  
    |**전체 처리**|테이블 개체와 여기에 포함된 모든 개체를 처리합니다. 이미 처리된 개체에 대해 전체 처리를 실행하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 개체의 모든 데이터를 삭제한 다음 개체를 처리합니다. 개체에 구조적 변경이 발생한 경우 이러한 종류의 처리가 필요합니다. 이 옵션에 가장 많은 리소스가 필요합니다.|  
    |**데이터 처리**|계층 또는 관계를 다시 작성하거나 계산 열 및 측정값을 다시 계산하지 않고 테이블에 데이터를 로드합니다.|  
    |**지우기 처리**|테이블과 테이블 파티션에서 모든 데이터를 제거합니다.|  
    |**조각 모음 처리**|보조 테이블 인덱스를 조각 모음합니다.|  
  
3.  테이블 확인란 열에서 테이블을 확인하고 처리할 테이블을 추가로 선택한 후(선택 사항) **확인**을 클릭합니다.  
  
###  <a name="bkmk_process_partition"></a> 하나 이상의 파티션을 처리하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 처리할 파티션이 있는 테이블을 마우스 오른쪽 단추로 클릭한 다음 **파티션**을 클릭합니다.  
  
2.  **파티션** 대화 상자의 **파티션**에서 처리 단추를 클릭합니다.  
  
3.  **파티션 처리** 대화 상자의 **모드** 목록 상자에서 다음 처리 모드 중 하나를 선택합니다.  
  
    |모드|Description|  
    |----------|-----------------|  
    |**기본값 처리**|파티션 개체의 처리 상태를 검색하고 필요한 처리를 수행하여 처리되지 않거나 부분적으로 처리된 파티션 개체를 완전히 처리된 상태로 전달합니다. 빈 테이블 및 파티션에 대한 데이터를 로드하고 계층, 계산 열 및 관계를 작성 또는 다시 작성(다시 계산)합니다.|  
    |**전체 처리**|파티션 개체와 여기에 포함된 모든 개체를 처리합니다. 이미 처리된 개체에 대해 전체 처리를 실행하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 개체의 모든 데이터를 삭제한 다음 개체를 처리합니다. 개체에 구조적 변경이 발생한 경우 이러한 종류의 처리가 필요합니다.|  
    |**데이터 처리**|계층 또는 관계를 다시 작성하거나 계산 열 및 측정값을 다시 계산하지 않고 파티션 또는 테이블에 데이터를 로드합니다.|  
    |**지우기 처리**|파티션에서 모든 데이터를 제거합니다.|  
    |**증분 처리**|새 데이터로 파티션을 증분 업데이트합니다.|  
  
4.  **처리** 확인란 열에서 선택된 모드로 처리할 파티션을 선택한 후 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 형식 모델 파티션&#40;SSAS 테이블 형식&#41;](tabular-model-partitions-ssas-tabular.md)   
 [테이블 형식 모델 파티션 만들기 및 관리&#40;SSAS 테이블 형식&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
