---
title: 관계 준비 테이블(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3b5cc194306a4baecb2c5fa5478bf4733d1386af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67284980"
---
# <a name="relationship-staging-table-master-data-services"></a>관계 준비 테이블(Master Data Services)
  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 데이터베이스의 관계 준비 테이블(stg.name_Relationship)을 사용하여 멤버 사이의 관계를 기반으로 명시적 계층의 멤버 위치를 변경할 수 있습니다.  
  
##  <a name="TableColumns"></a>테이블 열  
 다음 표에서는 간계 준비 테이블에 나오는 각 필드의 용도에 대해 설명합니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**ID**|자동으로 할당된 식별자입니다. 이 필드에 값을 입력하지 마십시오. 일괄 처리를 처리하지 않은 경우 이 필드가 비어 있습니다.|  
|**RelationshipType**<br /><br /> 필수|설정하려는 관계의 유형입니다. 가능한 값은 다음과 같습니다.<br /><br /> **1**:P arent<br /><br /> **2**: 형제 (같은 수준)|  
|**ImportStatus_ID**<br /><br /> 필수|가져오기 프로세스의 상태입니다. 가능한 값은 다음과 같습니다.<br /><br /> **0**-레코드를 준비할 준비가 되었음을 나타내기 위해 지정 합니다.<br /><br /> **1**-자동으로 할당 되며 레코드의 준비 프로세스가 성공 했음을 나타냅니다.<br /><br /> **2**-자동으로 할당 되며 레코드 준비 프로세스가 실패 했음을 나타냅니다.|  
|**Batch_ID**<br /><br /> 웹 서비스에만 필요|준비할 레코드를 그룹화하는 자동 할당 식별자입니다. 일괄 처리의 모든 멤버에는 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ID **열의** 사용자 인터페이스에 표시되는 이 식별자가 할당됩니다.<br /><br /> 일괄 처리를 처리하지 않은 경우 이 필드가 비어 있습니다.|  
|**BatchTag**<br /><br /> 필수, 웹 서비스에서 사용하는 경우 제외|일괄 처리의 고유 이름으로, 최대 50자입니다.|  
|**HierarchyName**<br /><br /> 필수|명시적 계층의 이름입니다. 각 통합 멤버는 하나의 계층에만 속할 수 있습니다.|  
|**ParentCode**<br /><br /> 필수|부모-자식 관계의 경우 자식 리프 또는 통합 멤버의 부모가 될 통합 멤버의 코드입니다.<br /><br /> 형제 관계의 경우 형제 중 하나의 코드입니다.|  
|**ChildCode**<br /><br /> 필수|부모-자식 관계의 경우 자식이 될 통합 또는 리프 멤버의 코드입니다.<br /><br /> 형제 관계의 경우 형제 중 하나의 코드입니다.|  
|**정렬 순서**<br /><br /> 옵션|부모 아래에 있는 다른 멤버와 관련하여 해당 멤버의 순서를 나타내는 정수입니다. 각 자식 멤버마다 고유한 식별자를 지정해야 합니다.|  
|**ErrorCode**|오류 코드를 표시합니다. 
  **ImportStatus_ID**가 **2**인 모든 레코드의 경우 [준비 프로세스 오류&#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)를 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [MDS(Master Data Services) &#40;준비 프로세스를 사용 하 여 명시적 계층 멤버를 이동&#41;](add-update-and-delete-data-master-data-services.md)   
 [데이터 가져오기 &#40;MDS(Master Data Services)&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [준비 프로세스 중에 발생 하는 오류를 보려면 MDS(Master Data Services) &#40;&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [준비 프로세스 오류 &#40;MDS(Master Data Services)&#41;](staging-process-errors-master-data-services.md)  
  
  
