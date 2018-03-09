---
title: sys.server_permissions (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.server_permissions_TSQL
- sys.server_permissions
- server_permissions
- server_permissions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_permissions catalog view
ms.assetid: 7d78bf17-6c64-4166-bd0b-9e9e20992136
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96312970ada17baf213e436e338986423526f470
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysserverpermissions-transact-sql"></a>sys.server_permissions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  각 서버 수준 사용 권한에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**클래스**|**tinyint**|사용 권한이 있는 클래스를 나타냅니다.<br /><br /> 100 = 서버<br /><br /> 101 = 서버 보안 주체<br /><br /> 105 = 끝점|  
|**class_desc**|**nvarchar (60)**|사용 권한이 있는 클래스에 대한 설명입니다. 다음 값 중 하나입니다.<br /><br /> **서버**<br /><br /> **SERVER_PRINCIPAL**<br /><br /> **ENDPOINT**|  
|**major_id**|**int**|사용 권한이 있는 보안 개체의 ID이며 클래스에 따라 해석됩니다. 대부분의 항목에서 이 ID는 클래스가 나타내는 대상의 ID입니다. 비표준 ID는 다음과 같이 해석됩니다.<br /><br /> 100 항상 0 =|  
|**minor_id**|**int**|사용 권한이 있는 대상의 보조 ID이며 클래스에 따라 해석됩니다.|  
|**grantee_principal_id**|**int**|사용 권한을 부여할 서버 보안 주체 ID입니다.|  
|**grantor_principal_id**|**int**|이 사용 권한을 부여한 사용자의 서버 보안 주체 ID입니다.|  
|**유형**|**char(4)**|서버 사용 권한의 유형입니다. 사용 권한 유형 목록은 다음 표를 참조하세요.|  
|**permission_name**|**nvarchar (128)**|사용 권한 이름입니다.|  
|**상태**|**char(1)**|사용 권한 상태입니다.<br /><br /> D = 거부<br /><br /> R = 취소<br /><br /> G = 허용<br /><br /> W = Grant 옵션을 사용하여 허용|  
|**state_desc**|**nvarchar (60)**|사용 권한 상태에 대한 설명입니다.<br /><br /> DENY<br /><br /> REVOKE<br /><br /> GRANT<br /><br /> GRANT_WITH_GRANT_OPTION|  
  
|사용 권한 유형|사용 권한 이름|보안 개체에 적용되는 항목|  
|---------------------|---------------------|--------------------------|  
|ADBO|ADMINISTER BULK OPERATIONS|SERVER|  
|AL|ALTER|ENDPOINT, LOGIN|  
|ALCD|ALTER ANY CREDENTIAL|SERVER|  
|ALCO|ALTER ANY CONNECTION|SERVER|  
|ALDB|ALTER ANY DATABASE|SERVER|  
|ALES|ALTER ANY EVENT NOTIFICATION|SERVER|  
|ALHE|ALTER ANY ENDPOINT|SERVER|  
|ALLG|ALTER ANY LOGIN|SERVER|  
|ALLS|ALTER ANY LINKED SERVER|SERVER|  
|ALRS|ALTER RESOURCES|SERVER|  
|ALSS|ALTER SERVER STATE|SERVER|  
|ALST|ALTER SETTINGS|SERVER|  
|ALTR|ALTER TRACE|SERVER|  
|AUTH|AUTHENTICATE SERVER|SERVER|  
|CL|CONTROL|ENDPOINT, LOGIN|  
|CL|CONTROL SERVER|SERVER|  
|CO|CONNECT|ENDPOINT|  
|COSQ|CONNECT SQL|SERVER|  
|CRDB|CREATE ANY DATABASE|SERVER|  
|CRDE|CREATE DDL EVENT NOTIFICATION|SERVER|  
|CRHE|CREATE ENDPOINT|SERVER|  
|CRTE|CREATE TRACE EVENT NOTIFICATION|SERVER|  
|IM|IMPERSONATE|Login|  
|SHDN|SHUTDOWN|SERVER|  
|TO|TAKE OWNERSHIP|ENDPOINT|  
|VW|VIEW DEFINITION|ENDPOINT, LOGIN|  
|VWAD|VIEW ANY DEFINITION|SERVER|  
|VWDB|VIEW ANY DATABASE|SERVER|  
|VWSS|VIEW SERVER STATE|SERVER|  
|XA|EXTERNAL ACCESS|SERVER|  
  
## <a name="permissions"></a>Permissions  
 모든 사용자는 자산의 권한을 볼 수 있습니다. 다른 로그인에 대한 사용 권한을 보려면 로그인할 때 VIEW DEFINITION, ALTER ANY LOGIN 또는 사용 권한이 필요합니다. 사용자 정의 서버 역할을 보려면 ANY SERVER ROLE 또는 역할의 멤버 자격이 필요합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 쿼리는 서버 보안 주체에 대해 명시적으로 부여되거나 거부된 사용 권한을 나열합니다.  
  
> [!IMPORTANT]  
>  고정 서버 역할의 사용 권한은 sys.server_permissions에 나타나지 않습니다. 따라서 서버 보안 주체가 여기에 나열되지 않은 추가 사용 권한을 가질 수 있습니다.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pe.state_desc, pe.permission_name   
FROM sys.server_principals AS pr   
JOIN sys.server_permissions AS pe   
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
  
  
