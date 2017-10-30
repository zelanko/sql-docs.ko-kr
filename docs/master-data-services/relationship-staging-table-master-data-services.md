---
title: "관계 준비 테이블(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: a43b9a600e62b63468c21b9a32f1a706a7ec5eda
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="relationship-staging-table-master-data-services"></a>관계 준비 테이블(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 관계 준비 테이블(stg.name_Relationship)을 사용하여 멤버 사이의 관계를 기반으로 명시적 계층의 멤버 위치를 변경할 수 있습니다.  
  
##  <a name="TableColumns"></a> 테이블 열  
 다음 표에서는 간계 준비 테이블에 나오는 각 필드의 용도에 대해 설명합니다.  
  
|열 이름|Description|Value|  
|-----------------|-----------------|-----------|  
|**ID**|자동으로 할당된 식별자입니다.|이 필드에 값을 입력하지 마십시오. 일괄 처리를 처리하지 않은 경우 이 필드가 비어 있습니다.|  
|**RelationshipType**|필수임<br /><br /> 설정하려는 관계의 유형입니다.|가능한 값은<br /><br /> **1**: 부모<br /><br /> **2**: 형제(같은 수준)|  
|**ImportStatus_ID**|필수임<br /><br /> 가져오기 프로세스의 상태입니다.|가능한 값은<br /><br /> **0**- 레코드를 준비할 수 있음을 나타냅니다.<br /><br /> **1**- 자동으로 할당되며 레코드 준비 프로세스가 성공했음을 나타냅니다.<br /><br /> **2**- 자동으로 할당되며 레코드 준비 프로세스가 실패했음을 나타냅니다.|  
|**Batch_ID**|웹 서비스에만 필요<br /><br /> 준비할 레코드를 그룹화하는 자동 할당 식별자입니다.<br /><br /> 일괄 처리를 처리하지 않은 경우 이 필드가 비어 있습니다.|일괄 처리의 모든 멤버에는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ID **열의** 사용자 인터페이스에 표시되는 이 식별자가 할당됩니다.|  
|**BatchTag**|필수, 웹 서비스에서 사용하는 경우 제외<br /><br /> 일괄 처리의 고유 이름으로, 최대 50자입니다.||  
|**HierarchyName**|필수임<br /><br /> 명시적 계층의 이름입니다. 각 통합 멤버는 하나의 계층에만 속할 수 있습니다.||  
|**ParentCode**|필수임<br /><br /> 부모-자식 관계의 경우 자식 리프 또는 통합 멤버의 부모가 될 통합 멤버의 코드입니다.<br /><br /> 형제 관계의 경우 형제 중 하나의 코드입니다.||  
|**ChildCode**|필수임<br /><br /> 부모-자식 관계의 경우 자식이 될 통합 또는 리프 멤버의 코드입니다.<br /><br /> 형제 관계의 경우 형제 중 하나의 코드입니다.||  
|**정렬 순서**|선택 사항<br /><br /> 부모 아래에 있는 다른 멤버와 관련하여 해당 멤버의 순서를 나타내는 정수입니다. 각 자식 멤버마다 고유한 식별자를 지정해야 합니다.||  
|**ErrorCode**|오류 코드를 표시합니다. **ImportStatus_ID**가 **2**인 모든 레코드의 경우 [준비 프로세스 오류&#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)를 참조하세요.||  
  
## <a name="see-also"></a>관련 항목:  
 [개요: 테이블에서 데이터 가져오기&#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [준비 과정에서 발생하는 오류 보기&#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [준비 프로세스 오류&#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  

