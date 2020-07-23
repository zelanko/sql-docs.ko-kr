---
title: sys. edge_constraints (Transact-sql) | Microsoft Docs
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
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b05b73b3de7cc9707a89830d56bb54f1dc33c6f
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919736"
---
# <a name="sysedge_constraints-transact-sql"></a>sys. edge_constraints (Transact-sql)
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

에 지 제약 조건에 해당 하는 각 개체에 대해 하나의 행을 포함 합니다. 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.|  
|**is_disabled**|**bit**|1 = 가장자리 제약 조건이 disbled입니다.<br /><br /> 0 = 가장자리 제약 조건을 사용 합니다.|  
|**is_not_trusted**|**bit**|1 = 시스템에서 가장자리 제약 조건을 확인 하지 않았습니다.<br /><br /> 0 = 시스템에서에 지 제약 조건을 확인 했습니다.|  
|**delete_referential_action**|**tinyint**|이에 지 제약 조건에 정의 된 참조 동작입니다.<br /><br />0 = 작업 없음|  
|**delete_referential_action_desc**|**nvarchar(60)**|이에 지 제약 조건에 정의 된 참조 동작에 대 한 설명입니다.<br /><br />NO_ACTION|  
|**is_system_named**|**bit**|1 = 시스템에서 가장자리 제약 조건 이름을 생성 했습니다.<br /><br />0 = 사용자가 가장자리 제약 조건 이름을 제공 했습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
