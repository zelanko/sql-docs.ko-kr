---
title: sys.conversation_priorities (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- conversation_priorities_TSQL
- conversation_priorities
- sys.conversation_priorities_TSQL
- sys.conversation_priorities
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], priorities
- Service Broker, conversations
- sys.conversation_priorities catalog view
ms.assetid: 7cbb9171-3310-4aae-8458-755c882d6462
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73d823e5ad3efb2b91f4a0fd591d4e3fa54eefd5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysconversationpriorities-transact-sql"></a>sys.conversation_priorities(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  다음 표와 같이 현재 데이터베이스에 생성된 각 대화 우선 순위마다 한 행을 포함합니다. 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|Priority_id|**int**|대화 우선 순위를 고유하게 식별하는 숫자입니다. NULL을 허용하지 않습니다.|  
|name|**sysname**|대화 우선 순위의 이름입니다. NULL을 허용하지 않습니다.|  
|service_contract_id|**int**|대화 우선 순위에 지정된 계약의 식별자입니다. 이는 sys.service_contracts의 service_contract_id 열에서 조인할 수 있습니다. NULL을 허용합니다.|  
|local_service_id|**int**|대화 우선 순위의 로컬 서비스로 지정된 서비스의 식별자입니다. 이 열은 sys.services의 service_id 열에서 조인할 수 있습니다. NULL을 허용합니다.|  
|remote_service_name|**nvarchar(256)**|대화 우선 순위의 원격 서비스로 지정된 서비스의 이름입니다. NULL을 허용합니다.|  
|priority|**tinyint**|이 대화 우선 순위에 지정된 우선 순위 수준입니다. NULL을 허용하지 않습니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 계약과 로컬 서비스 이름을 보여 주는 조인을 사용하여 대화 우선 순위를 나열합니다.  
  
```  
SELECT scp.name AS priority_name,  
       ssc.name AS contract_name,  
       ssvc.name AS local_service_name,  
       scp.remote_service_name,  
       scp.priority AS priority_level  
FROM sys.conversation_priorities AS scp  
    INNER JOIN sys.service_contracts AS ssc  
       ON scp.service_contract_id = ssc.service_contract_id  
    INNER JOIN sys.services AS ssvc  
       ON scp.local_service_id = ssvc.service_id  
ORDER BY priority_name, contract_name,  
         local_service_name, remote_service_name;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [CREATE BROKER PRIORITY&#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys.services &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)   
 [sys.service_contracts &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-service-contracts-transact-sql.md)  
  
  
