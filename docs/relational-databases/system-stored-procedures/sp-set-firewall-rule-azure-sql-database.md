---
description: sp_set_firewall_rule(Azure SQL Database)
title: sp_set_firewall_rule (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest
ms.openlocfilehash: 795aeb9a03f839cae400e92060ac21056f314d2f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468284"
---
# <a name="sp_set_firewall_rule-azure-sql-database"></a>sp_set_firewall_rule(Azure SQL Database)
[!INCLUDE [asdb-asa](../../includes/applies-to-version/asdb-asa.md)]

  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 대한 서버 수준 방화벽 설정을 만들거나 업데이트합니다. 이 저장 프로시저는 master 데이터베이스에서 서버 수준 보안 주체 로그인 또는 할당 된 Azure Active Directory 보안 주체에만 사용할 수 있습니다.  
  
  
## <a name="syntax"></a>구문  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 다음 표에서는에서 지원 되는 인수와 옵션을 보여 줍니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] .  
  
|Name|Datatype|설명|  
|----------|--------------|-----------------|  
|[ @name =] ' name '|**NVARCHAR (128)**|서버 수준의 방화벽 설정을 설명하고 구분하는 데 사용된 이름입니다.|  
|[ @start_ip_address =] ' start_ip_address '|**VARCHAR (50)**|서버 수준 방화벽 설정 범위에서 가장 낮은 IP 주소입니다. 이 값보다 크거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 연결을 시도할 수 있습니다. 가능한 가장 낮은 IP 주소는 `0.0.0.0`입니다.|  
|[ @end_ip_address =] ' end_ip_address '|**VARCHAR (50)**|서버 수준 방화벽 설정 범위에서 가장 높은 IP 주소입니다. 이 값보다 작거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 연결을 시도할 수 있습니다. 가능한 가장 높은 IP 주소는 `255.255.255.255`입니다.<br /><br /> 참고:이 필드와 *start_ip_address* 필드가 모두 이면 Azure 연결을 시도할 수 있습니다 `0.0.0.0` .|  
  
## <a name="remarks"></a>설명  
 서버 수준 방화벽 설정 이름은 고유해야 합니다. 저장 프로시저에 대해 제공된 설정 이름이 해당 방화벽 설정 테이블에 이미 있습니다. 시작 및 끝 IP 주소가 업데이트됩니다. 그렇지 않으면, 새 서버 수준 방화벽 설정이 만들어집니다.  
  
 시작 IP 주소와 끝 IP 주소가 `0.0.0.0`인 서버 수준 방화벽 설정을 추가하면 Azure에서 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 액세스할 수 있습니다. 서버 수준 방화벽 설정의 용도를 기억할 수 있도록 하는 *이름* 매개 변수에 값을 제공 합니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 강제 실행하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.  
  
## <a name="permissions"></a>사용 권한  
 프로 비전 프로세스에서 생성 된 서버 수준 보안 주체 로그인 또는 관리자로 할당 된 Azure Active Directory 보안 주체가 서버 수준 방화벽 규칙을 만들거나 수정할 수 있습니다. Sp_set_firewall_rule를 실행 하려면 사용자가 master 데이터베이스에 연결 되어 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 코드는 Azure에서 액세스를 허용하는 `Allow Azure`라는 서버 수준 방화벽 설정을 만듭니다. 가상 master 데이터베이스에서 다음을 실행 합니다.  
  
```  
-- Enable Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 다음 코드는 `Example setting 1` IP 주소에 대해서만 `0.0.0.2`이라는 서버 수준 방화벽 설정을 만듭니다. 그런 다음 `sp_set_firewall_rule` `0.0.0.4` 해당 방화벽 설정에서 끝 IP 주소를로 업데이트 하기 위해 저장 프로시저를 다시 호출 합니다. 이렇게 하면 IP 주소, `0.0.0.2` `0.0.0.3` 및가 `0.0.0.4` 서버에 액세스할 수 있는 범위가 만들어집니다.  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Azure SQL Database 방화벽](/azure/azure-sql/database/firewall-configure)   
 [방법: 방화벽 설정 구성 (Azure SQL Database)](/azure/azure-sql/database/firewall-configure)   
 [sys.firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)