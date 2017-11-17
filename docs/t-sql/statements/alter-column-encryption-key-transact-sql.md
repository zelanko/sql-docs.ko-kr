---
title: ALTER COLUMN ENCRYPTION KEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/28/2015
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
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6aaa1f85f860272cdb672d29bccdda39380f728a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-column-encryption-key-transact-sql"></a>ALTER COLUMN ENCRYPTION KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  데이터베이스를 추가 또는 삭제 된 암호화 된 값에서 열 암호화 키를 변경 합니다. CEK는 해당 열 마스터 키 회전을 허용 하는 최대 12 개의 값을 가질 수 있습니다. CEK는 사용 하 여 열을 암호화할 때 사용 되는 [상시 암호화 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 기능입니다. CEK 값을 추가 하기 전에 사용 하 여 값을 암호화 하는 데 사용 된 열 마스터 키 정의 해야 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) 문.  
  
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
 변경 중인 열 암호화 키입니다.  
  
 *column_master_key_name*  
 열 암호화 키 (CEK)를 암호화 하는 데 사용 되는 열 마스터 키 (CMK)의 이름을 지정 합니다.  
  
 *algorithm_name*  
 값을 암호화 하는 데 사용 된 암호화 알고리즘의 이름입니다. 시스템 공급자에 대 한 알고리즘 해야 **RSA_OAEP**합니다. 열 암호화 키 값을 삭제 하는 경우이 인수가 올바르지 않습니다.  
  
 *varbinary_literal*  
 CEK BLOB로 암호화 되며 지정 된 마스터 암호화 키. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다. 열 암호화 키 값을 삭제 하는 경우이 인수가 올바르지 않습니다.  
  
> [!WARNING]  
>  전달 하면 일반 텍스트 CEK 값이 문에서 합니다. 이렇게 하면이 기능의 이점 구성 하는 합니다.  
  
## <a name="remarks"></a>주의  
 일반적으로 열 암호화 키를 암호화 된 값이 하나만 만들어집니다. (현재 열 마스터 키 요구 새 열 마스터 키로 교체) 회전할 수, 열 암호화 키의 새 값을 추가할 수 있습니다 열 마스터 키가 필요한 경우 새 열 마스터 키로 암호화 합니다. 이렇게 하면 클라이언트 응용 프로그램이 새 열 마스터 키 이루어지고 클라이언트 응용 프로그램에 제공 하는 동안 열 암호화 키로 암호화 된 데이터에 액세스할 수 있습니다. 상시 암호화 드라이버 새 마스터 키에 액세스할 필요는 없으며, 이전 열 마스터 키로 암호화 된 열 암호화 키 값을 사용 하 여 중요 한 데이터 액세스 할 수 있습니다 하는 클라이언트 응용 프로그램에서 사용할 수 있습니다. 암호화 알고리즘, 상시 암호화 지원 256 비트를 일반 텍스트 값이 필요 합니다. 열 마스터 키를 보유 하 고 키 저장소를 캡슐화 하는 키 저장소 공급자를 사용 하 여 암호화 된 값을 생성 합니다.  
  
 사용 하 여 [sys.columns&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md), [sys.column_encryption_keys&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) 및 [sys.column_encryption_key_values&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) 열 암호화 키에 대 한 정보를 볼 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 필요한 **ALTER ANY COLUMN ENCRYPTION KEY** 데이터베이스에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-adding-a-column-encryption-key-value"></a>1. 열 암호화 키 값을 추가합니다.  
 다음 예에서는 라는 열 암호화 키 변경 `MyCEK`합니다.  
  
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
  
### <a name="b-dropping-a-column-encryption-key-value"></a>2. 열 암호화 키 값을 삭제 하는 중  
 다음 예에서는 라는 열 암호화 키 변경 `MyCEK` 값을 삭제 하 여 합니다.  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
DROP VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK  
);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION key&#40; Transact SQL &#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_keys&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_encryption_key_values&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  

