---
title: sys.remote_logins (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.remote_logins_TSQL
- remote_logins
- remote_logins_TSQL
- sys.remote_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_logins catalog view
ms.assetid: 38477e91-d084-4df7-b1de-b930c5580189
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: df40db329851fbe931cb96f5b1aac99905d705c4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysremotelogins-transact-sql"></a>sys.remote_logins(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  원격 로그인 매핑당 한 개의 행을 반환합니다. 이 카탈로그 뷰는 해당 서버에서 들어오는 로컬 로그인을 실제 로컬 로그인으로 매핑하는 데 사용됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|서버 ID **sys.servers**합니다. 이 이름은 "원격" 서버의 연결에 의해 제공됩니다.|  
|**remote_name**|**sysname**|연결이 제공하는 매핑할 로그인 이름입니다. NULL인 경우에는 연결에서 지정된 로그인 이름이 사용됩니다.|  
|**local_principal_id**|**int**|로그인이 매핑될 서버 보안 주체의 ID입니다. 0인 경우에는 원격 로그인이 같은 이름을 가진 로그인에 매핑됩니다.|  
|**modify_date**|**datetime**|연결된 로그인을 마지막으로 변경한 날짜입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [연결 된 서버 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
