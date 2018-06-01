---
title: sys.firewall_rules (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 090ec967e25fff1fac3761298214e0366c0f2478
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "33180259"
---
# <a name="sysfirewallrules-azure-sql-database"></a>sys.firewall_rules(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  와 연결 된 서버 수준 방화벽 설정에 대 한 정보를 반환 하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]합니다.  
  
 `sys.firewall_rules` 뷰는 다음 열을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|id|**INT**|서버 수준 방화벽 설정의 식별자입니다.|  
|NAME|**NVARCHAR (128)**|서버 수준 방화벽 설정을 설명하고 구분하기 위해 선택한 이름입니다.|  
|start_ip_address|**VARCHAR (50)**|서버 수준 방화벽 설정 범위에서 가장 낮은 IP 주소입니다. 이 값보다 크거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 연결을 시도할 수 있습니다. 가능한 가장 낮은 IP 주소는 `0.0.0.0`입니다.|  
|end_ip_address|**VARCHAR (50)**|서버 수준 방화벽 설정 범위에서 가장 높은 IP 주소입니다. 이 값보다 작거나 같은 IP 주소는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서버에 연결을 시도할 수 있습니다. 가능한 가장 높은 IP 주소는 `255.255.255.255`입니다.<br /><br /> 참고: Windows Azure 연결을 시도할 때이 필드와 **start_ip_address** equals 필드 `0.0.0.0`합니다.|  
|create_date|**날짜/시간**|서버 수준 방화벽 설정이 만들어진 UTC 날짜 및 시간입니다.<br /><br /> 참고: UTC는 약어 표준시입니다.|  
|modify_date|**날짜/시간**|서버 수준 방화벽 설정이 마지막 수정된 UTC 날짜 및 시간입니다.|  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 방화벽 규칙을 제거 하려면 [sp_delete_firewall_rule &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)합니다. 단일 데이터베이스에 대 한 방화벽 규칙을 설정 하려면 참조 [sys.database_firewall_rules &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)합니다. 기존 방화벽 규칙에 대 한 정보를 반환 하려면 sys.firewall_rules (Azure SQL 데이터베이스)를 쿼리 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 보기에 읽기 전용 액세스는 연결할 수 있는 권한이 있는 모든 사용자가 사용할 수는 **마스터** 데이터베이스입니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.database_firewall_rules &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_set_firewall_rule &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [FILESTREAM 액세스를 위한 방화벽 구성](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [보고서 서버 액세스를 위한 방화벽 구성](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [방법: 방화벽 설정 구성(Azure SQL 데이터베이스)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
