---
title: firewall_rules (Azure SQL Database) | Microsoft Docs
ms.date: 03/26/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.firewall_rules
- firewall_rules
- sys.firewall_rules_TSQL
- firewall_rules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- firewall_rules
- sys.firewall_rules
ms.assetid: 140d2cd8-9aa1-4cc5-870d-e1dbc873b3fe
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 91c3a4101f19afe4a986514fea8dab207c6d9b48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70155547"
---
# <a name="sysfirewall_rules-azure-sql-database"></a>sys.firewall_rules(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  와 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]연결 된 서버 수준 방화벽 설정에 대 한 정보를 반환 합니다.  
  
 
  `sys.firewall_rules` 뷰는 다음 열을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|id|**INT**|서버 수준 방화벽 설정의 식별자입니다.|  
|name|**NVARCHAR (128)**|서버 수준 방화벽 설정을 설명하고 구분하기 위해 선택한 이름입니다.|  
|start_ip_address|**VARCHAR (45)**|서버 수준 방화벽 설정 범위에서 가장 낮은 IP 주소입니다. 이 값보다 크거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 연결을 시도할 수 있습니다. 가능한 가장 낮은 IP 주소는 `0.0.0.0`입니다.|  
|end_ip_address|**VARCHAR (45)**|서버 수준 방화벽 설정 범위에서 가장 높은 IP 주소입니다. 이 값보다 작거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 연결을 시도할 수 있습니다. 가능한 가장 높은 IP 주소는 `255.255.255.255`입니다.<br /><br /> 참고:이 필드와 **start_ip_address** 필드가 모두 이면 `0.0.0.0`Azure 연결을 시도할 수 있습니다.|  
|create_date|**날짜**|서버 수준 방화벽 설정이 만들어진 UTC 날짜 및 시간입니다.<br /><br /> 참고: UTC는 협정 세계시의 머리글자어입니다.|  
|modify_date|**날짜**|서버 수준 방화벽 설정이 마지막 수정된 UTC 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>설명

 Microsoft Azure SQL Database와 연결 된 데이터베이스 수준 방화벽 설정에 대 한 정보를 반환 하려면 [&#41;&#40;Azure SQL Database database_firewall_rules ](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)를 사용 합니다.  
  
## <a name="permissions"></a>사용 권한

 **Master** 데이터베이스에 연결할 수 있는 권한이 있는 모든 사용자는이 뷰에 대 한 읽기 전용 액세스를 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

[sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[FILESTREAM 액세스를 위한 방화벽 구성](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[보고서 서버 액세스를 위한 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
