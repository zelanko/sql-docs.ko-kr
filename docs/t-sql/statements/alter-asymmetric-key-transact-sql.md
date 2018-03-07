---
title: ALTER ASYMMETRIC KEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/12/2017
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
- ALTER_ASYMMETRIC_KEY_TSQL
- ALTER ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- passwords [SQL Server], asymmetric keys
- encryption [SQL Server], asymmetric keys
- DECRYPTION BY PASSWORD option
- ALTER ASYMMETRIC KEY statement
- asymmetric keys [SQL Server], modifying
ms.assetid: 958e95d6-fbe6-43e8-abbd-ccedbac2dbac
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13acb5d893188d08d8855d755c89cf9672eee066
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-asymmetric-key-transact-sql"></a>ALTER ASYMMETRIC KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  비대칭 키의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER ASYMMETRIC KEY Asym_Key_Name <alter_option>  
  
<alter_option> ::=  
      <password_change_option>   
    | REMOVE PRIVATE KEY   

<password_change_option> ::=  
    WITH PRIVATE KEY ( <password_option> [ , <password_option> ] )  

<password_option> ::=  
      ENCRYPTION BY PASSWORD = 'strongPassword'  
    | DECRYPTION BY PASSWORD = 'oldPassword'  
```  
  
## <a name="arguments"></a>인수  
 *Asym_Key_Name*  
 데이터베이스에서 비대칭 키를 식별하는 이름입니다.  
  
 REMOVE PRIVATE KEY  
 비대칭 키로부터 개인 키를 제거합니다. 공개 키는 제거되지 않습니다.  
  
 WITH PRIVATE KEY  
 개인 키의 보호를 변경합니다.  
  
 ENCRYPTION BY PASSWORD **='***stongPassword***'**  
 개인 키를 보호하기 위한 새 암호를 지정합니다. *암호* 의 인스턴스를 실행 하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이 옵션을 생략하면 개인 키가 데이터베이스 마스터 키로 암호화됩니다.  
  
 DECRYPTION BY PASSWORD **='***oldPassword***'**  
 개인 키가 현재 보호되는 이전 암호를 지정합니다. 개인 키가 데이터베이스 마스터 키로 암호화된 경우 필요하지 않습니다.  
  
## <a name="remarks"></a>주의  
 데이터베이스 마스터 키가 없으면 ENCRYPTION BY PASSWORD 옵션이 필요하고 암호가 제공되지 않으면 작업이 실패합니다. 데이터베이스 마스터 키를 만드는 방법에 대 한 정보를 참조 하세요. [CREATE MASTER key&#40; Transact SQL &#41; ](../../t-sql/statements/create-master-key-transact-sql.md).  
  
 ALTER ASYMMETRIC KEY를 사용하면 다음 표에서와 같이 PRIVATE KEY 옵션을 지정하여 개인 키 보호를 변경할 수 있습니다.  
  
|변경할 보호 방법|ENCRYPTION BY PASSWORD|DECRYPTION BY PASSWORD|  
|----------------------------|----------------------------|----------------------------|  
|이전 암호를 새 암호로 변경|필수|필수임|  
|암호를 마스터 키로 변경|생략|필수임|  
|마스터 키를 암호로 변경|필수임|생략|  
  
 개인 키를 보호하는 데 사용하려면 먼저 데이터베이스 마스터 키를 열어야 합니다. 자세한 내용은 참조 [OPEN MASTER key&#40; Transact SQL &#41; ](../../t-sql/statements/open-master-key-transact-sql.md).  
  
 비대칭 키의 소유권을 변경 하려면 사용 [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 개인 키를 제거하는 경우 비대칭 키에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-password-of-the-private-key"></a>1. 개인 키의 암호 변경  
 다음 예에서는 비대칭 키 `PacificSales09`의 개인 키를 보호하는 데 사용된 암호를 변경합니다. 새 암호는 `<enterStrongPasswordHere>`입니다.  
  
```  
ALTER ASYMMETRIC KEY PacificSales09   
    WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<oldPassword>',  
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>');  
GO  
```  
  
### <a name="b-removing-the-private-key-from-an-asymmetric-key"></a>2. 비대칭 키로부터 개인 키 제거  
 다음 예에서는 `PacificSales19`에서 개인 키를 제거하여 공개 키만 남겨 둡니다.  
  
```  
ALTER ASYMMETRIC KEY PacificSales19 REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="c-removing-password-protection-from-a-private-key"></a>3. 개인 키로부터 암호 보호 제거  
 다음 예에서는 개인 키에서 암호 보호를 제거하고 데이터베이스 마스터 키로 보호합니다.  
  
```  
OPEN MASTER KEY;  
ALTER ASYMMETRIC KEY PacificSales09 WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<enterStrongPasswordHere>' );  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [SQL Server 및 데이터베이스 암호화 키&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [MASTER key&#40; 열기 Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
