---
title: sp_delete_database_firewall_rule (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 4e10f1d1194b88e591eb85d6daacb478549674ee
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="spdeletedatabasefirewallrule-azure-sql-database"></a>sp_delete_database_firewall_rule(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  데이터베이스 수준 방화벽 설정을 제거 프로그램 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다. 데이터베이스 방화벽 규칙을 구성에서 모든 사용자 데이터베이스와 master 데이터베이스를 삭제 하 고 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]합니다.   
  
 
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_database_firewall_rule [@name =] [N]'name'
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@name =**] **'***이름***'**  
 제거할 데이터베이스 수준 방화벽 설정의 이름입니다. *이름* 은 **nvarchar (128)** 기본값은 없습니다. 유니코드 식별자 `N` 는 선택 사항에 대 한 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]합니다. 
  
## <a name="permissions"></a>Permissions  
 서버 수준 보안 주체 로그인만 프로 비전 프로세스 또는 관리자는 데이터베이스 수준 방화벽 규칙을 삭제할 수로 할당 된 Azure Active Directory 사용자가 만든 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 데이터베이스 수준 방화벽 설정에서 명명 된 제거 `Example DB Setting 1`합니다.
  
```  
-- Remove database-level firewall setting  
EXECUTE sp_delete_database_firewall_rule N'Example DB Setting 1';  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Azure SQL 데이터베이스 방화벽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [방법: 방화벽 설정 구성 (Azure SQL 데이터베이스)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_set_database_firewall_rule &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  


