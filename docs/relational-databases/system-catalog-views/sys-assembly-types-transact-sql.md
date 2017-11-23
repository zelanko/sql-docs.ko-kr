---
title: sys.assembly_types (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 211cb9f89fe2e84b6a8a21dd8268551df6a2e97c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysassemblytypes-transact-sql"></a>sys.assembly_types(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  CLR 어셈블리에 의해 정의되는 각 사용자 정의 형식당 한 개의 행을 포함합니다. 다음 **sys.assembly_types** 상속 된 열 목록에 나타납니다 (참조 [sys.types &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) 후 **rule_object_id**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|이 유형이 생성된 어셈블리의 ID입니다.|  
|**assembly_class**|**sysname**|이 유형을 정의하는 어셈블리 내의 클래스 이름입니다.|  
|**is_binary_ordered**|**bit**|이 유형의 바이트를 정렬하는 것은 비교 연산자를 사용해 유형을 정렬하는 것과 같습니다.|  
|**is_fixed_length**|**bit**|유형의 길이가 항상 max_length와 동일합니다.|  
|**prog_id**|**nvarchar (40)**|COM에 전달할 유형의 ProgID입니다.|  
|**assembly_qualified_name**|**nvarchar(4000)**|어셈블리가 명시된 정식 유형 이름입니다. 이 이름은 Type.GetType()에 전달하기에 알맞은 형식을 갖습니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [스칼라 유형 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
