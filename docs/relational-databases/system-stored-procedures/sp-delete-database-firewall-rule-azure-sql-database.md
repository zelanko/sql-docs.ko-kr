---
title: sp_delete_database_firewall_rule (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_database_firewall_rule
- sp_delete_database_firewall_rule_TSQL
- sys.sp_delete_database_firewall_rule
- sys.sp_delete_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_database_firewall_rule procedure
ms.assetid: ed295312-e586-4fc2-9e80-806b490ee7bd
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d5f16e1a1b3b3fdfd0a12083ea8e86e034f50330
ms.sourcegitcommit: acb5de9f493238180d13baa302552fdcc30d83c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59542113"
---
# <a name="spdeletedatabasefirewallrule-azure-sql-database"></a>sp_delete_database_firewall_rule(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  데이터베이스 수준 방화벽 설정을 제거 프로그램 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다. 데이터베이스 방화벽 규칙을 구성에 사용자 데이터베이스 및 master 데이터베이스에 대 한 삭제 하 고 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]입니다.   
  
 
## <a name="syntax"></a>구문  
  
```    
sp_delete_database_firewall_rule [@name =] [N]'name'
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 `[@name =] [N]'name'`  
 제거할 데이터베이스 수준 방화벽 설정의 이름입니다. *이름을* 됩니다 **nvarchar (128)** 이며 기본값은 없습니다. 유니코드 식별자 `N` 사항임 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]합니다. 
  
## <a name="permissions"></a>사용 권한  
 서버 수준 보안 주체 로그인만 프로 비전 프로세스 또는 관리자는 데이터베이스 수준 방화벽 규칙을 삭제할 수로 할당 된 Azure Active Directory 주체를 생성 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 데이터베이스 수준 이라는 방화벽 설정을 제거 `Example DB Setting 1`합니다.
  
```  
-- Remove database-level firewall setting  
EXECUTE sp_delete_database_firewall_rule N'Example DB Setting 1';  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [Azure SQL Database 방화벽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [방법: 방화벽 설정 구성 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  


