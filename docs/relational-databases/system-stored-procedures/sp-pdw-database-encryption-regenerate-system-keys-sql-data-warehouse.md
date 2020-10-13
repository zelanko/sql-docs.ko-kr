---
title: sp_pdw_database_encryption_regenerate_system_keys (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: bb13e323-a984-4462-8b6d-6019c38ddd9d
author: ronortloff
ms.author: rortloff
ms.reviewer: ''
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 28b5870be32b62cc0283c51e9370a4be70b198e5
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987239"
---
# <a name="sp_pdw_database_encryption_regenerate_system_keys-sql-data-warehouse"></a>sp_pdw_database_encryption_regenerate_system_keys (SQL Data Warehouse)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  어플라이언스에서 TDE를 사용 하는 경우 암호화 된 내부 데이터베이스에 대 한 인증서 및 데이터베이스 암호화 키를 회전 하려면 **sp_pdw_database_encryption_regenerate_system_keys** 을 사용 합니다. 여기에는 `tempdb`도 포함됩니다. TDE가 사용 하도록 설정 된 경우에만 성공 합니다.  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_database_encryption_regenerate_system_keys  ;  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 프로시저에는 매개 변수가 없습니다.  
  
 이 절차는 어플라이언스의 트래픽이 부족할 때 사용 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 데이터베이스 역할의 멤버 자격 또는 **CONTROL SERVER** 권한이 필요 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 데이터베이스 암호화 키를 다시 생성 합니다.  
  
```sql  
EXEC sys.sp_pdw_database_encryption_regenerate_system_keys;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
