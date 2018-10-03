---
title: sys.edge_constraints (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.edge_constraints
- edge_constraints
- SQL Graph
- edge_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.edge_constraints catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4068b127bdf4563e18cb459781f8a9a98ced6230
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785121"
---
# <a name="sysedgeconstraints-transact-sql"></a>sys.edge_constraints (Transact SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

각 개체는에 지 제약 조건에 대해 하나의 행을 포함 합니다. 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Sys.objects에서 상속 된 열 >**||이 뷰가 상속 하는 열 목록은 참조 하세요 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.|  
|**is_disabled**|**bit**|1 = edge 제약 조건을 사용할 수는 있습니다.<br /><br /> 0 = edge 제약 조건이 활성화 됩니다.|  
|**is_not_trusted**|**bit**|1 = edge 제약 조건 시스템에서 확인 되지 않았습니다.<br /><br /> 0 = edge 제약 조건 시스템에서 확인 되었습니다.|  
|**delete_referential_action**|**tinyint**|이 지 제약 조건에 정의 된 참조 동작입니다.<br /><br />0 = 작업이 없습니다.|  
|**delete_referential_action_desc**|**nvarchar(60)**|이 지 제약 조건에 정의 된 참조 동작의 설명입니다.<br /><br />NO_ACTION|  
|**is_system_named**|**bit**|1 = edge 시스템에서 생성 된 제약 조건 이름입니다.<br /><br />0 = edge 제약 조건 이름을 사용자가 제공 되었습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
