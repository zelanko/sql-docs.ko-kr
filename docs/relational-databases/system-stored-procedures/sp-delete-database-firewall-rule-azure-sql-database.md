---
description: sp_delete_database_firewall_rule(Azure SQL Database)
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
monikerRange: = azuresqldb-current
ms.openlocfilehash: ae71838bd9a384e616d0f1fe50d612535f840919
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472694"
---
# <a name="sp_delete_database_firewall_rule-azure-sql-database"></a>sp_delete_database_firewall_rule(Azure SQL Database)
[!INCLUDE[Azure SQL Database](../../includes/applies-to-version/asdb.md)]

  에서 데이터베이스 수준 방화벽 설정을 제거 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 합니다. 데이터베이스 방화벽 규칙은 master 데이터베이스 및의 사용자 데이터베이스에 대해 구성 및 삭제할 수 있습니다 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] .   
  
 
## <a name="syntax"></a>구문  
  
```    
sp_delete_database_firewall_rule [@name =] [N]'name'
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 `[@name =] [N]'name'`  
 제거할 데이터베이스 수준 방화벽 설정의 이름입니다. *name* 은 **nvarchar (128)** 이며 기본값은 없습니다. 유니코드 식별자는 `N` 의 경우 선택 사항입니다 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] . 
  
## <a name="permissions"></a>사용 권한  
 프로 비전 프로세스에서 생성 된 서버 수준 보안 주체 로그인 또는 관리자로 할당 된 Azure Active Directory 보안 주체가 데이터베이스 수준 방화벽 규칙을 삭제할 수 있습니다.  
  
## <a name="example"></a>예  
 다음 예에서는 이라는 데이터베이스 수준 방화벽 설정을 제거 합니다 `Example DB Setting 1` .
  
```  
-- Remove database-level firewall setting  
EXECUTE sp_delete_database_firewall_rule N'Example DB Setting 1';  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Azure SQL Database 방화벽](/azure/azure-sql/database/firewall-configure)   
 [방법: 방화벽 설정 구성 (Azure SQL Database)](/azure/azure-sql/database/firewall-configure)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
