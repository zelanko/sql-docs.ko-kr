---
description: sys.foreign_keys(Transact-SQL)
title: sys. foreign_keys (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33cf09cdbac74ea78fc642de8f1d557f39b84938
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539688"
---
# <a name="sysforeign_keys-transact-sql"></a>sys.foreign_keys(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  개체 당 행을 포함 합니다. 여기서는 외래 키 제약 조건입니다. 여기에는 **sys. type** = F입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.|  
|**referenced_object_id**|**int**|참조된 개체의 ID입니다.|  
|**key_index_id**|**int**|참조된 개체 내의 키 인덱스 ID입니다.|  
|**is_disabled**|**bit**|FOREIGN KEY 제약 조건이 비활성화되어 있습니다.|  
|**is_not_for_replication**|**bit**|NOT FOR REPLICATION 옵션을 사용하여 FOREIGN KEY 제약 조건을 만들었습니다.|  
|**is_not_trusted**|**bit**|시스템에서 FOREIGN KEY 제약 조건이 확인되지 않았습니다.|  
|**delete_referential_action**|**tinyint**|삭제가 발생할 때 이 FOREIGN KEY에 대해 선언된 참조 동작입니다.<br /><br /> 0 = 동작 없음<br /><br /> 1 = 연계 작업<br /><br /> 2 = Null 설정<br /><br /> 3 = 기본값 설정|  
|**delete_referential_action_desc**|**nvarchar(60)**|삭제가 발생할 때 이 FOREIGN KEY에 대해 선언된 참조 동작의 설명입니다.<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**update_referential_action**|**tinyint**|업데이트가 발생할 때 이 FOREIGN KEY에 대해 선언된 참조 동작입니다.<br /><br /> 0 = 동작 없음<br /><br /> 1 = 연계 작업<br /><br /> 2 = Null 설정<br /><br /> 3 = 기본값 설정|  
|**update_referential_action_desc**|**nvarchar(60)**|업데이트가 발생할 때 이 FOREIGN KEY에 대해 선언된 참조 동작의 설명입니다.<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**is_system_named**|**bit**|1 = 시스템에서 생성된 이름입니다.<br /><br /> 0 = 사용자가 제공한 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
