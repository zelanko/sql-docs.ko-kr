---
title: sp_enclave_send_keys (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2019
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
ms.openlocfilehash: ca6e7485e85665f06c2410438b902fa0647418ae
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593754"
---
# <a name="sp_enclave_send_keys-transact-sql"></a>sp_enclave_send_keys (Transact-sql)
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

데이터베이스에 정의 된 열 암호화 키를 [secure enclaves와 Always Encrypted](../security/encryption/always-encrypted-enclaves.md)에 사용 되는 서버 쪽 secure enclave에 보냅니다.

`sp_enclave_send_keys`는 enclave 사용 되는 키만 보내고 임의 암호화를 사용 하 여 인덱스를 포함 하는 열을 암호화 합니다. 일반 사용자 쿼리의 경우 클라이언트 드라이버는 쿼리의 계산에 필요한 키를 enclave에 제공 합니다. `sp_enclave_send_keys`은 데이터베이스에 정의 되어 있고 암호화 된 인덱스 열에 사용 되는 모든 열 암호화 키를 보냅니다. 

`sp_enclave_send_keys`는 enclave에 키를 전송 하는 쉬운 방법을 제공 하 고 후속 인덱싱 작업을 위해 열 암호화 키 캐시를 채웁니다. `sp_enclave_send_keys` 사용 하 여 사용:
- Dba에 게 열 마스터 키에 대 한 액세스 권한이 없는 경우 암호화 된 데이터베이스 열의 인덱스 또는 통계를 다시 작성 하거나 변경 하는 DBA입니다. [캐시 된 열 암호화 키를 사용 하 여 인덱싱 작업 호출](../security/encryption/always-encrypted-enclaves-create-use-indexes.md#invoke-indexing-operations-using-cached-column-encryption-keys)을 참조 하세요.
- 암호화 된 열에 대 한 인덱스 복구를 완료 하려면 [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] 합니다. [데이터베이스 복구](../security/encryption/always-encrypted-enclaves.md#database-recovery)를 참조 하세요.
- SQL Server에 대 한 .NET Framework Data Provider를 사용 하 여 암호화 된 열에 데이터를 대량 로드 하는 응용 프로그램입니다.

`sp_enclave_send_keys`성공적으로 호출 하려면 데이터베이스 연결에 대해 Always Encrypted 및 enclave 계산을 사용 하 여 데이터베이스에 연결 해야 합니다. 열 마스터 키에 대 한 액세스 권한이 있어야 하며, 열 암호화 키를 보호 하 고, 데이터베이스의 Always Encrypted 키 메타 데이터에 액세스할 수 있는 권한이 있어야 합니다. 

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
  
## <a name="permissions"></a>사용 권한

 데이터베이스에서 `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` 및 `VIEW ANY COLUMN MASTER KEY DEFINITION` 권한이 필요 합니다.  
  
## <a name="examples"></a>예  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>참고 항목
- [보안 enclave를 사용한 Always Encrypted](../security/encryption/always-encrypted-enclaves.md) 
 
- [Secure enclaves와 함께 Always Encrypted를 사용 하 여 열에 인덱스 만들기 및 사용](../security/encryption/always-encrypted-enclaves-create-use-indexes.md)

- [자습서: 임의 암호화를 사용 하 여 enclave 사용 열에서 인덱스 만들기 및 사용](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)
