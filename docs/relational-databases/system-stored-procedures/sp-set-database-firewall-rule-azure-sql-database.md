---
title: sp_set_database_firewall_rule
titleSuffix: Azure SQL Database
ms.date: 08/04/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
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
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: dfe41ee68412414df24bc7f0bd583bbb0109b3db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74055085"
---
# <a name="sp_set_database_firewall_rule-azure-sql-database"></a>sp_set_database_firewall_rule(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  에 대 한 데이터베이스 수준 방화벽 규칙을 만들거나 업데이트 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다. 데이터베이스 방화벽 규칙은 **master** 데이터베이스 및의 사용자 데이터베이스에 대해 구성할 수 있습니다 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. 데이터베이스 방화벽 규칙은 포함 된 데이터베이스 사용자를 사용할 때 특히 유용 합니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)를 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] [N]'name'`데이터베이스 수준 방화벽 설정을 설명 하 고 구별 하는 데 사용 되는 이름입니다. *name* 은 **nvarchar (128)** 이며 기본값은 없습니다. 유니코드 식별자 `N` 는의 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]경우 선택 사항입니다. 
  
`[ @start_ip_address = ] 'start_ip_address'`데이터베이스 수준 방화벽 설정 범위에서 가장 낮은 IP 주소입니다. 이 값보다 크거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 인스턴스에 연결을 시도할 수 있습니다. 가능한 가장 낮은 IP 주소는 `0.0.0.0`입니다. *start_ip_address* 는 **varchar (50)** 이며 기본값은 없습니다.  
  
`[ @end_ip_address = ] 'end_ip_address'`데이터베이스 수준 방화벽 설정 범위에서 가장 높은 IP 주소입니다. 이 값보다 작거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 인스턴스에 연결을 시도할 수 있습니다. 가능한 가장 높은 IP 주소는 `255.255.255.255`입니다. *end_ip_address* 는 **varchar (50)** 이며 기본값은 없습니다.  
  
 다음 표에서는에서 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]지원 되는 인수와 옵션을 보여 줍니다.  
  
> [!NOTE]  
>  Azure 연결 시도는이 필드와 *start_ip_address* 필드가 모두 같은 `0.0.0.0`경우에 허용 됩니다.  
  
## <a name="remarks"></a>설명  
 데이터베이스의 데이터베이스 수준 방화벽 설정 이름은 고유해야 합니다. 저장 프로시저에 대해 제공된 데이터베이스 수준 방화벽 설정 이름이 해당 데이터베이스 수준 방화벽 설정 테이블에 이미 있습니다. 시작 및 끝 IP 주소가 업데이트됩니다. 그렇지 않으면, 새 데이터베이스 수준 방화벽 설정이 만들어집니다.  
  
 시작 IP 주소와 끝 IP 주소가와 동일한 `0.0.0.0`데이터베이스 수준 방화벽 설정을 추가 하면 모든 Azure 리소스에서 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 있는 데이터베이스에 액세스할 수 있습니다. 방화벽 설정의 용도를 기억할 수 있도록 하는 *이름* 매개 변수에 값을 제공 합니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 **CONTROL** 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 코드는 Azure에서 데이터베이스에 액세스할 수 있는 `Allow Azure`라는 데이터베이스 수준 방화벽 설정을 만듭니다.  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 다음 코드는 `Example DB Setting 1` IP 주소에 대해서만 `0.0.0.4`이라는 데이터베이스 수준 방화벽 설정을 만듭니다. 그런 다음 해당 `sp_set_database firewall_rule` 방화벽 설정에서 끝 IP 주소를로 `0.0.0.6`업데이트 하기 위해 저장 프로시저를 다시 호출 합니다. 이렇게 하면 IP 주소 `0.0.0.4` `0.0.0.5`, 및 `0.0.0.6` 가 데이터베이스에 액세스할 수 있는 범위가 만들어집니다.
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Azure SQL Database 방화벽](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [방법: 방화벽 설정 구성 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
