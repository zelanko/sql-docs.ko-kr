---
description: sp_pdw_log_user_data_masking (SQL Data Warehouse)
title: sp_pdw_log_user_data_masking (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c3b65b6e3626a79fae4f5b5ac87e997ce3c97554
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988809"
---
# <a name="sp_pdw_log_user_data_masking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL Data Warehouse)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  **Sp_pdw_log_user_data_masking** 를 사용 하 여 활동 로그에서 사용자 데이터 마스킹을 사용 하도록 설정 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 합니다. 사용자 데이터 마스킹은 어플라이언스의 모든 데이터베이스에 대 한 문에 영향을 줍니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] **Sp_pdw_log_user_data_masking** 의 영향을 받는 활동 로그는 특정 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그입니다. **sp_pdw_log_user_data_masking** 는 데이터베이스 트랜잭션 로그 또는 오류 로그에 영향을 주지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **배경:** 기본 구성 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그에는 전체 문이 포함 되어 있으며 [!INCLUDE[tsql](../../includes/tsql-md.md)] **INSERT**, **UPDATE**및 **SELECT** 문과 같은 작업에 포함 된 사용자 데이터를 포함 하는 경우도 있습니다. 어플라이언스에서 문제가 발생 하는 경우 문제를 재현할 필요 없이 문제를 일으킨 조건을 분석할 수 있습니다. 사용자 데이터가 활동 로그에 기록 되는 것을 방지 하기 위해 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 고객은이 저장 프로시저를 사용 하 여 사용자 데이터 마스킹을 설정 하도록 선택할 수 있습니다. 문은 활동 로그에 계속 기록 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 되지만 사용자 데이터를 포함할 수 있는 문의 모든 리터럴은 마스킹 되며 미리 정의 된 상수 값으로 대체 됩니다.  
  
 기기에서 투명 한 데이터 암호화를 사용 하는 경우 활동 로그의 사용자 데이터에 대 한 마스킹을 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 자동으로 설정 됩니다.  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
#### <a name="parameters"></a>매개 변수  
`[ @masking_mode = ] masking_mode` 투명 한 데이터 암호화 로그 사용자 데이터 마스킹을 사용 하는지 여부를 결정 합니다. *masking_mode* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
-   0 = 사용 안 함, 사용자 데이터가 활동 로그에 표시 됩니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
-   1 = 사용, 사용자 데이터 문이 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그에 나타나지만 사용자 데이터는 마스킹 됩니다.  
  
-   2 = 사용자 데이터를 포함 하는 문이 활동 로그에 기록 되지 않습니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
 매개 변수 없이 **sp_pdw_ log_user_data_masking** 를 실행 하면 어플라이언스에 대 한 tde 로그 사용자 데이터 마스킹의 현재 상태가 스칼라 결과 집합으로 반환 됩니다.  
  
## <a name="remarks"></a>설명  
 활동 로그의 사용자 데이터 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 을 사용 하면 **SELECT** 및 DML 문에서 사용자 데이터를 포함할 수 있는 미리 정의 된 상수 값으로 리터럴을 바꿀 수 있습니다. *Masking_mode* 를 1로 설정 해도 열 이름 또는 테이블 이름과 같은 메타 데이터는 마스킹 되지 않습니다. *Masking_mode* 를 2로 설정 하면 열 이름이 나 테이블 이름과 같은 메타 데이터가 있는 문이 제거 됩니다.  
  
 활동 로그의 사용자 데이터 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 은 다음과 같은 방식으로 구현 됩니다.  
  
-   활동 로그의 TDE 및 사용자 데이터 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 은 기본적으로 해제 되어 있습니다. 어플라이언스에서 데이터베이스 암호화를 사용 하지 않는 경우 문은 자동으로 마스킹 되지 않습니다.  
  
-   어플라이언스에서 TDE를 사용 하도록 설정 하면 활동 로그에서 사용자 데이터 마스킹을 자동으로 설정 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 됩니다.  
  
-   TDE를 사용 하지 않도록 설정 해도 활동 로그의 사용자 데이터 마스킹에는 영향을 주지 않습니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
-   [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] **Sp_pdw_log_user_data_masking** 절차를 사용 하 여 활동 로그에서 사용자 데이터 마스킹을 명시적으로 사용 하도록 설정할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 데이터베이스 역할의 멤버 자격 또는 **CONTROL SERVER** 권한이 필요 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 어플라이언스에서 TDE 로그 사용자 데이터 마스킹을 사용 하도록 설정 합니다.  
  
```sql  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
