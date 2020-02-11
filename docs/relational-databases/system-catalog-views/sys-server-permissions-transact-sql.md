---
title: sys. server_permissions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2019
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cbfa717aa70bb057734a285e2b6d84fdc6f4961a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71163928"
---
# <a name="sysserver_permissions-transact-sql"></a>sys.server_permissions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  각 서버 수준 사용 권한에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**클래스**|**tinyint**|사용 권한이 있는 클래스를 나타냅니다.<br /><br /> 100 = 서버<br /><br /> 101 = 서버 보안 주체<br /><br /> 105 = 엔드포인트|  
|**class_desc**|**nvarchar (60)**|사용 권한이 있는 클래스에 대한 설명입니다. 해당 값은<br /><br /> **서버인**<br /><br /> **SERVER_PRINCIPAL**<br /><br /> **엔드포인트**|  
|**major_id**|**int**|사용 권한이 있는 보안 개체의 ID이며 클래스에 따라 해석됩니다. 대부분의 항목에서 이 ID는 클래스가 나타내는 대상의 ID입니다. 비표준 ID는 다음과 같이 해석됩니다.<br /><br /> 100 = 항상 0|  
|**minor_id**|**int**|사용 권한이 있는 대상의 보조 ID이며 클래스에 따라 해석됩니다.|  
|**grantee_principal_id**|**int**|사용 권한을 부여할 서버 보안 주체 ID입니다.|  
|**grantor_principal_id**|**int**|이 사용 권한을 부여한 사용자의 서버 보안 주체 ID입니다.|  
|**type**|**char (4)**|서버 사용 권한의 유형입니다. 사용 권한 유형 목록은 다음 표를 참조하세요.|  
|**permission_name**|**nvarchar(128)**|사용 권한 이름입니다.|  
|**상태일**|**char (1)**|사용 권한 상태입니다.<br /><br /> D = 거부<br /><br /> R = 취소<br /><br /> G = 허용<br /><br /> W = Grant 옵션을 사용하여 허용|  
|**state_desc**|**nvarchar (60)**|사용 권한 상태에 대한 설명입니다.<br /><br /> 거부<br /><br /> REVOKE<br /><br /> GRANT<br /><br /> GRANT_WITH_GRANT_OPTION|  
  
|사용 권한 유형|사용 권한 이름|보안 개체에 적용되는 항목|  
|---------------------|---------------------|--------------------------|  
|AAES|ALTER ANY EVENT SESSION|SERVER|
|ADBO|ADMINISTER BULK OPERATIONS|SERVER|  
|AL|ALTER|ENDPOINT, LOGIN|  
|ALAA|ALTER ANY SERVER AUDIT|SERVER|
|ALAG|ALTER ANY AVAILABILITY GROUP|SERVER|
|ALCD|ALTER ANY CREDENTIAL|SERVER|  
|ALCO|ALTER ANY CONNECTION|SERVER|  
|ALDB|ALTER ANY DATABASE|SERVER|  
|ALES|ALTER ANY EVENT NOTIFICATION|SERVER|  
|ALHE|ALTER ANY ENDPOINT|SERVER|  
|ALLG|ALTER ANY LOGIN|SERVER|  
|ALLS|ALTER ANY LINKED SERVER|SERVER|  
|ALRS|ALTER RESOURCES|SERVER|
|ALSR|ALTER ANY SERVER ROLE|SERVER|  
|ALSS|ALTER SERVER STATE|SERVER|  
|ALST|ALTER SETTINGS|SERVER|  
|ALTR|ALTER TRACE|SERVER|  
|AUTH|AUTHENTICATE SERVER|SERVER|
|CADB|CONNECT ANY DATABASE|SERVER|  
|CL|CONTROL|ENDPOINT, LOGIN|  
|CL|CONTROL SERVER|SERVER|  
|CO|CONNECT|엔드포인트|  
|COSQ|CONNECT SQL|SERVER|
|CRAC|CREATE AVAILABILITY GROUP|SERVER|  
|CRDB|CREATE ANY DATABASE|SERVER|  
|CRDE|CREATE DDL EVENT NOTIFICATION|SERVER|  
|CRHE|CREATE ENDPOINT|SERVER|
|CRSR|CREATE SERVER ROLE|SERVER|  
|CRTE|CREATE TRACE EVENT NOTIFICATION|SERVER|
|IAL|IMPERSONATE ANY LOGIN|SERVER|  
|IM|IMPERSONATE|LOGIN|  
|SHDN|SHUTDOWN|SERVER|
|SUS|SELECT ALL USER SECURABLES|SERVER|
|TO|TAKE OWNERSHIP|엔드포인트|  
|VW|VIEW DEFINITION|ENDPOINT, LOGIN|  
|VWAD|VIEW ANY DEFINITION|SERVER|  
|VWDB|VIEW ANY DATABASE|SERVER|  
|VWSS|VIEW SERVER STATE|SERVER|  
|XA|EXTERNAL ACCESS|SERVER|
|XU|UNSAFE ASSEMBLY|SERVER|
  
## <a name="permissions"></a>사용 권한  
 모든 사용자는 자산의 권한을 볼 수 있습니다. 다른 로그인에 대한 사용 권한을 보려면 로그인할 때 VIEW DEFINITION, ALTER ANY LOGIN 또는 사용 권한이 필요합니다. 사용자 정의 서버 역할을 보려면 ANY SERVER ROLE 또는 역할의 멤버 자격이 필요합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 쿼리는 서버 보안 주체에 대해 명시적으로 부여되거나 거부된 사용 권한을 나열합니다.  
  
> [!IMPORTANT]  
> 고정 서버 역할의 사용 권한은 sys.server_permissions에 나타나지 않습니다. 따라서 서버 보안 주체가 여기에 나열되지 않은 추가 사용 권한을 가질 수 있습니다.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pe.state_desc, pe.permission_name   
FROM sys.server_principals AS pr   
JOIN sys.server_permissions AS pe   
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 카탈로그 뷰](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [보안 개체](../../relational-databases/security/securables.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [권한 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
