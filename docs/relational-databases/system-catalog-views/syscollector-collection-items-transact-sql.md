---
title: syscollector_collection_items (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f775d96b0bc56217f1400021e6c51b62d2886e5f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899950"
---
# <a name="syscollector_collection_items-transact-sql"></a>syscollector_collection_items(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  컬렉션 집합의 항목에 대한 정보를 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|컬렉션 집합을 식별합니다. Null을 허용하지 않습니다.|  
|**collection_item_id**|**int**|컬렉션 집합의 항목을 식별합니다. Null을 허용하지 않습니다.|  
|**collector_type_uid**|**uniqueidentifier**|수집기 유형을 식별하는 데 사용되는 GUID입니다. Null을 허용하지 않습니다.|  
|**name**|**nvarchar(4000)**|컬렉션 집합의 이름입니다. Null을 허용합니다.|  
|**주기와**|**int**|컬렉션 항목이 데이터를 수집하는 빈도입니다. Null을 허용하지 않습니다.|  
|**parameters**|**xml**|컬렉션 항목과 연결된 수집기 유형에 대한 매개 변수화를 설명합니다. 특정 수집기 유형에 대 한 **parameter_schema** 에 저장 된 XSD (xml 스키마)를 사용 하 여이 컬렉션 항목에 대 한 xml 스키마의 유효성을 검사 합니다. Null을 허용합니다. 자세한 내용은 [syscollector_collector_types &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)를 참조 하세요.|  
  
## <a name="permissions"></a>사용 권한  
 **Dc_operator**, **dc_proxy**에 대 한 SELECT가 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;데이터 수집기 저장 프로시저](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;데이터 수집기 뷰](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)  
  
  
