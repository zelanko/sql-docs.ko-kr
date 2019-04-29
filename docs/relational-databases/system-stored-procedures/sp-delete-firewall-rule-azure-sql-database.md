---
title: sp_delete_firewall_rule (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.service: sql-database
ms.reviewer: ''
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 406f94ab0ab2d0ebaddf9635448e364bf90ceb8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032785"
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
  
 [@name =] '*name*'  
 제거된 서버 수준 방화벽 설정의 이름입니다. *이름을* 됩니다 **nvarchar (128)** 기본값은 없습니다.  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 강제 실행하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.  
  
## <a name="permissions"></a>사용 권한  
 프로비전 프로세스로 만들어진 서버 수준의 보안 주체 로그인만 서버 수준 방화벽 규칙을 삭제할 수 있습니다. 사용자는 sp_delete_firewall_rule를 실행 하려면 master 데이터베이스에 연결 되어야 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 'Example setting 1'이라는 서버 수준 방화벽 설정을 제거합니다. 가상 master 데이터베이스에서 문을 실행 합니다.  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>관련 항목  
 [Azure SQL Database 방화벽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [방법: 방화벽 설정 구성 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys.firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
  


