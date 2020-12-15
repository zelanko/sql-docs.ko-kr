---
description: sp_pdw_database_encryption (Azure Synapse Analytics)
title: sp_pdw_database_encryption (Azure Synapse Analytics) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 73d1eb9fe27fa060a8bfcd13341a3908545aeed3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468344"
---
# <a name="sp_pdw_database_encryption-azure-synapse-analytics"></a>sp_pdw_database_encryption (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  **Sp_pdw_database_encryption** 를 사용 하 여 어플라이언스에 대해 투명 한 데이터 암호화를 사용 하도록 설정 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 합니다. **Sp_pdw_database_encryption** 를 1로 설정 하면 **ALTER database** 문을 사용 하 여 tde를 사용 하 여 데이터베이스를 암호화 합니다.  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

#### <a name="parameters"></a>매개 변수  
`[ @enabled = ] enabled` 투명 한 데이터 암호화를 사용할지 여부를 결정 합니다. *enabled* 는 **int** 이며 다음 값 중 하나일 수 있습니다.  
  
-   0 = 사용 안 함  
  
-   1 = 사용  
  
 매개 변수 없이 **sp_pdw_database_encryption** 를 실행 하면 어플라이언스의 현재 상태를 스칼라 결과 집합으로 반환 합니다. 즉, 0은 사용 하지 않도록 설정 하 고 1은 사용 하도록 설정 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **Sp_pdw_database_encryption** 를 사용 하 여 tde를 사용 하도록 설정 하면 tempdb 데이터베이스가 삭제 되 고 다시 만들어지고 암호화 됩니다. 이러한 이유로 tempdb를 사용 하는 다른 활성 세션이 있는 동안에는 TDE를 어플라이언스에서 사용 하도록 설정할 수 없습니다. 어플라이언스에서 TDE를 사용 하거나 사용 하지 않도록 설정 하는 작업은 어플라이언스의 상태를 변경 하는 작업입니다. 대부분의 경우 어플라이언스 수명에서 한 번 수행 되 고 어플라이언스에 트래픽이 없을 때 실행 되어야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 데이터베이스 역할의 멤버 자격 또는 **CONTROL SERVER** 권한이 필요 합니다.  
  
## <a name="example"></a>예  
 다음 예에서는 어플라이언스에서 TDE를 사용 하도록 설정 합니다.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>참조  
 [Azure Synapse Analytics를 &#40;sp_pdw_database_encryption_regenerate_system_keys&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [Azure Synapse Analytics를 &#40;sp_pdw_log_user_data_masking&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
