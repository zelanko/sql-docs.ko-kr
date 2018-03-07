---
title: ADD SIGNATURE (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ADD SIGNATURE
- ADD_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ADD SIGNATURE statement
- adding digital signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 64d8b682-6ec1-4e5b-8aee-3ba11e72d21f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 022c07cfc66694642da57042284c638ca1587496
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="add-signature-transact-sql"></a>ADD SIGNATURE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  저장 프로시저, 함수, 어셈블리 또는 트리거에 디지털 서명을 추가하고 연대 서명도 추가합니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ADD [ COUNTER ] SIGNATURE TO module_class::module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | CERTIFICATE cert_name [ WITH PASSWORD = 'password' ]  
    | CERTIFICATE cert_name WITH SIGNATURE = signed_blob   
    | ASYMMETRIC KEY Asym_Key_Name  
    | ASYMMETRIC KEY Asym_Key_Name [ WITH PASSWORD = 'password'.]  
    | ASYMMETRIC KEY Asym_Key_Name WITH SIGNATURE = signed_blob  
```  
  
## <a name="arguments"></a>인수  
 *module_class*  
 서명을 추가할 모듈의 클래스입니다. 스키마 범위 모듈에 대한 기본값은 OBJECT입니다.  
  
 *모듈*  
 서명하거나 연대 서명할 저장 프로시저, 함수, 어셈블리 또는 트리거의 이름입니다.  
  
 인증서 *cert_name*  
 저장 프로시저, 함수, 어셈블리 또는 트리거에 서명하거나 연대 서명하는 데 사용할 인증서의 이름입니다.  
  
 암호와 함께 ='*암호*'  
 인증서의 개인 키나 비대칭 키의 암호를 해독하는 데 필요한 암호입니다. 이 절은 개인 키가 데이터베이스 마스터 키로 보호되지 않는 경우에만 필요합니다.  
  
 서명 =*signed_blob*  
 모듈의 서명된 BLOB(Binary Large Object)를 지정합니다. 이 절은 개인 키를 포함하지 않고 모듈을 제공하려는 경우 유용합니다. 이 절을 사용할 때는 모듈, 서명 및 공개 키만 있으면 서명된 BLOB(Binary Large Object)을 데이터베이스에 추가할 수 있습니다. *signed_blob* 은 16 진수 형식의 blob 자체입니다.  
  
 비대칭 키 *Asym_Key_Name*  
 저장 프로시저, 함수, 어셈블리 또는 트리거에 서명하거나 연대 서명하는 데 사용할 비대칭 키의 이름입니다.  
  
## <a name="remarks"></a>주의  
 서명하거나 연대 서명할 모듈과 모듈에 서명하는 데 사용되는 인증서 또는 비대칭 키가 있어야 합니다. 모듈의 모든 문자는 서명 계산에 포함됩니다. 여기에는 선행 캐리지 리턴과 줄 바꿈도 포함됩니다.  
  
 모듈에 서명하거나 연대 서명하는 데 사용되는 인증서와 비대칭 키의 수는 제한되지 않습니다.  
  
 모듈이 변경되면 모듈의 서명이 삭제됩니다.  
  
 모듈에 EXECUTE AS 절이 포함되어 있으면 보안 주체의 SID(보안 ID)도 서명 프로세스의 일부로 포함됩니다.  
  
> [!CAUTION]  
>  모듈 서명은 사용 권한을 부여하는 용도로만 사용해야 하며 사용 권한을 거부하거나 취소하는 용도로 사용하면 안 됩니다.  
  
 인라인 테이블 반환 함수에 서명할 수 없습니다.  
  
 서명 정보는 sys.crypt_properties 카탈로그 뷰에 표시됩니다.  
  
> [!WARNING]  
>  서명 절차를 다시 만들 때 원래 일괄 처리의 모든 문은 다시 만들기 일괄 처리와 일치해야 합니다. 공백이나 주석이라도 일괄 처리 일부가 다를 경우 결과 서명이 달라집니다.  
  
## <a name="countersignatures"></a>연대 서명  
 서명 된 모듈을 실행할 때는 서명이 일시적으로 추가 SQL 토큰에 되지만 모듈에서 다른 모듈을 실행 하거나 실행을 종료 하면 서명은 손실 됩니다. 연대 서명은 특수 한 형식의 서명이 있습니다. 그 자체로는 사용 권한을 부여하지 않습니다. 그러나 동일한 인증서나 비대칭 키를 통해 만든 서명을 연대 서명된 개체에 대한 호출 기간 동안 유지할 수 있도록 허용합니다.  
  
 예를 들어 Alice라는 사용자가 ProcSelectT1ForAlice 프로시저를 호출하고, 이 프로시저가 procSelectT1 프로시저를 호출하며, 이 프로시저는 T1 테이블에서 선택한다고 가정해 보겠습니다. Alice에게는 ProcSelectT1ForAlice 및 procSelectT1에 대한 EXECUTE 권한은 있지만 T1에 대한 SELECT 권한은 없으며 이 전체 체인에 소유권 체인은 포함되어 있지 않습니다. Alice는 직접적으로 또는 ProcSelectT1ForAlice 및 procSelectT1을 사용해 T1 테이블에 액세스할 수 없습니다. Alice가 항상 ProcSelectT1ForAlice를 사용 하 여 액세스를 위해 할 것 이므로 procSelectT1 실행 권한은 부여 하려고 하지 않습니다. 아래에서는 이 작업을 수행하는 방법에 대해 설명합니다.  
  
-   procSelectT1이 T1에 액세스할 수 있도록 procSelectT1에 서명을 하면 Alice가 procSelectT1을 직접 호출할 수 있으므로 ProcSelectT1ForAlice를 호출하지 않아도 됩니다.  
  
-   Alice에 대해 procSelectT1에 대한 EXECUTE 권한을 거부할 수도 있지만, 이렇게 하면 Alice가 ProcSelectT1ForAlice를 통해 procSelectT1을 호출할 수 없게 됩니다.  
  
-   ProcSelectT1ForAlice에 서명을 해도 procSelectT1을 호출하는 과정에서 서명이 손실되기 때문에 그 자체로는 작업이 수행되지 않습니다.  
  
그러나 ProcSelectT1ForAlice에 서명 하는 데 사용 하는 같은 인증서로 procSelectT1 연대 서명을으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호출 체인 전체에 대해 서명을 유지 하 고 t 1에 대 한 액세스를 허용 됩니다. 연대 서명은 아무런 권한을 부여하지 않으므로 Alice가 procSelectT1을 직접 호출하려고 시도해도 T1에는 액세스할 수 없습니다. 아래의 3번 예에서는 이 예에 사용할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 보여 줍니다.  
  
## <a name="permissions"></a>Permissions  
 개체에 대한 ALTER 권한과 인증서 또는 비대칭 키에 대한 CONTROL 권한이 필요합니다. 연결된 개인 키가 암호로 보호되어 있으면 사용자도 암호가 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-signing-a-stored-procedure-by-using-a-certificate"></a>1. 인증서를 사용하여 저장 프로시저에 서명  
 다음 예에서는 `HumanResources.uspUpdateEmployeeLogin` 인증서를 사용하여 `HumanResourcesDP` 저장 프로시저에 서명합니다.  
  
```  
USE AdventureWorks2012;  
ADD SIGNATURE TO HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
### <a name="b-signing-a-stored-procedure-by-using-a-signed-blob"></a>2. 서명된 BLOB을 사용하여 저장 프로시저에 서명  
 다음 예에서는 새 데이터베이스를 만들고 예에서 사용할 인증서를 만듭니다. 예에서는 간단한 저장 프로시저를 만들어 서명하고 `sys.crypt_properties`에서 서명 BLOB을 검색합니다. 서명이 삭제된 후 다시 추가됩니다. 예에서는 WITH SIGNATURE 구문을 사용하여 프로시저에 서명합니다.  
  
```  
CREATE DATABASE TestSignature ;  
GO  
USE TestSignature ;  
GO  
-- Create a CERTIFICATE to sign the procedure.  
CREATE CERTIFICATE cert_signature_demo   
    ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
    WITH SUBJECT = 'ADD SIGNATURE demo';  
GO  
-- Create a simple procedure.  
CREATE PROC [sp_signature_demo]  
AS  
    PRINT 'This is the content of the procedure.' ;  
GO  
-- Sign the procedure.  
ADD SIGNATURE TO [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo]   
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y' ;  
GO  
-- Get the signature binary BLOB for the sp_signature_demo procedure.  
SELECT cp.crypt_property  
    FROM sys.crypt_properties AS cp  
    JOIN sys.certificates AS cer  
        ON cp.thumbprint = cer.thumbprint  
    WHERE cer.name = 'cert_signature_demo' ;  
GO  
```  
  
 이 문에서 반환하는 `crypt_property` 서명은 프로시저를 만들 때마다 달라집니다. 이 예의 뒷부분에서 사용할 수 있도록 결과를 적어 두십시오. 이 예에서는 나타나는 결과: `0x831F5530C86CC8ED606E5BC2720DA835351E46219A6D5DE9CE546297B88AEF3B6A7051891AF3EE7A68EAB37CD8380988B4C3F7469C8EABDD9579A2A5C507A4482905C2F24024FFB2F9BD7A953DD5E98470C4AA90CE83237739BB5FAE7BAC796E7710BDE291B03C43582F6F2D3B381F2102EEF8407731E01A51E24D808D54B373`합니다.  
  
```  
-- Drop the signature so that it can be signed again.  
DROP SIGNATURE FROM [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo];  
GO  
-- Add the signature. Use the signature BLOB obtained earlier.  
ADD SIGNATURE TO [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo]  
    WITH SIGNATURE = 0x831F5530C86CC8ED606E5BC2720DA835351E46219A6D5DE9CE546297B88AEF3B6A7051891AF3EE7A68EAB37CD8380988B4C3F7469C8EABDD9579A2A5C507A4482905C2F24024FFB2F9BD7A953DD5E98470C4AA90CE83237739BB5FAE7BAC796E7710BDE291B03C43582F6F2D3B381F2102EEF8407731E01A51E24D808D54B373 ;  
GO  
```  
  
### <a name="c-accessing-a-procedure-using-a-countersignature"></a>3. 연대 서명을 사용하여 프로시저 액세스  
 다음 예에서는 연대 서명을 통해 개체 액세스를 제어하는 방법을 보여 줍니다.  
  
```  
-- Create tesT1 database  
CREATE DATABASE testDB;  
GO  
USE testDB;  
GO  
-- Create table T1  
CREATE TABLE T1 (c varchar(11));  
INSERT INTO T1 VALUES ('This is T1.');  
  
-- Create a TestUser user to own table T1  
CREATE USER TestUser WITHOUT LOGIN;  
ALTER AUTHORIZATION ON T1 TO TestUser;  
  
-- Create a certificate for signing  
CREATE CERTIFICATE csSelectT  
  ENCRYPTION BY PASSWORD = 'SimplePwd01'  
  WITH SUBJECT = 'Certificate used to grant SELECT on T1';  
CREATE USER ucsSelectT1 FROM CERTIFICATE csSelectT;  
GRANT SELECT ON T1 TO ucsSelectT1;  
  
-- Create a principal with low privileges  
CREATE LOGIN Alice WITH PASSWORD = 'SimplePwd01';  
CREATE USER Alice;  
  
-- Verify Alice cannoT1 access T1;  
EXECUTE AS LOGIN = 'Alice';  
    SELECT * FROM T1;  
REVERT;  
  
-- Create a procedure that directly accesses T1  
CREATE PROCEDURE procSelectT1 AS  
BEGIN  
    PRINT 'Now selecting from T1...';  
    SELECT * FROM T1;  
END;  
GO  
GRANT EXECUTE ON procSelectT1 to public;  
  
-- Create special procedure for accessing T1  
CREATE PROCEDURE  procSelectT1ForAlice AS  
BEGIN  
   IF USER_ID() <> USER_ID('Alice')  
    BEGIN  
        PRINT 'Only Alice can use this.';  
        RETURN  
    END  
   EXEC procSelectT1;  
END;  
GO;  
GRANT EXECUTE ON procSelectT1ForAlice TO PUBLIC;  
  
-- Verify procedure works for a sysadmin user  
EXEC procSelectT1ForAlice;  
  
-- Alice still can't use the procedure yet  
EXECUTE AS LOGIN = 'Alice';  
    EXEC procSelectT1ForAlice;  
REVERT;  
  
-- Sign procedure to grant it SELECT permission  
ADD SIGNATURE TO procSelectT1ForAlice BY CERTIFICATE csSelectT   
WITH PASSWORD = 'SimplePwd01';  
  
-- Counter sign proc_select_t, to make this work  
ADD COUNTER SIGNATURE TO procSelectT1 BY CERTIFICATE csSelectT   
WITH PASSWORD = 'SimplePwd01';  
  
-- Now the proc works.   
-- Note that calling procSelectT1 directly still doesn't work  
EXECUTE AS LOGIN = 'Alice';  
    EXEC procSelectT1ForAlice;  
    EXEC procSelectT1;  
REVERT;  
  
-- Cleanup  
USE master;  
GO  
DROP DATABASE testDB;  
DROP LOGIN Alice;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.crypt_properties &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [DROP 서명 &#40; Transact SQL &#41;](../../t-sql/statements/drop-signature-transact-sql.md)  
  
  
