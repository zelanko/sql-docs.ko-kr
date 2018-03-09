---
title: sys.foreign_keys (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- foreign_keys
- sys.foreign_keys
- sys.foreign_keys_TSQL
- foreign_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.foreign_keys catalog view
ms.assetid: e960df1a-13fc-43ee-ba91-34c1b719ac2c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f2051dc726a4622f5340dc0972cf6fc38798d3f9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysforeignkeys-transact-sql"></a>sys.foreign_keys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  개체와 FOREIGN KEY 제약 된 당 한 행을 포함 **sys.object.type** = 6.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Sys.objects에서 상속 된 열 >**||이 뷰가 상속 하는 열 목록은 참조 [sys.objects& #40; Transact SQL & #41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**referenced_object_id**|**int**|참조된 개체의 ID입니다.|  
|**key_index_id**|**int**|참조된 개체 내의 키 인덱스 ID입니다.|  
|**is_disabled**|**bit**|FOREIGN KEY 제약 조건이 비활성화되어 있습니다.|  
|**is_not_for_replication**|**bit**|NOT FOR REPLICATION 옵션을 사용하여 FOREIGN KEY 제약 조건을 만들었습니다.|  
|**is_not_trusted**|**bit**|시스템에서 FOREIGN KEY 제약 조건이 확인되지 않았습니다.|  
|**delete_referential_action**|**tinyint**|삭제가 발생할 때 이 FOREIGN KEY에 대해 선언된 참조 동작입니다.<br /><br /> 0 = 동작 없음<br /><br /> 1 = 연계 작업<br /><br /> 2 = Null 설정<br /><br /> 3 = 기본값 설정|  
|**delete_referential_action_desc**|**nvarchar (60)**|삭제가 발생할 때 이 FOREIGN KEY에 대해 선언된 참조 동작의 설명입니다.<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**update_referential_action**|**tinyint**|업데이트가 발생할 때 이 FOREIGN KEY에 대해 선언된 참조 동작입니다.<br /><br /> 0 = 동작 없음<br /><br /> 1 = 연계 작업<br /><br /> 2 = Null 설정<br /><br /> 3 = 기본값 설정|  
|**update_referential_action_desc**|**nvarchar (60)**|업데이트가 발생할 때 이 FOREIGN KEY에 대해 선언된 참조 동작의 설명입니다.<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**is_system_named**|**bit**|1 = 시스템에서 생성된 이름입니다.<br /><br /> 0 = 사용자가 제공한 이름입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 & #40; Transact SQL & #41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
