---
title: SUSER_SNAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_SNAME_TSQL
- SUSER_SNAME
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- SIDs [SQL Server]
- SUSER_SNAME function
- users [SQL Server], logins
- logins [SQL Server], names
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- names [SQL Server], logins
ms.assetid: 11ec7d86-d429-4004-a436-da25df9f8761
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 29a0fc66901fe358113f244a770e70a9dbe2e12b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85994007"
---
# <a name="suser_sname-transact-sql"></a>SUSER_SNAME(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SID(보안 ID)와 연결된 로그인 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SUSER_SNAME ( [ server_user_sid ] )   
```  
  
## <a name="arguments"></a>인수  
 *server_user_sid*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
 선택적 로그인 보안 ID입니다. *server_user_sid*는 **varbinary(85)** 입니다. *server_user_sid*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 또는 그룹의 보안 ID일 수 있습니다. *server_user_sid*가 지정되지 않은 경우 현재 사용자에 대한 정보가 반환됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar(128)**  
  
## <a name="remarks"></a>설명  
 SUSER_SNAME을 ALTER TABLE 또는 CREATE TABLE에서 DEFAULT 제약 조건으로 사용할 수 있습니다. SUSER_SNAME은 SELECT 목록이나 WHERE 절, 그리고 식이 사용되는 모든 곳에 사용할 수 있습니다. 지정된 매개 변수가 없는 경우에도 SUSER_SNAME 다음에는 항상 괄호가 나와야 합니다.  
  
 인수 없이 SUSER_SNAME이 호출되면 현재 보안 컨텍스트의 이름이 반환됩니다. EXECUTE AS를 사용하여 컨텍스트를 전환한 일괄 처리 내에서 인수 없이 SUSER_SNAME이 호출되면 가장된 컨텍스트의 이름이 반환됩니다. 가장된 컨텍스트에서 SUSER_SNAME이 호출된 경우 ORIGINAL_LOGIN은 원래 컨텍스트의 이름을 반환합니다.  
  
## <a name="sssdsfull-remarks"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 주의 사항  
 SUSER_NAME은 항상 현재 보안 컨텍스트에 대한 로그인 이름을 반환합니다.  
  
 SUSER_SNAME 문은 EXECUTE AS를 통해 가장된 보안 컨텍스트를 사용하는 실행을 지원하지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-suser_sname"></a>A. SUSER_SNAME 사용  
 다음 예에서는 현재 보안 컨텍스트의 로그인 이름을 반환합니다.  
  
```  
SELECT SUSER_SNAME();  
GO  
```  
  
### <a name="b-using-suser_sname-with-a-windows-user-security-id"></a>B. Windows 사용자의 SID로 SUSER_SNAME 사용  
 다음 예에서는 Windows SID와 연결된 로그인 이름을 반환합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
```  
SELECT SUSER_SNAME(0x010500000000000515000000a065cf7e784b9b5fe77c87705a2e0000);  
GO  
```  
  
### <a name="c-using-suser_sname-as-a-default-constraint"></a>C. DEFAULT 제약 조건으로 SUSER_SNAME 사용  
 다음 예에서는 `SUSER_SNAME`를 `DEFAULT` 문의 `CREATE TABLE` 제약 조건으로 사용합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sname_example  
(  
login_sname sysname DEFAULT SUSER_SNAME(),  
employee_id uniqueidentifier DEFAULT NEWID(),  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sname_example DEFAULT VALUES;  
GO  
```  
  
### <a name="d-calling-suser_sname-in-combination-with-execute-as"></a>D. SUSER_SNAME을 EXECUTE AS와 함께 호출  
 이 예에서는 SUSER_SNAME이 가장된 컨텍스트에서 호출된 경우의 동작을 보여 줍니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상
  
```  
SELECT SUSER_SNAME();  
GO  
EXECUTE AS LOGIN = 'WanidaBenShoof';  
SELECT SUSER_SNAME();  
REVERT;  
GO  
SELECT SUSER_SNAME();  
GO  
  
```  
  
 결과는 다음과 같습니다.  
  
 ```
sa  
WanidaBenShoof  
sa
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-suser_sname"></a>E. SUSER_SNAME 사용  
 다음 예에서는 `0x01` 값을 갖는 SID에 대한 로그인 이름을 반환합니다.  
  
```  
SELECT SUSER_SNAME(0x01);  
GO  
```  
  
### <a name="f-returning-the-current-login"></a>F. 현재 로그인 반환  
 다음 예에서는 현재 로그인의 로그인 이름을 반환합니다.  
  
```  
SELECT SUSER_SNAME() AS CurrentLogin;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SUSER_SID&#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  

