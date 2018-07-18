---
title: sp_set_database_firewall_rule (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6fa2b1effae12bd8132c331d4e1ba33055c656e0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984125"
---
# <a name="spsetdatabasefirewallrule-azure-sql-database"></a>sp_set_database_firewall_rule(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  데이터베이스 수준 방화벽 규칙을 만들거나 여 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]입니다. 에 대 한 데이터베이스 방화벽 규칙을 구성할 수 있습니다 합니다 **마스터** 데이터베이스 및 사용자 데이터베이스에 대 한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다. 데이터베이스 방화벽 규칙은 포함 된 데이터베이스 사용자를 사용 하는 경우에 특히 유용 합니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)를 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 **[@name**  =] [N]'*이름*'  
 데이터베이스 수준의 방화벽 설정을 설명하고 구분하는 데 사용된 이름입니다. *이름을* 됩니다 **nvarchar (128)** 이며 기본값은 없습니다. 유니코드 식별자 `N` 사항임 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]합니다. 
  
 **[@start_ip_address**  =] '*start_ip_address*'  
 데이터베이스 수준의 방화벽 설정 범위에서 가장 낮은 IP 주소입니다. 이 값보다 크거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 인스턴스에 연결을 시도할 수 있습니다. 가능한 가장 낮은 IP 주소는 `0.0.0.0`입니다. *start_ip_address* 됩니다 **varchar(50)** 이며 기본값은 없습니다.  
  
 [**@end_ip_address** =] '*end_ip_address*'  
 데이터베이스 수준의 방화벽 설정 범위에서 가장 높은 IP 주소입니다. 이 값보다 작거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 인스턴스에 연결을 시도할 수 있습니다. 가능한 가장 높은 IP 주소는 `255.255.255.255`입니다. *end_ip_address* 됩니다 **varchar(50)** 이며 기본값은 없습니다.  
  
 다음 표에서 지원 되는 인수를 보여 줍니다. 및 옵션에 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]입니다.  
  
> [!NOTE]  
>  Azure 연결을 시도할 수 있습니다이 필드와 *start_ip_address* equals 필드 `0.0.0.0`합니다.  
  
## <a name="remarks"></a>Remarks  
 데이터베이스의 데이터베이스 수준 방화벽 설정 이름은 고유해야 합니다. 저장 프로시저에 대해 제공된 데이터베이스 수준 방화벽 설정 이름이 해당 데이터베이스 수준 방화벽 설정 테이블에 이미 있습니다. 시작 및 끝 IP 주소가 업데이트됩니다. 그렇지 않으면, 새 데이터베이스 수준 방화벽 설정이 만들어집니다.  
  
 시작 및 끝 IP 주소에 일치 하는 데이터베이스 수준 방화벽 설정을 추가 하는 경우 `0.0.0.0`, 데이터베이스에 대 한 액세스를 사용 하면는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 모든 Azure 리소스에서 서버. 값을 제공 합니다 *이름을* 도움이 되는 매개 변수는 방화벽 설정을 기억할에 대 한 합니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 코드는 데이터베이스 수준 이라는 방화벽 설정을 만듭니다 `Allow Azure` Azure에서 데이터베이스에 액세스할을 수 있는 합니다.  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 다음 코드는 `Example DB Setting 1` IP 주소에 대해서만 `0.0.0.4`이라는 데이터베이스 수준 방화벽 설정을 만듭니다. 그런 다음, `sp_set_database firewall_rule` 끝 IP 주소를 업데이트 하려면 저장된 프로시저를 다시 호출 `0.0.0.6`에, 방화벽 설정 합니다. 이 IP 주소를 허용 하는 범위를 만듭니다 `0.0.0.4`, `0.0.0.5`, 및 `0.0.0.6` 데이터베이스에 액세스할 수 있습니다.
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [Azure SQL Database 방화벽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [방법: 방화벽 설정 구성 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
