---
title: "sp_set_database_firewall_rule (Azure SQL 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 08/04/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c83057218c015eb9d3488ea730e507ab795ddade
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spsetdatabasefirewallrule-azure-sql-database"></a>sp_set_database_firewall_rule(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  에 대 한 데이터베이스 수준 방화벽 규칙을 만들거나 여 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다. 에 대 한 데이터베이스 방화벽 규칙을 구성할 수 있습니다는 **마스터** 데이터베이스 및 사용자 데이터베이스에 대 한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다. 데이터베이스 방화벽 규칙은 포함 된 데이터베이스 사용자를 사용할 때 특히 유용 합니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)를 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 **[@name**  =] [N]'*이름*'  
 데이터베이스 수준의 방화벽 설정을 설명하고 구분하는 데 사용된 이름입니다. *이름* 은 **nvarchar (128)** 기본값은 없습니다. 유니코드 식별자 `N` 는 선택 사항에 대 한 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]합니다. 
  
 **[@start_ip_address**  =] '*start_ip_address*'  
 데이터베이스 수준의 방화벽 설정 범위에서 가장 낮은 IP 주소입니다. 이 값보다 크거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 인스턴스에 연결을 시도할 수 있습니다. 가능한 가장 낮은 IP 주소는 `0.0.0.0`입니다. *start_ip_address* 은 **varchar (50)** 기본값은 없습니다.  
  
 [ **@end_ip_address**  =] '*end_ip_address*'  
 데이터베이스 수준의 방화벽 설정 범위에서 가장 높은 IP 주소입니다. 이 값보다 작거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 인스턴스에 연결을 시도할 수 있습니다. 가능한 가장 높은 IP 주소는 `255.255.255.255`입니다. *end_ip_address* 은 **varchar (50)** 기본값은 없습니다.  
  
 다음 표에서 지원 되는 인수를 보여 줍니다. 및 옵션에 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
> [!NOTE]  
>  Azure 연결을 시도할 때이 필드와 *start_ip_address* equals 필드 `0.0.0.0`합니다.  
  
## <a name="remarks"></a>주의  
 데이터베이스의 데이터베이스 수준 방화벽 설정 이름은 고유해야 합니다. 저장 프로시저에 대해 제공된 데이터베이스 수준 방화벽 설정 이름이 해당 데이터베이스 수준 방화벽 설정 테이블에 이미 있습니다. 시작 및 끝 IP 주소가 업데이트됩니다. 그렇지 않으면, 새 데이터베이스 수준 방화벽 설정이 만들어집니다.  
  
 시작 및 끝 IP 주소를 일치 하는 데이터베이스 수준 방화벽 설정을 추가 하면 `0.0.0.0`, 데이터베이스에 대 한 액세스를 사용 하면는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Azure 리소스에서는 서버입니다. 값을 제공 된 *이름* 데 도움이 되는 매개 변수는 방화벽 설정을 기억할에 대 한 합니다.  
  
## <a name="permissions"></a>Permissions  
 필요한 **제어** 데이터베이스에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
 다음 코드에서는 데이터베이스 수준 방화벽 설정에서 호출 `Allow Azure` Azure에서 데이터베이스에 액세스할 수 있도록 합니다.  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 다음 코드는 `Example DB Setting 1` IP 주소에 대해서만 `0.0.0.4`이라는 데이터베이스 수준 방화벽 설정을 만듭니다. 그런 다음 `sp_set_database firewall_rule` 끝 IP 주소를 업데이트 하려면 저장된 프로시저를 다시 호출 `0.0.0.6`한다는 점에서, 방화벽 설정 합니다. 이렇게 하면 IP 주소를 허용 하는 범위를 만들어집니다 `0.0.0.4`, `0.0.0.5`, 및 `0.0.0.6` 데이터베이스에 액세스 합니다.
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Azure SQL 데이터베이스 방화벽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [방법: 방화벽 설정 구성 (Azure SQL 데이터베이스)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule&#40; Azure SQL 데이터베이스 &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40; Azure SQL 데이터베이스 &#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40; Azure SQL 데이터베이스 &#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
