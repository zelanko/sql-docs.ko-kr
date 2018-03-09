---
title: "sp_delete_firewall_rule (Azure SQL 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2016
ms.prod: 
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_delete_firewall_rule_TSQL
- sp_delete_firewall_rule
- sys.sp_delete_firewall_rule
- sys.sp_delete_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_firewall_rule procedure
ms.assetid: cf93eed1-ba97-4850-9fcc-b9c5a9317908
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa2815c27668bc680ce5da72b6713e29b517f43b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spdeletefirewallrule-azure-sql-database"></a>sp_delete_firewall_rule(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에서 서버 수준 방화벽 설정을 제거합니다. 이 저장 프로시저는 master 데이터베이스에서 서버 수준 보안 주체 로그인에 대해서만 사용할 수 있습니다.  

  
## <a name="syntax"></a>구문  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>인수  
 저장 프로시저의 인수는 다음과 같습니다.  
  
 [@name =] '*이름*'  
 제거된 서버 수준 방화벽 설정의 이름입니다. *이름* 은 **nvarchar (128)** 이며 기본값은 없습니다.  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 한 연결을 인증 하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시 됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 데이터베이스에 최신 버전의 로그인 테이블에 있는지 확인 하려면 실행할 [DBCC FLUSHAUTHCACHE &#40; Transact SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 프로비전 프로세스로 만들어진 서버 수준의 보안 주체 로그인만 서버 수준 방화벽 규칙을 삭제할 수 있습니다. 사용자는 sp_delete_firewall_rule를 실행 하려면 master 데이터베이스에 연결 되어야 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 'Example setting 1'이라는 서버 수준 방화벽 설정을 제거합니다. 가상 master 데이터베이스에는 문을 실행 합니다.  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>관련 항목:  
 [Azure SQL 데이터베이스 방화벽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [방법: 방화벽 설정 구성 (Azure SQL 데이터베이스)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule&#40; Azure SQL 데이터베이스 &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys.firewall_rules &#40; Azure SQL 데이터베이스 &#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
  


