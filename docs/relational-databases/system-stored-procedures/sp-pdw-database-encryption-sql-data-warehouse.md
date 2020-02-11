---
title: sp_pdw_database_encryption (SQL Data Warehouse) | Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 47d7aca62ddbf2637b54d77171a08817b842555c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008917"
---
# <a name="sp_pdw_database_encryption-sql-data-warehouse"></a>sp_pdw_database_encryption (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  **Sp_pdw_database_encryption** 를 사용 하 여 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 어플라이언스에 대해 투명 한 데이터 암호화를 사용 하도록 설정 합니다. **Sp_pdw_database_encryption** 를 1로 설정 하면 **ALTER database** 문을 사용 하 여 tde를 사용 하 여 데이터베이스를 암호화 합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>매개 변수  
`[ @enabled = ] enabled`투명 한 데이터 암호화를 사용할지 여부를 결정 합니다. *enabled* 는 **int**이며 다음 값 중 하나일 수 있습니다.  
  
-   0 = 사용 안 함  
  
-   1 = 사용  
  
 매개 변수 없이 **sp_pdw_database_encryption** 를 실행 하면 어플라이언스의 현재 상태를 스칼라 결과 집합으로 반환 합니다. 즉, 0은 사용 하지 않도록 설정 하 고 1은 사용 하도록 설정 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **Sp_pdw_database_encryption**를 사용 하 여 tde를 사용 하도록 설정 하면 tempdb 데이터베이스가 삭제 되 고 다시 만들어지고 암호화 됩니다. 이러한 이유로 tempdb를 사용 하는 다른 활성 세션이 있는 동안에는 TDE를 어플라이언스에서 사용 하도록 설정할 수 없습니다. 어플라이언스에서 TDE를 사용 하거나 사용 하지 않도록 설정 하는 작업은 어플라이언스의 상태를 변경 하는 작업입니다. 대부분의 경우 어플라이언스 수명에서 한 번 수행 되 고 어플라이언스에 트래픽이 없을 때 실행 되어야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 데이터베이스 역할의 멤버 자격 또는 **CONTROL SERVER** 권한이 필요 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 어플라이언스에서 TDE를 사용 하도록 설정 합니다.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
