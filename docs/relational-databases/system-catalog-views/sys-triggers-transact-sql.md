---
title: sys.triggers (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- triggers
- triggers_TSQL
- sys.triggers
- sys.triggers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.triggers catalog view
ms.assetid: cefa4fc4-b8b9-4cd7-b124-eed5283acbfc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab5788614af71fe9fa4cab1a4f22e81d5a19a6d8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="systriggers-transact-sql"></a>sys.triggers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  트리거인 각 개체에 대해 TR 또는 TA 유형으로 한 행을 포함합니다. DML 트리거 이름은 스키마 범위 설정 되며, 따라서 볼 수에 **sys.objects**합니다. DDL 트리거 이름은 부모 엔터티에 의해 범위가 결정되며 이 뷰에서만 볼 수 있습니다.  
  
 **parent_class** 및 **이름** 열은 데이터베이스에서 트리거를 고유 하 게 식별 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|트리거 이름입니다. DML 트리거 이름은 스키마 범위입니다. DDL 트리거 이름은 부모 엔터티에 따라 범위가 결정됩니다.|  
|**object_id**|**int**|개체 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**parent_class**|**tinyint**|트리거 부모의 클래스입니다.<br /><br /> 0 = DDL 트리거의 데이터베이스<br /><br /> 1 = DML 트리거의 개체 또는 열|  
|**parent_class_desc**|**nvarchar (60)**|트리거 부모 클래스에 대한 설명입니다.<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|트리거 부모의 ID로 다음과 같습니다.<br /><br /> 0 = 데이터베이스가 부모인 트리거<br /><br /> 이것이 DML 트리거는 **object_id** 된 테이블의 DML 트리거가 정의 된 보기입니다.|  
|**유형**|**char(2)**|개체 유형:<br /><br /> TA = 어셈블리(CLR) 트리거<br /><br /> TR = SQL 트리거|  
|**type_desc**|**nvarchar (60)**|개체 유형에 대한 설명입니다.<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|트리거를 만든 날짜입니다.|  
|**modify_date**|**datetime**|ALTER 문을 사용하여 개체를 마지막으로 수정한 날짜입니다.|  
|**is_ms_shipped**|**bit**|내부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에서 사용자 대신 만든 트리거입니다.|  
|**is_disabled**|**bit**|트리거가 해제됩니다.|  
|**is_not_for_replication**|**bit**|트리거가 NOT FOR REPLICATION로 만들어졌습니다.|  
|**is_instead_of_trigger**|**bit**|1 = INSTEAD OF 트리거<br /><br /> 0 = AFTER 트리거|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
