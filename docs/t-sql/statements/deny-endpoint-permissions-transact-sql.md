---
title: "DENY 끝점 사용 권한 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- endpoints [SQL Server], permissions
- DENY statement, endpoints
- denying permissions [SQL Server], endpoints
- permissions [SQL Server], endpoints
ms.assetid: 3ac40457-7529-4eda-95a4-5247345cc8cf
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a263d6a5a576b4f4e06bb44a6c6fb40c99e64660
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="deny-endpoint-permissions-transact-sql"></a>DENY 끝점 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  끝점에 대한 사용 권한을 거부합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DENY permission  [ ,...n ] ON ENDPOINT :: endpoint_name  
    TO < server_principal >  [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>인수  
 *사용 권한*  
 끝점에 대해 거부할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 끝점에서 **::***endpoint_name*  
 사용 권한을 거부할 끝점을 지정합니다. 범위 한정자 (**::**)가 필요 합니다.  
  
 \<server_principal >  
 사용 권한을 거부할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
 *SQL_Server_login*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *SQL_Server_login_from_Windows_login*  
 Windows 로그인에서 생성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *SQL_Server_login_from_certificate*  
 인증서로 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *SQL_Server_login_from_AsymKey*  
 비대칭 키에 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 CASCADE  
 사용 권한이 거부된 보안 주체에게 사용 권한을 부여 받은 다른 보안 주체의 사용 권한도 거부됨을 나타냅니다.  
  
 AS *SQL_Server_login*  
 지정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 쿼리를 실행 하는 보안 주체는 권한을 부여할 권한이 거부 파생 되는 로그인입니다.  
  
## <a name="remarks"></a>주의  
 현재 데이터베이스는 경우에 서버 범위의 사용 권한은 거부 될 수 **마스터**합니다.  
  
 끝점에 대 한 정보는 [sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md) 카탈로그 뷰에 있습니다. 서버 사용 권한 정보에 표시 됩니다는 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 카탈로그 뷰 및 서버 보안 주체에 대 한 정보에 표시 되는 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 카탈로그 뷰.  
  
 끝점은 서버 수준 보안 개체입니다. 다음 표에는 끝점에 대해 거부할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|끝점 사용 권한|끝점 사용 권한에 포함된 사용 권한|서버 사용 권한에 포함된 사용 권한|  
|-------------------------|------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY ENDPOINT|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 끝점에 대한 CONTROL 권한 또는 서버에 대한 ALTER ANY ENDPOINT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-denying-view-definition-permission-on-an-endpoint"></a>1. 끝점에 대한 VIEW DEFINITION 권한 거부  
 다음 예제에서는 거부 `VIEW DEFINITION` 끝점에 대 한 `Mirror7` 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `ZArifin`합니다.  
  
```  
USE master;  
DENY VIEW DEFINITION ON ENDPOINT::Mirror7 TO ZArifin;  
GO  
```  
  
### <a name="b-denying-take-ownership-permission-with-cascade-option"></a>2. CASCADE 옵션을 지정하여 TAKE OWNERSHIP 권한 거부  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 `TAKE OWNERSHIP` 및 `Shipping83`가 `PKomosinski`을 부여한 보안 주체에 대해 끝점 `PKomosinski`에 대한 `TAKE OWNERSHIP` 권한을 거부합니다.  
  
```  
USE master;  
DENY TAKE OWNERSHIP ON ENDPOINT::Shipping83 TO PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [GRANT 끝점 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [REVOKE 끝점 사용 권한 &#40; Transact SQL &#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [끝점 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [sys.endpoints &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

