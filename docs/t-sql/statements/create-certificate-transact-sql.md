---
description: CREATE CERTIFICATE(Transact-SQL)
title: CREATE CERTIFICATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3d4799b962fd1c8b6084443f5d83fa171fe4b0a1
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124132"
---
# <a name="create-certificate-transact-sql"></a>CREATE CERTIFICATE(Transact-SQL)
[!INCLUDE [sql-asdb-asa-pdw](../../includes/applies-to-version/sql-asdb-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스에 인증서를 추가합니다.  

 이 기능은 Data Tier Application Framework(DACFx)를 사용하는 데이터베이스 내보내기와 호환되지 않습니다. 내보내기 전에 모든 인증서를 삭제해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE CERTIFICATE certificate_name [ AUTHORIZATION user_name ]   
    { FROM <existing_keys> | <generate_new_keys> }  
    [ ACTIVE FOR BEGIN_DIALOG = { ON | OFF } ]  
  
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
  
> [!Note]
> [!INCLUDE [Synapse preview note](../../includes/synapse-preview-note.md)]
   
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
CREATE CERTIFICATE certificate_name   
    { <generate_new_keys> | FROM <existing_keys> }  
    [ ; ]  
  
<generate_new_keys> ::=   
    WITH SUBJECT = 'certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<existing_keys> ::=   
    {   
      FILE ='path_to_file'  
      WITH PRIVATE KEY   
         (   
           FILE = 'path_to_private_key'  
           , DECRYPTION BY PASSWORD ='password'   
         )  
    }  
  
<date_options> ::=  
    START_DATE ='datetime' | EXPIRY_DATE ='datetime'  
```  
[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *certificate_name*  
 데이터베이스에 있는 인증서에 대한 이름입니다.  
  
 AUTHORIZATION *user_name*  
 이 인증서를 소유하게 될 사용자의 이름입니다.  
  
 ASSEMBLY *assembly_name*  
 데이터베이스에 이미 로드된 서명된 어셈블리를 지정합니다.  
  
 [ EXECUTABLE ] FILE = '*path_to_file*'  
 인증서를 포함하는 DER 인코딩 파일에 대해 파일 이름을 포함한 전체 경로를 지정합니다. EXECUTABLE 옵션을 사용한 경우 파일은 인증서로 서명된 DLL입니다. *path_to_file* 은 로컬 경로 또는 네트워크 위치에 대한 UNC 경로일 수 있습니다. 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트에서 액세스됩니다. 이 계정에는 필요한 파일 시스템 사용 권한이 있어야 합니다.  

> [!IMPORTANT]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 파일에서 인증서 생성 또는 프라이빗 키 파일 사용을 지원하지 않습니다.
  
 BINARY = *asn_encoded_certificate*  
 이진 상수로 지정된 ASN 인코딩 인증서 바이트.  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상  
  
 WITH PRIVATE KEY  
 인증서의 프라이빗 키가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드되도록 지정합니다. 이 절은 어셈블리에서 인증서를 만들 때 유효하지 않습니다. 어셈블리에서 생성된 인증서의 프라이빗 키를 로드하려면 [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md)를 사용합니다.  
  
 FILE ='*path_to_private_key*'  
 프라이빗 키에 대해 파일 이름을 포함하여 전체 경로를 지정합니다. *path_to_private_key* 는 로컬 경로 또는 네트워크 위치에 대한 UNC 경로일 수 있습니다. 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정의 보안 컨텍스트에서 액세스됩니다. 이 계정에는 필요한 파일 시스템 사용 권한이 있어야 합니다.  
  
> [!IMPORTANT]  
> 포함된 데이터베이스 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서는 이 옵션을 사용할 수 없습니다.  
  
 BINARY = *private_key_bits*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 이진 상수로 지정되는 프라이빗 키 비트입니다. 이러한 비트는 암호화된 형식일 수 있습니다. 암호화된 경우 사용자는 해독 암호를 입력해야 합니다. 이 암호에 대해서는 암호 정책 확인이 수행되지 않습니다. 프라이빗 키 비트는 PVK 파일 형식이어야 합니다.  
  
 DECRYPTION BY PASSWORD = '*key_password*'  
 파일에서 검색한 프라이빗 키의 암호를 해독하는 데 필요한 암호를 지정합니다. 프라이빗 키가 Null 암호로 보호되는 경우 이 절은 선택 사항입니다. 암호 보호 없이 프라이빗 키를 파일에 저장하는 것은 권장되지 않습니다. 암호가 필요하지만 지정된 암호가 없으면 문이 실패합니다.  
  
 ENCRYPTION BY PASSWORD = '*password*'  
 프라이빗 키를 암호화하는 데 사용할 암호를 지정합니다. 암호로 인증서를 암호화하려는 경우에만 이 옵션을 사용합니다. 이 절을 생략하면 프라이빗 키가 데이터베이스 마스터 키로 암호화됩니다. *password* 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다. 자세한 내용은 [Password Policy](../../relational-databases/security/password-policy.md)을 참조하세요.  
  
 SUBJECT = '*certificate_subject_name*'  
 *제목* 이란 단어는 X.509 표준에 정의된 것과 같이 인증서의 메타데이터에 있는 필드를 나타냅니다. 제목은 64자를 초과할 수 없으며 이 제한은 Linux에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 적용됩니다. Windows에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 제목은 최대 128자까지 지정할 수 있습니다. 128자를 초과하는 제목은 카탈로그에 저장될 때 잘리지만 인증서가 포함된 BLOB(Binary Large Object)에는 전체 제목 이름이 포함됩니다.  
  
 START_DATE = '*datetime*'  
 인증서가 유효하게 되는 날짜입니다. 지정하지 않으면 START_DATE가 현재 날짜와 같게 설정됩니다. START_DATE는 UTC 시간이며 날짜 및 시간으로 변환이 가능한 모든 형식으로 지정할 수 있습니다.  
  
 EXPIRY_DATE = '*datetime*'  
 인증서가 만료되는 날짜입니다. 지정하지 않으면 EXPIRY_DATE가 START_DATE의 일년 후 날짜로 설정됩니다. EXPIRY_DATE는 UTC 시간이며 날짜 및 시간으로 변환이 가능한 모든 형식으로 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker는 만료 날짜를 확인하지만 인증서를 사용하는 암호화를 통한 백업도 만료 날짜를 확인하며 만료된 인증서로 새로운 백업 생성을 허용하지 않지만 만료된 인증서로 복원은 허용합니다. 인증서가 데이터베이스 암호화 또는 Always Encrypted에 사용되는 경우에는 만료되지 않습니다.  
  
 ACTIVE FOR BEGIN_DIALOG = { **ON** | OFF }  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 기능의 시작자가 인증서를 사용할 수 있게 합니다. 기본값은 ON입니다.  
  
## <a name="remarks"></a>설명  
 인증서는 X.509 표준을 따르고 X.509 V1 필드를 지원하는 데이터베이스 수준의 보안 개체입니다. `CREATE CERTIFICATE`는 파일, 이진 상수 또는 어셈블리에서 인증서를 로드할 수 있습니다. 이 문은 또한 키 쌍을 생성하고 자체 서명된 인증서를 만들 수 있습니다.  
  
 프라이빗 키는 암호화된 형식으로 \< = 2500 바이트여야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 생성된 프라이빗 키는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 1024 비트 길이이고 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]으로 시작하는 2048 비트 길이입니다. 외부 원본으로부터 가져온 프라이빗 키의 최소 길이는 384비트이고 최대 길이는 4,096비트입니다. 가져온 프라이빗 키의 길이는 64비트의 정수 배수여야 합니다. TDE에 사용되는 인증서의 프라이빗 키 크기는 3456비트로 제한됩니다.  
  
 인증서의 전체 일련 번호가 저장되지만 처음 16 바이트만 sys.certificates 카탈로그 뷰에 나타납니다.  
  
 인증서의 전체 발급자 필드가 저장되지만 sys.certificates 카탈로그 뷰의 처음 884 바이트만 저장됩니다.  
  
 프라이빗 키는 *certificate_name* 으로 지정한 퍼블릭 키와 일치해야 합니다.  
  
 컨테이너로부터 인증서를 만들 때 프라이빗 키 로드는 선택 사항입니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 자체 서명된 인증서를 생성할 때 항상 프라이빗 키가 생성됩니다. 기본적으로 프라이빗 키는 데이터베이스 마스터 키를 사용하여 암호화됩니다. 데이터베이스 마스터 키가 없고 지정된 암호가 없으면 문이 실패합니다.  
  
 `ENCRYPTION BY PASSWORD` 옵션은 프라이빗 키가 데이터베이스 마스터 키로 암호화된 경우 필요하지 않습니다. 이 옵션은 프라이빗 키가 암호로 암호화되는 경우에만 사용합니다. 지정된 암호가 없으면 인증서의 프라이빗 키가 데이터베이스 마스터 키를 사용하여 암호화됩니다. 데이터베이스 마스터 키를 열 수 없는 경우 이 절을 생략하면 오류가 발생합니다.  
  
 데이터베이스 마스터 키를 사용하여 프라이빗 키를 암호화한 경우에는 해독 암호를 지정할 필요가 없습니다.  
  
> [!NOTE]  
> 암호화 및 서명에 대한 기본 제공 함수는 인증서의 만료 날짜를 검사하지 않습니다. 이러한 함수의 사용자는 인증서 만료에 대한 검사 시기를 결정해야 합니다.  
  
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md) 및 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md) 함수를 사용하여 인증서의 이진 설명을 만들 수 있습니다. **CERTPRIVATEKEY** 및 **CERTENCODED** 를 사용하여 다른 데이터베이스로 인증서를 복사하는 예는 [CERTENCODED &#40;Transact-SQL&amp;amp;#41](../../t-sql/functions/certencoded-transact-sql.md) 문서의 예제 B를 참조하세요.  

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서는 MD2, MD4, MD5, SHA 및 SHA1 알고리즘이 사용되지 않습니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]까지는 자체 서명된 인증서가 SHA1을 사용하여 생성됩니다. [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터는 자체 서명된 인증서가 SHA2_256을 사용하여 생성됩니다.

## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 `CREATE CERTIFICATE` 권한이 필요합니다. Windows 로그인, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 애플리케이션 역할만 인증서를 소유할 수 있습니다. 그룹 및 역할은 인증서를 소유할 수 없습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-a-self-signed-certificate"></a>A. 자체 서명된 인증서 만들기  
 다음 예에서는 `Shipping04`라는 인증서를 만듭니다. 이 인증서의 프라이빗 키는 암호를 사용하여 보호됩니다.  
  
```sql  
CREATE CERTIFICATE Shipping04   
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
   WITH SUBJECT = 'Sammamish Shipping Records',   
   EXPIRY_DATE = '20201031';  
GO  
```  
  
### <a name="b-creating-a-certificate-from-a-file"></a>B. 파일로부터 인증서 만들기  
 다음 예에서는 데이터베이스에서 인증서를 만들고 파일로부터 키 쌍을 로드합니다.  
  
```sql  
CREATE CERTIFICATE Shipping11   
    FROM FILE = 'c:\Shipping\Certs\Shipping11.cer'   
    WITH PRIVATE KEY (FILE = 'c:\Shipping\Certs\Shipping11.pvk',   
    DECRYPTION BY PASSWORD = 'sldkflk34et6gs%53#v00');  
GO   
```  

> [!IMPORTANT]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 파일로부터 인증서 만들기를 지원하지 않습니다.
   
### <a name="c-creating-a-certificate-from-a-signed-executable-file"></a>C. 서명된 실행 파일로부터 인증서 만들기  
  
```sql  
CREATE CERTIFICATE Shipping19   
    FROM EXECUTABLE FILE = 'c:\Shipping\Certs\Shipping19.dll';  
GO  
```  
  
 또는 `dll` 파일로부터 어셈블리를 만든 다음 어셈블리로부터 인증서를 만들 수 있습니다.  
  
```sql  
CREATE ASSEMBLY Shipping19   
    FROM ' c:\Shipping\Certs\Shipping19.dll'   
    WITH PERMISSION_SET = SAFE;  
GO  
CREATE CERTIFICATE Shipping19 FROM ASSEMBLY Shipping19;  
GO  
```  

> [!IMPORTANT]
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 파일로부터 인증서 만들기를 지원하지 않습니다.

> [!IMPORTANT]
> [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 [‘CLR 엄격한 보안’](../../database-engine/configure-windows/clr-strict-security.md) 서버 구성 옵션이 제공되어, 먼저 보안을 설정하지 않으면 어셈블리를 로드할 수 없습니다. 인증서를 로드하고, 인증서를 만들고, 해당 로그인에 `UNSAFE ASSEMBLY`를 부여한 다음, 어셈블리를 로드합니다.

### <a name="d-creating-a-self-signed-certificate"></a>D. 자체 서명된 인증서 만들기  
 다음 예에서는 암호화된 암호를 지정하지 않고 `Shipping04`라는 인증서를 만듭니다. 이 예제는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]와 함께 사용할 수 있습니다.
  
```sql  
CREATE CERTIFICATE Shipping04   
   WITH SUBJECT = 'Sammamish Shipping Records';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)   
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  


