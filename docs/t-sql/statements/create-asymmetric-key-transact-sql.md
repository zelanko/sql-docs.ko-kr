---
title: "비대칭 키 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 08/07/2017
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
- ASYMMETRIC_KEY_TSQL
- CREATE ASYMMETRIC KEY
- CREATE_ASYMMETRIC_KEY_TSQL
- ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], creating
- encryption [SQL Server], asymmetric keys
- CREATE ASYMMETRIC KEY statement
- asymmetric keys [SQL Server]
- cryptography [SQL Server], asymmetric keys
ms.assetid: 141bc976-7631-49f6-82bd-a235028645b1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: eeacba0076f6fed7b6dcda8802616dd9398df7ef
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="create-asymmetric-key-transact-sql"></a>CREATE ASYMMETRIC KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스에서 비대칭 키를 만듭니다.  
  
 이 기능은 Data Tier Application Framework(DACFx)를 사용하는 데이터베이스 내보내기와 호환되지 않습니다. 내보내기 전에 모든 비대칭 키를 삭제해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE ASYMMETRIC KEY Asym_Key_Name   
   [ AUTHORIZATION database_principal_name ]  
   [ FROM <Asym_Key_Source> ]  
   [ WITH <key_option> ] 
   [ ENCRYPTION BY <encrypting_mechanism> ] 
   [ ; ]
  
<Asym_Key_Source>::=  
     FILE = 'path_to_strong-name_file'  
   | EXECUTABLE FILE = 'path_to_executable_file'  
   | ASSEMBLY Assembly_Name  
   | PROVIDER Provider_Name  
  
<key_option> ::=  
   ALGORITHM = <algorithm>  
      |  
   PROVIDER_KEY_NAME = 'key_name_in_provider'  
      |  
      CREATION_DISPOSITION = { CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
      { RSA_4096 | RSA_3072 | RSA_2048 | RSA_1024 | RSA_512 }   
  
<encrypting_mechanism> ::=  
    PASSWORD = 'password'   
```  
  
## <a name="arguments"></a>인수  
 *Asym_Key_Source*  
 비대칭 키 쌍을 로드할 원본을 지정합니다.  
  
 권한 부여 *database_principal_name*  
 비대칭 키의 소유자를 지정합니다. 소유자는 역할 또는 그룹일 수 없습니다. 이 옵션을 생략하면 소유자가 현재 사용자가 됩니다.  
  
 파일 ='*path_to_strong name_file*'  
 키 쌍을 로드할 강력한 이름 파일의 경로를 지정합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 실행 파일 ='*path_to_executable_file*'  
 공개 키를 로드할 어셈블리 파일을 지정합니다. Windows API에서 MAX_PATH를 통해 260자로 제한됩니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 어셈블리 *Assembly_Name*  
 공개 키를 로드할 어셈블리 이름을 지정합니다.  
  
ENCRYPTION BY  *\<key_name_in_provider >* 키를 암호화 하는 방법을 지정 합니다. 인증서, 암호 또는 비대칭 키일 수 있습니다.  
  
 KEY_NAME ='*key_name_in_provider*'  
 외부 공급자의 키 이름을 지정합니다. 외부 키 관리에 대 한 자세한 내용은 참조 하세요. [확장 가능 키 관리 &#40; Ekm&#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 CREATION_DISPOSITION = CREATE_NEW  
 확장 가능 키 관리 장치에 새 키를 만듭니다. PROV_KEY_NAME을 사용하여 장치에 키 이름을 지정해야 합니다. 키가 이미 장치에 있는 경우 문이 오류와 함께 실패합니다.  
  
 CREATION_DISPOSITION = OPEN_EXISTING  
 지도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기존 확장 가능 키 관리 키에 비대칭 키입니다. PROV_KEY_NAME을 사용하여 장치에 키 이름을 지정해야 합니다. CREATION_DISPOSITION = OPEN_EXISTING을 지정하지 않은 경우 기본값은 CREATE_NEW입니다.  
  
 알고리즘 = \<알고리즘 >  
 5 개의 알고리즘 제공 될 수 있습니다. RSA_4096, RSA_3072, RSA_2048, RSA_1024, 및 RSA_512 합니다.  
  
 RSA_1024 및 RSA_512 사용 되지 않습니다. RSA_1024 또는 RSA_512 (권장 하지 않음) 사용 하 여 데이터베이스 호환성 수준을 120 이하로 설정 해야 합니다.  
  
 암호 = '*암호*'  
 개인 키를 암호화하는 데 사용할 암호를 지정합니다. 이 절이 없는 경우 개인 키는 데이터베이스 마스터 키로 암호화됩니다. *암호* 최대 128 자입니다. *암호* 의 인스턴스를 실행 하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="remarks"></a>주의  
 *비대칭 키* 는 데이터베이스 수준에서 보안 가능한 엔터티입니다. 기본 형태의 이 엔터티에는 공개 키와 개인 키가 모두 포함됩니다. FROM 절 없이 실행될 경우 CREATE ASYMMETRIC KEY는 새로운 키 쌍을 생성합니다. FROM 절로 실행될 경우 CREATE ASYMMETRIC KEY는 파일에서 키 쌍을 가져오거나 어셈블리에서 공개 키를 가져옵니다.  
  
 기본적으로 개인 키는 데이터베이스 마스터 키로 보호됩니다. 데이터베이스 마스터 키를 만든 경우 개인 키를 보호하기 위해 암호가 필요합니다. 데이터베이스 마스터 키가 있으면 암호는 선택 사항입니다.  
  
 개인 키의 길이는 512, 1024 또는 2048비트일 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CREATE ASYMMETRIC KEY 권한이 필요합니다. AUTHORIZATION 절이 지정된 경우 데이터베이스 보안 주체에 대한 IMPERSONATE 권한 또는 응용 프로그램 역할에 대한 ALTER 권한이 필요합니다. Windows 로그인, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 응용 프로그램 역할만 비대칭 키를 소유할 수 있습니다. 그룹 및 역할은 비대칭 키를 소유할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-an-asymmetric-key"></a>1. 비대칭 키 만들기  
 다음 예에서는 `PacificSales09` 알고리즘을 사용하여 `RSA_2048`라는 비대칭 키를 만들고 암호로 개인 키를 보호합니다.  
  
```  
CREATE ASYMMETRIC KEY PacificSales09   
    WITH ALGORITHM = RSA_2048   
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';   
GO  
```  
  
### <a name="b-creating-an-asymmetric-key-from-a-file-giving-authorization-to-a-user"></a>2. 파일로부터 비대칭 키를 만들어서 사용자에게 권한 부여  
 다음 예에서는 파일에 저장된 키 쌍으로부터 비대칭 키 `PacificSales19`를 만든 다음 사용자 `Christina`에게 비대칭 키를 사용할 수 있는 권한을 부여합니다.  
  
```  
CREATE ASYMMETRIC KEY PacificSales19 AUTHORIZATION Christina   
    FROM FILE = 'c:\PacSales\Managers\ChristinaCerts.tmp'    
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="c-creating-an-asymmetric-key-from-an-ekm-provider"></a>3. EKM 공급자에서 비대칭 키 만들기  
 다음 예에서는 파일에 저장된 키 쌍에서 비대칭 키 `EKM_askey1`을 만듭니다. 그런 다음 `EKMProvider1`이라는 확장 가능 키 관리 공급자와 이 공급자의 `key10_user1`이라는 키를 사용하여 해당 키를 암호화합니다.  
  
```  
CREATE ASYMMETRIC KEY EKM_askey1   
    FROM PROVIDER EKM_Provider1  
    WITH   
        ALGORITHM = RSA_2048,   
        CREATION_DISPOSITION = CREATE_NEW  
        , PROVIDER_KEY_NAME  = 'key10_user1' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Azure Key Vault를 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
