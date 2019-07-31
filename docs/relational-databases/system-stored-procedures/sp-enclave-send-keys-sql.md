---
title: sp_enclave_send_keys (Transact-sql) | Microsoft Docs
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
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b4ced2feee2227ba1db492f721f57907069c5d99
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661356"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

데이터베이스의 모든 enclave 사용 열 암호화 키를 [보안 enclaves &#40;데이터베이스 엔진&#41;를](../../relational-databases/security/encryption/always-encrypted-enclaves.md)사용 하 여 Always Encrypted에서 사용 하는 enclave로 보냅니다.

## <a name="syntax"></a>구문  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>인수

이 저장 프로시저에는 인수가 없습니다.

## <a name="return-value"></a>반환 값

이 저장 프로시저에는 반환 값이 없습니다.
  
## <a name="result-sets"></a>결과 집합

이 저장 프로시저에는 결과 집합이 없습니다.
  
## <a name="remarks"></a>설명

**sp_enclave_send_keys** 는 다음 조건이 모두 충족 되는 경우 enclave 사용 열 암호화 키를 enclave로 보냅니다.

- Enclave는 SQL Server 인스턴스에서 사용할 수 있습니다.
- **sp_enclave_send_keys** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 드라이버를 사용 하 여 응용 프로그램에서 호출 되 고 Always Encrypted 및 enclave 계산을 모두 사용 하는 데이터베이스 연결을 사용 하 여 보안 enclaves로 Always Encrypted을 지원 합니다.

## <a name="permissions"></a>사용 권한

 데이터베이스에서 **VIEW ANY COLUMN ENCRYPTION key** Definition 및 **VIEW ANY COLUMN MASTER KEY definition** 권한이 필요 합니다.  
  
## <a name="examples"></a>예  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>참조

 [Secure enclaves &#40;데이터베이스 엔진으로 Always Encrypted&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [자습서: 임의 암호화를 사용 하 여 enclave 사용 열에서 인덱스 만들기 및 사용](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [캐시 된 열 암호화 키를 사용 하 여 인덱싱 작업 호출](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [임의 암호화를 사용 하는 Enclave 사용 열의 인덱스](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [AlwaysOn 및 데이터베이스 마이그레이션에 대 한 고려 사항](../security/encryption/always-encrypted-enclaves.md#anchorname-1-considerations-availability-groups-db-migration)
