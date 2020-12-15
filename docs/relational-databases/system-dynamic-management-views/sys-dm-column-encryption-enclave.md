---
description: sys.dm_column_encryption_enclave(Transact-SQL)
title: sys.dm_column_encryption_enclave (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 6d15c17b4e023909210cef55884064757ae5ddc2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482784"
---
# <a name="sysdm_column_encryption_enclave-transact-sql"></a>sys.dm_column_encryption_enclave(Transact-SQL)
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Always Encrypted의 secure enclave에 대 한 성능 카운터를 반환 합니다. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../security/encryption/always-encrypted-enclaves.md)를 참조하세요.

를 마지막으로 다시 시작한 후 enclave가 구성 되어 올바르게 초기화 된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 뷰에는 정확히 한 개의 행이 포함 됩니다. Enclave이 구성 되지 않았거나 올바르게 초기화 되지 않은 경우 뷰는 행을 반환 하지 않습니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|current_enclave_session_count|**int**|Enclave를 사용 하는 현재 클라이언트 세션 수입니다.|  
|current_column_encryption_key_count|**int**|Enclave가 현재 보유 하 고 있는 열 암호화 키의 수입니다.|  
|current_memory_size_kb|**bigint**|Enclave 메모리 크기 (KB)|  
|total_evicted_session_count|**bigint**|마지막 서버 다시 시작 이후 제거 된 enclave 세션의 총 수입니다.|   
  
## <a name="permissions"></a>사용 권한  
`VIEW SERVER STATE` 권한이 필요합니다.   
  
## <a name="examples"></a>예  
 
```sql  
SELECT * FROM sys.dm_column_encryption_enclave;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Always Encrypted 서버 구성 옵션에 대한 Enclave 형식 구성](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
  
  
