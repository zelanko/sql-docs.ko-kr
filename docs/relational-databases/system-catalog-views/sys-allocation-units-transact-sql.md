---
title: sys.allocation_units (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.allocation_units_TSQL
- sys.allocation_units
- allocation_units_TSQL
- allocation_units
dev_langs:
- TSQL
helpviewer_keywords:
- sys.allocation_units catalog view
ms.assetid: ec9de780-68fd-4551-b70b-2d3ab3709b3e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 73ee5d7ac8bd512b69cc187f9860b9e7f2c38a78
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001293"
---
# <a name="sysallocation_units-transact-sql"></a>sys.allocation_units(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스의 각 할당 단위에 대해 한 행씩 있습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|allocation_unit_id|**bigint**|할당 단위의 ID입니다. 데이터베이스 내에서 고유합니다.|  
|type|**tinyint**|할당 단위 형식입니다.<br /><br /> 0 = 삭제됨<br /><br /> 1 = 행 내부 데이터(LOB 데이터 형식을 제외한 모든 데이터 형식)<br /><br /> 2 = LOB (large object) 데이터 (**텍스트**, **ntext**, **이미지**하십시오 **xml**, 큰 값 형식 및 CLR 사용자 정의 형식)<br /><br /> 3 = 행 오버플로 데이터|  
|type_desc|**nvarchar(60)**|할당 단위 유형에 대한 설명입니다.<br /><br /> **삭제**<br /><br /> **IN_ROW_DATA**<br /><br /> **LOB_DATA**<br /><br /> **ROW_OVERFLOW_DATA**|  
|container_id|**bigint**|할당 단위와 연결된 스토리지 컨테이너의 ID입니다.<br /><br /> type이 1 또는 3이면 container_id는 sys.partitions.hobt_id입니다.<br /><br /> type이 2이면 container_id = sys.partitions.partition_id입니다.<br /><br /> 0 = 삭제가 지연된 것으로 표시된 할당 단위|  
|data_space_id|**int**|이 할당 단위가 있는 파일 그룹의 ID입니다.|  
|total_pages|**bigint**|이 할당 단위가 할당하거나 예약한 총 페이지 수입니다.|  
|used_pages|**bigint**|실제로 사용 중인 총 페이지 수입니다.|  
|data_pages|**bigint**|다음을 포함하는 사용된 페이지 수입니다.<br /><br /> 행 내부 데이터<br /><br /> LOB 데이터<br /><br /> 행 오버플로 데이터<br /><br /> <br /><br /> 값이 반환 하는 내부 인덱스 페이지 및 할당 관리 페이지가 제외 됩니다.|  
  
> [!NOTE]  
>  대형 인덱스를 삭제하거나 다시 작성할 때 또는 대형 테이블을 삭제하거나 자를 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 트랜잭션이 커밋될 때까지 실제 페이지 할당 해제 및 관련 잠금을 연기합니다. 삭제 작업이 지연되어도 할당된 공간이 즉시 해제되지는 않습니다. 따라서 큰 개체를 삭제하거나 자를 때마다 sys.allocation_units에서 반환하는 값은 사용 가능한 실제 디스크 공간을 반영하지 않을 수도 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
