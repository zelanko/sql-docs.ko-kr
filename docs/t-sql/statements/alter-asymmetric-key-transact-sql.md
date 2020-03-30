---
title: ALTER ASYMMETRIC KEY(Transact-SQL) | Microsoft Docs
ms.date: 04/12/2017
ms.prod: sql
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 06263499babe005bca36a982bc863dfa24356b5d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68066068"
---
# <a name="alter-asymmetric-key-transact-sql"></a>ALTER ASYMMETRIC KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  비대칭 키의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 비대칭 키로부터 프라이빗 키를 제거합니다. 퍼블릭 키는 제거되지 않습니다.  
  
 WITH PRIVATE KEY  
 프라이빗 키의 보호를 변경합니다.  
  
 ENCRYPTION BY PASSWORD **='***strongPassword***'**  
 프라이빗 키를 보호하기 위한 새 암호를 지정합니다. *password*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다. 이 옵션을 생략하면 프라이빗 키가 데이터베이스 마스터 키로 암호화됩니다.  
  
 DECRYPTION BY PASSWORD **='***oldPassword***'**  
 프라이빗 키가 현재 보호되는 이전 암호를 지정합니다. 프라이빗 키가 데이터베이스 마스터 키로 암호화된 경우 필요하지 않습니다.  
  
## <a name="remarks"></a>설명  
 데이터베이스 마스터 키가 없으면 ENCRYPTION BY PASSWORD 옵션이 필요하고 암호가 제공되지 않으면 작업이 실패합니다. 데이터베이스 마스터 키 만들기에 대한 자세한 내용은 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)를 참조하세요.  
  
 ALTER ASYMMETRIC KEY를 사용하면 다음 표에서와 같이 PRIVATE KEY 옵션을 지정하여 프라이빗 키 보호를 변경할 수 있습니다.  
  
|변경할 보호 방법|ENCRYPTION BY PASSWORD|DECRYPTION BY PASSWORD|  
|----------------------------|----------------------------|----------------------------|  
|이전 암호를 새 암호로 변경|필수|필수|  
|암호를 마스터 키로 변경|생략|필수|  
|마스터 키를 암호로 변경|필수|생략|  
  
 프라이빗 키를 보호하는 데 사용하려면 먼저 데이터베이스 마스터 키를 열어야 합니다. 자세한 내용은 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)를 참조하세요.  
  
 비대칭 키의 소유권을 변경하려면 [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)을 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 프라이빗 키를 제거하는 경우 비대칭 키에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-password-of-the-private-key"></a>A. 프라이빗 키의 암호 변경  
 다음 예에서는 비대칭 키 `PacificSales09`의 프라이빗 키를 보호하는 데 사용된 암호를 변경합니다. 새 암호는 `<enterStrongPasswordHere>`입니다.  
  
```  
ALTER ASYMMETRIC KEY PacificSales09   
    WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<oldPassword>',  
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>');  
GO  
```  
  
### <a name="b-removing-the-private-key-from-an-asymmetric-key"></a>B. 비대칭 키로부터 프라이빗 키 제거  
 다음 예에서는 `PacificSales19`에서 프라이빗 키를 제거하여 퍼블릭 키만 남겨 둡니다.  
  
```  
ALTER ASYMMETRIC KEY PacificSales19 REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="c-removing-password-protection-from-a-private-key"></a>C. 프라이빗 키로부터 암호 보호 제거  
 다음 예에서는 프라이빗 키에서 암호 보호를 제거하고 데이터베이스 마스터 키로 보호합니다.  
  
```  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<database master key password>';  
ALTER ASYMMETRIC KEY PacificSales09 WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<enterStrongPasswordHere>' );  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [SQL Server 및 데이터베이스 암호화 키&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
