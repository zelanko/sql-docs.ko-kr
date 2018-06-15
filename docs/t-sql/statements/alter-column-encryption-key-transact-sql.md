---
title: ALTER COLUMN ENCRYPTION KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER COLUMN ENCRYPTION
- ALTER_COLUMN_ENCRYPTION_TSQL
- ALTER COLUMN ENCRYPTION KEY
- ALTER_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column encryption key, alter
- ALTER COLUMN ENCRYPTION KEY statement
ms.assetid: c79a220d-e178-4091-a330-c924cc0f0ae0
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 36340940aa563838fe3552d3ef9e43c925655e7d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064190"
---
# <a name="alter-column-encryption-key-transact-sql"></a>ALTER COLUMN ENCRYPTION KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  암호화 값을 추가 또는 삭제해 데이터베이스의 열 암호화 키를 수정합니다. CEK는 해당 열 마스터 키의 회전을 허용하는 값을 최대 2개까지 가질 수 있습니다. CEK는 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능을 사용하여 열을 암호화할 때 사용합니다. CEK 값을 추가하기 전에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 사용하여 값을 암호화하는 데 사용된 열 마스터 키를 정의해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER COLUMN ENCRYPTION KEY key_name   
    [ ADD | DROP ] VALUE   
    (  
        COLUMN_MASTER_KEY = column_master_key_name   
        [, ALGORITHM = 'algorithm_name' , ENCRYPTED_VALUE =  varbinary_literal ]   
    ) [;]  
```  
  
## <a name="arguments"></a>인수  
 *key_name*  
 변경하고 있는 열 암호화 마스터 키입니다.  
  
 *column_master_key_name*  
 열 암호화 키(CEK)를 암호화하는 데 사용되는 열 마스터 키(CMK)의 이름을 지정합니다.  
  
 *algorithm_name*  
 값을 암호화하는 데 사용되는 암호화 알고리즘의 이름입니다. 시스템 공급자에 대한 알고리즘은 **RSA_OAEP**이어야 합니다. 이 인수는 열 암호화 키 값을 삭제할 때에는 유효하지 않습니다.  
  
 *varbinary_literal*  
 지정된 마스터 암호화 키로 암호화된 CEK BLOB입니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다. 이 인수는 열 암호화 키 값을 삭제할 때에는 유효하지 않습니다.  
  
> [!WARNING]  
>  이 문의 일반 텍스트 CEK 값은 절대 전달하지 마십시오. 그럴 경우 이 기능의 이점을 구성하게 됩니다.  
  
## <a name="remarks"></a>Remarks  
 일반적으로 열 암호화 키는 단 하나의 암호화된 값으로 만들어집니다. 열 마스터 키가 회전할 필요가 있는 경우(지금의 열 마스터 키는 새 열 마스터 키로 교체해야 합니다) 새 열 마스터 키로 암호화된 열 암호화 키의 새 값을 추가할 수 있습니다. 이렇게 하면 클라이언트 응용 프로그램이 열 암호화 키로 암호화된 데이터에 액세스할 수 있게 하는 동시에 새 열 마스터 키가 클라이언트 응용 프로그램에 사용할 수 있게 됩니다. 새 마스터 키에 액세스 권한이 없는 클라이언트 응용 프로그램에서 Always Encrypted 기반 드라이버는 민감한 데이터에 액세스하기 위해 이전 열 마스터 키로 암호화된 열 암호화 키 값을 사용할 수 있습니다. Always Encrypted 지원 암호화 알고리즘은 256비트를 가진 일반 텍스트 값을 요구합니다. 암호화된 값은 열 마스터 키를 보유한 키 저장소를 캡슐화하는 키 저장소 공급자를 사용하여 생성돼야 합니다.  
  
 열 암호화 키에 대한 정보를 보려면 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md), [sys.column_encryption_keys&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md), [sys.column_encryption_key_values&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)를 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 **ALTER ANY COLUMN ENCRYPTION KEY** 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-adding-a-column-encryption-key-value"></a>1. 열 암호화 키 값 추가  
 다음 예에서는 `MyCEK`이라고 하는 열 암호화 키를 수정합니다.  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
ADD VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK2,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E00740075007300650072002F006D0079002F0064006500650063006200660034006100340031003000380034006200350033003200360066003200630062006200350030003600380065003900620061003000320030003600610037003800310066001DDA6134C3B73A90D349C8905782DD819B428162CF5B051639BA46EC69A7C8C8F81591A92C395711493B25DCBCCC57836E5B9F17A0713E840721D098F3F8E023ABCDFE2F6D8CC4339FC8F88630ED9EBADA5CA8EEAFA84164C1095B12AE161EABC1DF778C07F07D413AF1ED900F578FC00894BEE705EAC60F4A5090BBE09885D2EFE1C915F7B4C581D9CE3FDAB78ACF4829F85752E9FC985DEB8773889EE4A1945BD554724803A6F5DC0A2CD5EFE001ABED8D61E8449E4FAA9E4DD392DA8D292ECC6EB149E843E395CDE0F98D04940A28C4B05F747149B34A0BAEC04FFF3E304C84AF1FF81225E615B5F94E334378A0A888EF88F4E79F66CB377E3C21964AACB5049C08435FE84EEEF39D20A665C17E04898914A85B3DE23D56575EBC682D154F4F15C37723E04974DB370180A9A579BC84F6BC9B5E7C223E5CBEE721E57EE07EFDCC0A3257BBEBF9ADFFB00DBF7EF682EC1C4C47451438F90B4CF8DA709940F72CFDC91C6EB4E37B4ED7E2385B1FF71B28A1D2669FBEB18EA89F9D391D2FDDEA0ED362E6A591AC64EF4AE31CA8766C259ECB77D01A7F5C36B8418F91C1BEADDD4491C80F0016B66421B4B788C55127135DA2FA625FB7FD195FB40D90A6C67328602ECAF3EC4F5894BFD84A99EB4753BE0D22E0D4DE6A0ADFEDC80EB1B556749B4A8AD00E73B329C95827AB91C0256347E85E3C5FD6726D0E1FE82C925D3DF4A9  
);  
GO  
  
```  
  
### <a name="b-dropping-a-column-encryption-key-value"></a>2. 열 암호화 키 값 삭제  
 다음 예에서는 값을 삭제하여 `MyCEK`이라고 하는 열 암호화 키를 수정합니다.  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
DROP VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK  
);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_keys&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_encryption_key_values&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
