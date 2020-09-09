---
description: sys.key_constraints(Transact-SQL)
title: sys. key_constraints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.key_constraints
- key_constraints
- sys.key_constraints_TSQL
- key_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.key_constraints catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aa0fb4f82d6fea77efcf3d47efa9c97f37ad738b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548778"
---
# <a name="syskey_constraints-transact-sql"></a>sys.key_constraints(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  PRIMARY KEY 또는 UNIQUE 제약 조건인 각 개체당 한 개의 행을 포함합니다. **Sys. 개체를 포함 합니다.** PK 및 uq를 입력 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.|  
|**unique_index_id**|**int**|이 제약 조건을 강제 적용하기 위해 생성된 부모 개체에 있는 고유 인덱스의 ID입니다.|  
|**is_system_named**|**bit**|1 = 시스템에서 이름을 생성했습니다.<br /><br /> 0 = 사용자가 제공한 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
