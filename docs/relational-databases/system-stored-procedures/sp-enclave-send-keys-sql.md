---
title: sp_enclave_send_keys (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enclave_send_keys
- sp_enclave_send_keys_TSQL
- sys.sp_enclave_send_keys
- sys.sp_enclave_send_keys_TSQL
helpviewer_keywords:
- sp_enclave_send_keys
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6540cdd36cccba4f5a7ccb3beddf31ce00cd9107
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394145"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

보낼 모든 enclave 사용 열 암호화 키 데이터베이스에서 사용한 enclave [enclaves 보안을 사용 하 여 상시 암호화 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)합니다.

## <a name="syntax"></a>구문  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>인수

이 저장된 프로시저에 인수가 없습니다.

## <a name="return-value"></a>반환 값

이 저장된 프로시저에 반환 값이 없습니다.
  
## <a name="result-sets"></a>결과 집합

이 저장된 프로시저에 결과 집합이 없습니다.
  
## <a name="remarks"></a>Remarks

**sp_enclave_send_keys** 다음 조건이 모두 충족 되 면 enclave 사용 열 암호화 키가 enclave를 보냅니다.

- Enclave는 SQL Server 인스턴스에 사용 됩니다.
- **sp_enclave_send_keys** 사용 하 여 응용 프로그램에서 호출 된를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] client 드라이버를 사용 하도록 설정 하는 Always Encrypted와 enclave 계산에는 데이터베이스 연결을 사용 하 여 보안 enclaves를 사용 하 여 상시 암호화를 지원 합니다.

## <a name="permissions"></a>사용 권한

 필요 합니다 **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** 하 고 **VIEW ANY COLUMN MASTER KEY DEFINITION** 데이터베이스의 권한.  
  
## <a name="examples"></a>예  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>참고자료

 [보안 enclaves와 함께 always Encrypted &#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [자습서: 임의 암호화를 만들고 사용 하 여 enclave 사용 열에서 인덱스를 사용 하 여](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [캐시 된 열 암호화 키를 사용 하 여 인덱싱 작업을 호출 합니다.](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [임의 암호화를 사용 하 여 Enclave 사용 열 인덱스](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [AlwaysOn 및 데이터베이스 마이그레이션에 대 한 고려 사항](../security/encryption/always-encrypted-enclaves.md#considerations-for-alwayson-and-database-migration)
