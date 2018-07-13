---
title: 가 sp_pdw_database_encryption (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-objects
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6508d150df663a6e95437d0b6b3bfd0c8f65906f
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926154"
---
# <a name="sppdwdatabaseencryption-sql-data-warehouse"></a>가 sp_pdw_database_encryption (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  사용 하 여 **가 sp_pdw_database_encryption** 투명 한 데이터 암호화에 사용 하는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 어플라이언스입니다. 때 **가 sp_pdw_database_encryption** 사용 하 여 1로 설정 합니다 **ALTER DATABASE** TDE를 사용 하 여 데이터베이스를 암호화 하는 문입니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>매개 변수  
 [ **@enabled=** ] *enabled*  
 투명 한 데이터 암호화 사용 되는지 여부를 결정 합니다. *사용 하도록 설정* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
-   0 = 사용 안 함  
  
-   1 = 사용  
  
 실행 **가 sp_pdw_database_encryption** 스칼라 결과 집합으로 어플라이언스에 TDE의 현재 상태를 반환 하는 매개 변수 없이: 사용 안 함, 0 또는 1을 사용 하도록 설정 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 TDE를 사용 하 여 사용 하는 경우 **가 sp_pdw_database_encryption**, tempdb 데이터베이스 삭제, 다시 생성 및 암호화 합니다. Tempdb를 사용 하 여 다른 활성 세션이 있는 동안 따라서 TDE는 기기에서 사용할 수 없습니다. 사용 하도록 설정 하거나 기기에서 TDE를 사용 하지 않도록 설정 되며 대부분의 경우에서 어플라이언스의 상태를 변경 하는 동작 어플라이언스 수명에서 한 번 수행 해야 하는 어플라이언스에 트래픽이 없는 경우 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **sysadmin** 고정 데이터베이스 역할 또는 **CONTROL SERVER** 권한.  
  
## <a name="example"></a>예제  
 다음 예제에서는 어플라이언스에에서 TDE를 설정합니다.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
