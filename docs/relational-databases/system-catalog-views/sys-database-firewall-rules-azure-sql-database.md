---
title: "sys.database_firewall_rules (Azure SQL 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_firewall_rules_TSQL
- database_firewall_rules_TSQL
- sys.database_firewall_rules
- database_firewall_rules
dev_langs:
- TSQL
helpviewer_keywords:
- database_firewall_rules
- sys.database_firewall_rules
ms.assetid: 2e821593-3b9f-43d6-a99b-1ceffe177faf
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c598371c8df7a92622ec43700fc504b082640e1f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabasefirewallrules-azure-sql-database"></a>sys.database_firewall_rules(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  와 연결 된 데이터베이스 수준 방화벽 설정에 대 한 정보를 반환 하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다. 데이터베이스 수준 방화벽 설정은 포함된 데이터베이스 사용자를 사용할 때 특히 유용합니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)를 참조하세요.  
  
 `sys.database_firewall_rules` 뷰는 다음 열을 포함합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|id|**정수**|데이터베이스 수준 방화벽 설정의 식별자입니다.|  
|name|**NVARCHAR (128)**|데이터베이스 수준의 방화벽 설정을 설명하고 구분하기 위해 선택한 이름입니다.|  
|start_ip_address|**VARCHAR (50)**|데이터베이스 수준의 방화벽 설정 범위에서 가장 낮은 IP 주소입니다. 이 값보다 크거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 인스턴스에 연결을 시도할 수 있습니다. 가능한 가장 낮은 IP 주소는 `0.0.0.0`입니다.|  
|end_ip_address|**VARCHAR (50)**|방화벽 설정 범위에서 가장 높은 IP 주소입니다. 이 값보다 작거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 인스턴스에 연결을 시도할 수 있습니다. 가능한 가장 높은 IP 주소는 `255.255.255.255`입니다.<br /><br /> 참고: Windows Azure 연결을 시도할 때이 필드와 **start_ip_address** equals 필드 `0.0.0.0`합니다.|  
|create_date|**날짜/시간**|데이터베이스 수준의 방화벽 설정이 만들어진 UTC 날짜 및 시간입니다.|  
|modify_date|**날짜/시간**|데이터베이스 수준의 방화벽 설정이 마지막으로 수정된 UTC 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>주의  
 데이터베이스 방화벽 규칙을 제거 하려면 [sp_delete_database_firewall_rule & #40; Azure SQL 데이터베이스 & #41; ](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md). 모든에 대해 방화벽 규칙을 설정 하려면 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 참조 [sp_set_firewall_rule & #40; Azure SQL 데이터베이스 & #41; ](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md). 기존 데이터베이스에 대 한 정보 방화벽 규칙을 반환 하려면 쿼리 [sys.database_firewall_rules (Azure SQL 데이터베이스)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 이 보기는에서 사용할 수는 **마스터** 데이터베이스와 각 사용자 데이터베이스에 있습니다. 데이터베이스에 대한 연결 권한을 가진 모든 사용자에게는 이 뷰에 대한 읽기 전용 액세스가 부여됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_set_firewall_rule& #40; Azure SQL 데이터베이스 & #41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules (Azure SQL 데이터베이스)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_delete_database_firewall_rule & #40; Azure SQL 데이터베이스 & #41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [FILESTREAM 액세스를 위한 방화벽 구성](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [보고서 서버 액세스를 위한 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
