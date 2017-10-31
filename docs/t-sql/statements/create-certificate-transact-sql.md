---
title: "인증서 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTIFICATE
- CREATE_CERTIFICATE_TSQL
- sql13.swb.createcertificate.f1
- CERTIFICATE_TSQL
- CREATE CERTIFICATE
- sql13.swb.certificateproperties.f1
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- certificates [SQL Server], adding
- certificates [SQL Server]
- adding certificates
- cryptography [SQL Server], certificates
- CREATE CERTIFICATE statement
ms.assetid: a4274b2b-4cb0-446a-a956-1c8e6587515d
caps.latest.revision: 74
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8753e820278eb04fff6f12e405d766fff5292e58
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-certificate-transact-sql"></a>CREATE CERTIFICATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스에 인증서를 추가합니다.  
  
 이 기능은 Data Tier Application Framework(DACFx)를 사용하는 데이터베이스 내보내기와 호환되지 않습니다. 내보내기 전에 모든 인증서를 삭제해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE CERTIFICATE certificate_name [ AUTHORIZATION user_name ]   
    { FROM <existing_keys> | <generate_new_keys> }  
    [ ACTIVE FOR BEGIN_DIALOG =  { ON | OFF } ]  
  
<existing_keys> ::=   
    ASSEMBLY assembly_name  
    | {   
        [ EXECUTABLE ] FILE = 'path_to_file'  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]   
      }  
    | {   
        BINARY = asn_encoded_certificate  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]  
      }  
<generate_new_keys> ::=   
    [ ENCRYPTION BY PASSWORD = 'password' ]   
    WITH SUBJECT = 'certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<private_key_options> ::=  
      {   
        FILE = 'path_to_private_key'  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
    |  
      {   
        BINARY = private_key_bits  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
  
<date_options> ::=  
    START_DATE = 'datetime' | EXPIRY_DATE = 'datetime'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CERTIFICATE certificate_name   
    { <generate_new_keys> | FROM <existing_keys> }  
    [ ; ]  
  
<generate_new_keys> ::=   
    WITH SUBJECT ='certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<existing_keys> ::=   
    {   
      FILE ='path_to_file'  
      WITH PRIVATE KEY   
         (   
           FILE ='path_to_private_key'  
           , DECRYPTION BY PASSWORD ='password'   
         )  
    }  
  
<date_options> ::=  
    START_DATE ='datetime' | EXPIRY_DATE ='datetime'  
```  
  
## <a name="arguments"></a>인수  
 *certificate_name*  
 데이터베이스의 인증서에 대 한 이름이입니다.  
  
 권한 부여 *user_name*  
 이 인증서를 소유 하는 사용자의 이름이입니다.  
  
 어셈블리 *assembly_name*  
 데이터베이스에 이미 로드된 서명된 어셈블리를 지정합니다.  
  
 [실행 파일] 파일 ='*path_to_file*'  
 인증서를 포함하는 DER 인코딩 파일에 대해 파일 이름을 포함한 전체 경로를 지정합니다. EXECUTABLE 옵션을 사용한 경우 파일은 인증서로 서명된 DLL입니다. *path_to_file* 로컬 경로 또는 UNC 경로를 네트워크 위치 일 수 있습니다. 이 파일은의 보안 컨텍스트에서 액세스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정입니다. 이 계정에는 필요한 파일 시스템 사용 권한이 있어야 합니다.  
  
 WITH PRIVATE KEY  
 인증서의 개인 키가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드되도록 지정합니다. 이 절은 인증서가 파일에서 생성되는 경우에만 유효합니다. 어셈블리의 개인 키를 로드 하려면 사용 하 여 [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md)합니다.  
  
 파일 ='*path_to_private_key*'  
 개인 키에 대해 파일 이름을 포함하여 전체 경로를 지정합니다. *path_to_private_key* 로컬 경로 또는 UNC 경로를 네트워크 위치 일 수 있습니다. 이 파일은의 보안 컨텍스트에서 액세스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정입니다. 이 계정에는 필요한 파일 시스템 사용 권한이 있어야 합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 asn_encoded_certificate  
 ASN으로 인코딩된 인증서 비트로, 이진 상수로 지정됩니다.  
  
 이진 =*private_key_bits*  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 이진 상수로 지정되는 개인 키 비트입니다. 이러한 비트는 암호화된 형식일 수 있습니다. 암호화된 경우 사용자는 해독 암호를 입력해야 합니다. 이 암호에 대해서는 암호 정책 확인이 수행되지 않습니다. 개인 키 비트는 PVK 파일 형식이어야 합니다.  
  
 DECRYPTION BY PASSWORD ='*key_password*'  
 파일에서 검색한 개인 키의 암호를 해독하는 데 필요한 암호를 지정합니다. 개인 키가 Null 암호로 보호되는 경우 이 절은 선택 사항입니다. 암호 보호 없이 개인 키를 파일에 저장하는 것은 권장되지 않습니다. 암호가 필요 하 고 지정 된 암호가 문이 실패 합니다.  
  
 ENCRYPTION BY PASSWORD ='*암호*'  
 개인 키를 암호화 하는 데 사용 되는 암호를 지정 합니다. 암호로 인증서를 암호화하려는 경우에만 이 옵션을 사용합니다. 이 절을 생략 하면 개인 키는 데이터베이스 마스터 키를 사용 하 여 암호화 됩니다. *암호* 의 인스턴스를 실행 하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [Password Policy](../../relational-databases/security/password-policy.md)을 참조하세요.  
  
 제목 ='*certificate_subject_name*'  
 용어 *주체* 는 X.509 표준에 정의 된 대로 인증서의 메타 데이터에서 필드를 참조 합니다. 주체 ं व 64 자 해야 합니다. 사용 되지 않으며이 한도 대 한 적용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] linux. 에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows에서 주체에는 최대 128 자까지 사용할 수 있습니다. 128 자를 초과 하는 제목은 카탈로그에 저장 된 하지만 인증서가 포함 된 binary large object (BLOB)에 전체 제목 이름이 유지 될 때 잘립니다.  
  
 START_DATE ='*datetime*'  
 인증서가 유효하게 되는 날짜입니다. 지정 하지 않으면 START_DATE는 현재 날짜로 설정 되었습니다. START_DATE는 UTC 시간이며 날짜 및 시간으로 변환이 가능한 모든 형식으로 지정할 수 있습니다.  
  
 EXPIRY_DATE ='*datetime*'  
 인증서가 만료되는 날짜입니다. 지정 하지 않으면 EXPIRY_DATE 날짜 전이나 후 1 년에 설정 됩니다. EXPIRY_DATE는 UTC 시간이며 날짜 및 시간으로 변환이 가능한 모든 형식으로 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Service Broker는 만료 날짜를 확인합니다. 그러나 만료 인증서 암호화에 사용 되는 경우에 적용 되지 않습니다.  
  
 ACTIVE FOR BEGIN_DIALOG = { **ON** | OFF}  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 기능의 시작자가 인증서를 사용할 수 있게 합니다. 기본값은 ON입니다.  
  
## <a name="remarks"></a>주의  
 인증서는 X.509 표준을 따르고 X.509 V1 필드를 지원하는 데이터베이스 수준의 보안 개체입니다. CREATE CERTIFICATE는 파일이나 어셈블리로부터 인증서를 로드할 수 있습니다. 이 문은 또한 키 쌍을 생성하고 자체 서명된 인증서를 만들 수 있습니다.  
  
 개인 키는 해야 \<= 2500 바이트 암호화 된 형태로 표시 합니다. 개인 키에 의해 생성 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 1024 비트 통해 긴 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 2048 비트의 길이은 시작 되 고 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다. 외부 원본으로부터 가져온 개인 키의 최소 길이는 384비트이고 최대 길이는 4,096비트입니다. 가져온 개인 키의 길이는 64비트의 정수 배수여야 합니다. TDE에 사용되는 인증서의 개인 키 크기는 3456비트로 제한됩니다.  
  
 인증서의 일련 번호 전체 저장 되지만 첫 16 바이트만 sys.certificates 카탈로그 뷰에 나타납니다.  
  
 인증서의 발급자 필드 전체 저장 되지만 첫 번째 884 바이트는 sys.certificates 카탈로그 뷰.  
  
 개인 키로 지정 된 공개 키와 일치 해야 *certificate_name*합니다.  
  
 컨테이너로부터 인증서를 만들 때 개인 키 로드는 선택 사항입니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 자체 서명된 인증서를 생성할 때 항상 개인 키가 생성됩니다. 기본적으로 개인 키는 데이터베이스 마스터 키를 사용하여 암호화됩니다. 데이터베이스 마스터 키가 없는 경우 지정 된 암호가 문이 실패 합니다.  
  
 개인 키가 데이터베이스 마스터 키로 암호화 된 경우에 ENCRYPTION BY PASSWORD 옵션이 필요 하지 않습니다. 개인 키가 암호로 암호화 하는 경우에이 옵션을 사용 합니다. 지정된 암호가 없으면 인증서의 개인 키가 데이터베이스 마스터 키를 사용하여 암호화됩니다. 데이터베이스의 마스터 키를 열 수 없는 경우이 절을 생략 하면 오류가 발생 합니다.  
  
 데이터베이스 마스터 키를 사용하여 개인 키를 암호화한 경우에는 해독 암호를 지정할 필요가 없습니다.  
  
> [!NOTE]  
>  암호화 및 서명에 대한 기본 제공 함수는 인증서의 만료 날짜를 검사하지 않습니다. 이러한 함수의 사용자는 인증서 만료에 대한 검사 시기를 결정해야 합니다.  
  
 인증서에 대 한 이진 설명을 사용 하 여 만들 수 있습니다는 [CERTENCODED &#40; Transact SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md) 및 [CERTPRIVATEKEY &#40; Transact SQL &#41; ](../../t-sql/functions/certprivatekey-transact-sql.md) 함수입니다. 사용 하는 예제에 대 한 **CERTPRIVATEKEY** 및 **CERTENCODED** 인증서를 다른 데이터베이스로 복사할 항목의 예제 B를 참조 하십시오. [CERTENCODED &#40; Transact SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CREATE CERTIFICATE 권한이 필요합니다. Windows 로그인, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 응용 프로그램 역할만 인증서를 소유할 수 있습니다. 그룹 및 역할은 인증서를 소유할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-self-signed-certificate"></a>1. 자체 서명된 인증서 만들기  
 다음 예에서는 `Shipping04`라는 인증서를 만듭니다. 이 인증서의 개인 키는 암호를 사용하여 보호됩니다.  
  
```  
CREATE CERTIFICATE Shipping04   
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
   WITH SUBJECT = 'Sammamish Shipping Records',   
   EXPIRY_DATE = '20201031';  
GO  
```  
  
### <a name="b-creating-a-certificate-from-a-file"></a>2. 파일로부터 인증서 만들기  
 다음 예에서는 데이터베이스에서 인증서를 만들고 파일로부터 키 쌍을 로드합니다.  
  
```  
CREATE CERTIFICATE Shipping11   
    FROM FILE = 'c:\Shipping\Certs\Shipping11.cer'   
    WITH PRIVATE KEY (FILE = 'c:\Shipping\Certs\Shipping11.pvk',   
    DECRYPTION BY PASSWORD = 'sldkflk34et6gs%53#v00');  
GO   
```  
  
### <a name="c-creating-a-certificate-from-a-signed-executable-file"></a>3. 서명된 실행 파일로부터 인증서 만들기  
  
```  
CREATE CERTIFICATE Shipping19   
    FROM EXECUTABLE FILE = 'c:\Shipping\Certs\Shipping19.dll';  
GO  
```  
  
 또는 `dll` 파일로부터 어셈블리를 만든 다음 어셈블리로부터 인증서를 만들 수 있습니다.  
  
```  
CREATE ASSEMBLY Shipping19   
    FROM ' c:\Shipping\Certs\Shipping19.dll'   
    WITH PERMISSION_SET = SAFE;  
GO  
CREATE CERTIFICATE Shipping19 FROM ASSEMBLY Shipping19;  
GO  
```  
  
### <a name="d-creating-a-self-signed-certificate"></a>4. 자체 서명된 인증서 만들기  
 다음 예에서는 라는 인증서를 만듭니다. `Shipping04` 는 암호화 된 암호를 지정 하지 않고 있습니다. 이 예에서는 사용할 수 있습니다 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.
  
```  
CREATE CERTIFICATE Shipping04   
   WITH SUBJECT = 'Sammamish Shipping Records';  
GO  
```  
  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER CERTIFICATE &#40; Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP certificate&#40; Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [CERTENCODED &#40; Transact SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md)   
 [CERTPRIVATEKEY &#40; Transact SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
  
  



