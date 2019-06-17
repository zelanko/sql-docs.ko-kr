---
title: CREATE SYMMETRIC KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE SYMMETRIC KEY
- SYMMETRIC KEP
- CREATE_SYMMETRIC_KEY_TSQL
- SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SYMMETRIC KEY statement
- temporary symmetric keys [SQL Server]
- symmetric keys [SQL Server], creating
- symmetric keys [SQL Server]
ms.assetid: b5d23572-b79d-4cf1-9eef-d648fa3b1358
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 56be2b8913002d681a4478eff80448acd2e71089
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66836345"
---
# <a name="create-symmetric-key-transact-sql"></a>CREATE SYMMETRIC KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 대칭 키를 생성하고 해당 속성을 지정합니다.  
  
 이 기능은 Data Tier Application Framework(DACFx)를 사용하는 데이터베이스 내보내기와 호환되지 않습니다. 내보내기 전에 모든 대칭 키를 삭제해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE SYMMETRIC KEY key_name   
    [ AUTHORIZATION owner_name ]  
    [ FROM PROVIDER provider_name ]  
    WITH 
      [
          <key_options> [ , ... n ]  
        | ENCRYPTION BY <encrypting_mechanism> [ , ... n ] 
      ]
  
<key_options> ::=  
      KEY_SOURCE = 'pass_phrase'  
    | ALGORITHM = <algorithm>  
    | IDENTITY_VALUE = 'identity_phrase'  
    | PROVIDER_KEY_NAME = 'key_name_in_provider'   
    | CREATION_DISPOSITION = {CREATE_NEW | OPEN_EXISTING }  
  
<algorithm> ::=  
    DES | TRIPLE_DES | TRIPLE_DES_3KEY | RC2 | RC4 | RC4_128  
    | DESX | AES_128 | AES_192 | AES_256   
  
<encrypting_mechanism> ::=  
      CERTIFICATE certificate_name   
    | PASSWORD = 'password'   
    | SYMMETRIC KEY symmetric_key_name   
    | ASYMMETRIC KEY asym_key_name  
```  
  
## <a name="arguments"></a>인수  
 *Key_name*  
 데이터베이스에서 대칭 키를 식별하는 고유한 이름을 지정합니다. _key_name_이 하나의 숫자(#) 기호로 시작하면 임시 키가 지정됩니다. 예를 들면 **#temporaryKey900007**과 같습니다. 2개 이상의 #으로 시작하는 이름이 포함된 대칭 키는 만들 수 없습니다. 임시 대칭 키는 EKM 공급자를 사용하여 만들 수 없습니다.  
  
 AUTHORIZATION *owner_name*  
 이 키를 소유하는 데이터베이스 사용자 또는 응용 프로그램 역할의 이름을 지정합니다.  
  
 FROM PROVIDER *provider_name*  
 EKM(확장 가능 키 관리) 공급자와 이름을 지정합니다. 키는 EKM 장치에서 내보내지 않았습니다. 먼저 CREATE PROVIDER 문을 사용하여 공급자를 정의해야 합니다. 외부 키 공급자 만들기에 대한 자세한 내용은 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)을 참조하세요.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 KEY_SOURCE **='** _pass\_phrase_ **'**  
 키를 파생할 전달 구를 지정합니다.  
  
 IDENTITY_VALUE **='** _identity\_phrase_ **'**  
 임시 키로 암호화된 데이터 분류용 GUID를 생성할 ID 구를 지정합니다.  
  
 PROVIDER_KEY_NAME **='** _key\_name\_in\_provider_ **'**  
 EKM(확장 가능 키 관리) 공급자에서 참조되는 이름을 지정합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 CREATION_DISPOSITION **=** CREATE_NEW  
 확장 가능 키 관리 장치에 새 키를 만듭니다.  키가 이미 장치에 있는 경우 문이 오류와 함께 실패합니다.  
  
 CREATION_DISPOSITION **=** OPEN_EXISTING  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대칭 키를 기존 EKM(확장 가능 키 관리) 키에 매핑합니다. CREATION_DISPOSITION = OPEN_EXISTING을 지정하지 않으면 기본값은 CREATE_NEW입니다.  
  
 *certificate_name*  
 대칭 키를 암호화하는 데 사용되는 인증서 이름을 지정합니다. 인증서는 데이터베이스에 이미 있어야 합니다.  
  
 **'** *password* **'**  
 대칭 키의 보안을 유지할 수 있는 TRIPLE_DES 키를 파생할 암호를 지정합니다. *password*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다. 항상 강력한 암호를 사용합니다.  
  
 *symmetric_key_name*  
 만들려는 키를 암호화하는 데 사용되는 대칭 키를 지정합니다. 지정된 키는 데이터베이스에 이미 있어야 하며 열려 있어야 합니다.  
  
 *asym_key_name*  
 만들려는 키를 암호화하는 데 사용되는 비대칭 키를 지정합니다. 이 비대칭 키는 데이터베이스에 이미 있어야 합니다.  
  
 \<algorithm>  
암호화 알고리즘을 지정하십시오.   
> [!WARNING]  
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 AES_128, AES_192 및 AES_256 이외의 모든 알고리즘을 지원하지 않습니다. 오래된 알고리즘을 사용하려면(권장하지 않음) 데이터베이스 간 호환성 수준을 120 이하로 설정해야 합니다.  
  
## <a name="remarks"></a>Remarks  
 대칭 키를 만들 때 대칭 키는 인증서, 암호, 대칭 키, 비대칭 키 또는 PROVIDER 중 하나 이상을 사용하여 암호화해야 합니다. 키에는 각 유형에 대해 두 개 이상의 암호화가 포함될 수 있습니다. 즉, 여러 인증서, 암호, 대칭 키 및 비대칭 키를 동시에 사용하여 단일 대칭 키를 암호화할 수 있습니다.  
  
> [!CAUTION]  
>  대칭 키가 인증서(또는 다른 키) 대신에 암호로 암호화된 경우 암호를 암호화하는 데 TRIPLE DES 암호화 알고리즘이 사용됩니다. 따라서 AES와 같은 강력한 암호화 알고리즘을 사용하여 만든 키는 더 약한 알고리즘으로 보호됩니다.  
  
 키를 여러 사용자에게 배포하기 전에 선택적인 암호를 사용하여 대칭 키를 암호화할 수 있습니다.  
  
 임시 키는 키를 만드는 사용자가 소유합니다. 임시 키는 현재 세션에 대해서만 유효합니다.  
  
 IDENTITY_VALUE는 새 대칭 키로 암호화된 데이터를 분류하는 GUID를 생성합니다. 이 분류는 암호화된 데이터와 키를 일치시키는 데 사용됩니다. 특정 구에서 생성된 GUID는 항상 동일합니다. GUID를 생성하는 데 사용한 구는 현재 해당 구를 사용하는 세션이 하나 이상 있는 한 다시 사용할 수 없습니다. IDENTITY_VALUE는 선택적인 절이지만 임시 키로 암호화된 데이터를 저장할 때는 이 절을 사용하는 것이 좋습니다.  
  
 기본 암호화 알고리즘은 없습니다.  
  
> [!IMPORTANT]  
>  중요한 데이터를 보호할 때는 RC4 및 RC4_128 스트림 암호를 사용하지 않는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이러한 키로 수행된 암호화를 더 이상 인코딩하지 않습니다.  
  
 대칭 키에 대한 정보는 [sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 대칭 키는 암호화 공급자에서 만든 대칭 키로 암호화할 수 없습니다.  
  
 **DES 알고리즘 관련 설명:**  
  
-   DESX 이름이 잘못 지정되었습니다. ALGORITHM = DESX를 사용하여 만든 대칭 키에 실제로 192비트 키를 포함하는 TRIPLE DES 암호화가 사용됩니다. DESX 알고리즘은 제공되지 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
-   ALGORITHM = TRIPLE_DES_3KEY를 사용하여 만든 대칭 키에 192비트 키를 포함하는 TRIPLE DES가 사용됩니다.  
-   ALGORITHM = TRIPLE_DES를 사용하여 만든 대칭 키에 128비트 키를 포함하는 TRIPLE DES가 사용됩니다.  
  
 **RC4 알고리즘의 사용 중단:**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 솔트를 자동으로 제공하지 않기 때문에 서로 다른 데이터 블록에서 동일한 RC4 또는 RC4_128 KEY_GUID를 반복해서 사용하면 동일한 RC4 키가 만들어집니다. 동일한 RC4 키를 반복해서 사용하는 것은 암호화를 매우 약하게 만드는 잘 알려진 오류입니다. 따라서 RC4 및 RC4_128 키워드는 더 이상 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
> [!WARNING]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER ANY SYMMETRIC KEY 권한이 필요합니다. AUTHORIZATION이 지정된 경우 데이터베이스 사용자에 대한 IMPERSONATE 권한 또는 애플리케이션 역할에 대한 ALTER 권한이 필요합니다. 인증서 또는 비대칭 키를 통한 암호화의 경우에는 해당 인증서 또는 비대칭 키에 대한 VIEW DEFINITION 권한이 필요합니다. Windows 로그인, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 애플리케이션 역할만 대칭 키를 소유할 수 있습니다. 그룹 및 역할은 대칭 키를 소유할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-symmetric-key"></a>1\. 대칭 키 만들기  
 다음 예에서는 `JanainaKey09` 알고리즘을 사용하여 `AES 256`라는 대칭 키를 만든 다음 새 키를 `Shipping04` 인증서를 사용하여 암호화합니다.  
  
```  
CREATE SYMMETRIC KEY JanainaKey09   
WITH ALGORITHM = AES_256  
ENCRYPTION BY CERTIFICATE Shipping04;  
GO  
```  
  
### <a name="b-creating-a-temporary-symmetric-key"></a>2\. 임시 대칭 키 만들기  
 다음 예에서는 `#MarketingXXV`라는 임시 대칭 키를 `The square of the hypotenuse is equal to the sum of the squares of the sides` 전달 구에서 만듭니다. 이 키는 `Pythagoras` 문자열에서 생성되고 `Marketing25` 인증서로 암호화된 GUID와 함께 제공됩니다.  
  
```  
  
CREATE SYMMETRIC KEY #MarketingXXV   
WITH ALGORITHM = AES_128,  
KEY_SOURCE   
     = 'The square of the hypotenuse is equal to the sum of the squares of the sides',  
IDENTITY_VALUE = 'Pythagoras'  
ENCRYPTION BY CERTIFICATE Marketing25;  
GO  
```  
  
### <a name="c-creating-a-symmetric-key-using-an-extensible-key-management-ekm-device"></a>C. EKM(확장 가능 키 관리) 장치를 사용하여 대칭 키 만들기  
 다음 예에서는 `MySymKey`라는 공급자와 `MyEKMProvider`의 키 이름을 사용하여 `KeyForSensitiveData`라는 대칭 키를 만듭니다. `User1`에 인증을 할당하고 시스템 관리자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 `MyEKMProvider`라는 공급자를 이미 등록했다고 가정합니다.  
  
```  
CREATE SYMMETRIC KEY MySymKey  
AUTHORIZATION User1  
FROM PROVIDER EKMProvider  
WITH  
PROVIDER_KEY_NAME='KeyForSensitiveData',  
CREATION_DISPOSITION=OPEN_EXISTING;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Azure Key Vault를 사용한 확장 가능 키 관리&#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
