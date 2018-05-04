---
title: sp_pdw_log_user_data_masking (SQL 데이터 웨어하우스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-data-warehouse
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c858d435aef7e86b40d50dc2232dced53adf6c4f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  사용 하 여 **sp_pdw_log_user_data_masking** 사용자 데이터에 마스킹을 사용 하려면 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 합니다. 사용자 데이터 마스킹 문을 기기에서 모든 데이터베이스에 영향을 줍니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그의 영향을 받는 **sp_pdw_log_user_data_masking** 확신이 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 합니다. **sp_pdw_log_user_data_masking** 데이터베이스 트랜잭션 로그에는 영향을 주지 않는 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그입니다.  
  
 **배경:** 기본 구성에서 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 전체 포함 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 일부 경우에는 수와 같은 작업에 포함 된 사용자 데이터를 포함 **삽입**,  **업데이트**, 및 **선택** 문. 어플라이언스에서 문제가 발생할 때 이렇게 하면 분석 문제를 재현 하기 필요 없이 문제가 발생 한 조건입니다. 사용자 데이터에 기록 되지 않도록 하기 위해 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그가 저장된 프로시저를 사용 하 여 사용자 데이터 마스킹 설정에 고객을 선택할 수 있습니다. 문을에 계속 기록 됩니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 했지만 몇 가지 미리 정의 된 상수 값으로 대체 사용자 데이터를 포함 하는 문에서 리터럴; 마스킹됩니다.  
  
 어플라이언스에서 투명 한 데이터 암호화를 사용 하는 경우의 사용자 데이터를 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 작업 로그는 자동으로 켜 집니다.  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>매개 변수  
 [ **@masking_mode=** ] *masking_mode*  
 투명 한 데이터 암호화 로그 사용자 데이터 마스킹 사용 되는지 여부를 결정 합니다. *masking_mode* 은 **int**, 다음 값 중 하나가 될 수 있습니다.  
  
-   0 = 사용 안 함, 사용자 데이터에 표시 된 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 합니다.  
  
-   1 = 사용, 데이터 문을에 표시 되는 사용자는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 되지만 사용자 데이터는 마스크입니다.  
  
-   2 = 문을 포함 하는 사용자 데이터에 기록 되지 않습니다는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 합니다.  
  
 실행 **sp_pdw_ log_user_data_masking** 스칼라 결과 집합으로 어플라이언스에 TDE 로그 사용자 데이터 마스킹의 현재 상태를 반환 하는 매개 변수 없이 합니다.  
  
## <a name="remarks"></a>주의  
 사용자 데이터에 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동에서 미리 정의 된 상수 값을 사용 하 여 리터럴을 사용 하면 교체를 기록 **선택** 및 DML 문에서 사용자 데이터를 포함 하 합니다. 설정 *masking_mode* 1로 열 이름이 나 테이블 이름 같은 메타 데이터를을 마스크 하지 않습니다. 설정 *masking_mode* 2로 열 이름이 나 테이블 이름 같은 메타 데이터와 문을 제거 합니다.  
  
 사용자 데이터에 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그에서 다음과 같은 방법으로 구현 됩니다.  
  
-   TDE 및 사용자 데이터에 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그는 기본적으로 해제 되어 있습니다. 문은 하지 자동으로 마스킹됩니다 어플라이언스에서 데이터베이스 암호화를 사용 하지 않는 경우.  
  
-   사용자 데이터 마스킹 설정 기기에서 TDE를 자동으로 활성화 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 합니다.  
  
-   TDE를 사용 하지 않도록 설정 하더라도에서 마스킹 사용자 데이터는 영향을 주지 않습니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 합니다.  
  
-   사용자 데이터에 마스킹을 명시적으로 설정할 수 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그를 사용 하 여는 **sp_pdw_log_user_data_masking** 프로시저입니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **sysadmin** 고정 데이터베이스 역할 또는 **제어 서버** 권한.  
  
## <a name="example"></a>예제  
 다음 예에서는 어플라이언스에서 마스킹 로그 사용자 데이터를 TDE를 설정 합니다.  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [가 sp_pdw_database_encryption &#40;SQL 데이터 웨어하우스&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 데이터 웨어하우스&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
