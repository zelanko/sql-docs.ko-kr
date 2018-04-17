---
title: syscollector_collection_items (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6ffeae6501c29ffff1bacba96a959189859234e7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="syscollectorcollectionitems-transact-sql"></a>syscollector_collection_items(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  컬렉션 집합의 항목에 대한 정보를 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|컬렉션 집합을 식별합니다. Null을 허용하지 않습니다.|  
|**collection_item_id**|**int**|컬렉션 집합의 항목을 식별합니다. Null을 허용하지 않습니다.|  
|**collector_type_uid**|**uniqueidentifier**|수집기 유형을 식별하는 데 사용되는 GUID입니다. Null을 허용하지 않습니다.|  
|**name**|**nvarchar(4000)**|컬렉션 집합의 이름입니다. Null을 허용합니다.|  
|**frequency**|**int**|컬렉션 항목이 데이터를 수집하는 빈도입니다. Null을 허용하지 않습니다.|  
|**parameters**|**xml**|컬렉션 항목과 연결된 수집기 유형에 대한 매개 변수화를 설명합니다. 이 컬렉션 항목에 대 한 XML 스키마와는 XSD (XML 스키마)에 저장 된 유효성이 검사 되는 **parameter_schema** 특정 수집기 형식에 대 한 합니다. Null을 허용합니다. 자세한 내용은 참조 [syscollector_collector_types &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)합니다.|  
  
## <a name="permissions"></a>Permissions  
 에 대 한 SELECT가 필요 **dc_operator**, **dc_proxy**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 수집기 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
