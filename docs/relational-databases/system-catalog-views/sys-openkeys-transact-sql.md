---
title: (거래 SQL) sys.openkeys | Microsoft 문서
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- openkeys_TSQL
- sys.openkeys_TSQL
- openkeys
- sys.openkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.openkeys catalog view
ms.assetid: 719a1259-2398-4fcb-ba05-aeabba7aec21
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: ebc2e379d82c1b8a4e0406fd82900b7f21297123
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39543133"
---
# <a name="sysopenkeys-transact-sql"></a>sys.openkeys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  이 카탈로그 뷰는 현재 세션에서 열려 있는 암호화 키에 대한 정보를 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|키가 포함된 데이터베이스의 ID입니다.|  
|**database_name**|**sysname**|키가 포함된 데이터베이스의 이름입니다.|  
|**key_id**|**int**|키 ID입니다. 이 ID는 데이터베이스 내에서 고유합니다.|  
|**key_name**|**sysname**|키 이름입니다. 데이터베이스 내에서 고유합니다.|  
|**key_guid**|**varbinary**|키의 GUID입니다. 데이터베이스 내에서 고유합니다.|  
|**opened_date**|**datetime**|키가 열린 날짜와 시간입니다.|  
|**상태**|**int**|키가 메타데이터에서 유효한 경우 1을 반환합니다. 키가 메타데이터에 없으면 0을 반환합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [OPEN SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)  
  
  
