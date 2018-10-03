---
title: sp_pdw_log_user_data_masking (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 23d7846bd72329a62579765679687204a8e14ec5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630241"
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  사용 하 여 **sp_pdw_log_user_data_masking** 에서 마스킹 사용자 데이터를 사용 하도록 설정 하려면 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그. 사용자 데이터 마스킹 어플라이언스에 대 한 모든 데이터베이스의 문을 영향을 줍니다.  
  
> [!IMPORTANT]  
>  합니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그의 영향을 받는 **sp_pdw_log_user_data_masking** 확신 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그. **sp_pdw_log_user_data_masking** 데이터베이스 트랜잭션 로그 영향을 주지 않습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그입니다.  
  
 **백그라운드** 기본 구성에서 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그는 전체 포함 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 일부 경우에는 수와 같은 작업에 포함 된 사용자 데이터를 포함 **삽입**,  **업데이트**, 및 **선택** 문입니다. 어플라이언스에서 문제가 발생할 경우 이렇게 하면 분석 문제를 재현 하지 않고도 문제를 발생 시킨 조건에 있습니다. 사용자 데이터에 기록 되지 않도록 하기 위해 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그, 고객은이 저장된 프로시저를 사용 하 여 사용자 데이터 마스킹 설정 하도록 선택할 수 있습니다. 문을 계속 쓸 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그에 있지만 전부는 몇 가지 미리 정의 된 상수 값으로 대체 사용자 데이터를 포함할 수 있는 문의 리터럴; 마스킹됩니다.  
  
 어플라이언스에서 투명 한 데이터 암호화를 사용 하는 경우의 사용자 데이터 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그는 자동으로 켜 집니다.  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>매개 변수  
 [ **@masking_mode=** ] *masking_mode*  
 투명 한 데이터 암호화 로그 사용자 데이터 마스킹 사용 되는지 여부를 결정 합니다. *masking_mode* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
-   0 = 사용 안 함, 사용자 데이터에 표시 된 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그.  
  
-   1 = 사용, 데이터 문이 나타나는 사용자는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그 되지만 사용자 데이터를 마스킹.  
  
-   2 = 문을 포함 하는 사용자 데이터에 기록 되지 않습니다는 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그.  
  
 실행 **sp_pdw_ log_user_data_masking** 스칼라 결과 집합으로 어플라이언스에 TDE 로그 사용자 데이터 마스킹의 현재 상태를 반환 하는 매개 변수 없이 합니다.  
  
## <a name="remarks"></a>Remarks  
 사용자 데이터에 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동에서 미리 정의 된 상수 값을 사용 하 여 리터럴 수 있도록 대체 로그 **선택** 및 DML 문 처럼 사용자 데이터를 포함할 수 있습니다. 설정 *masking_mode* 1로 열 이름이 나 테이블 이름 같은 메타 데이터를을 마스크 하지 않습니다. 설정 *masking_mode* 2 열 이름이 나 테이블 이름 등의 메타 데이터를 사용 하 여 문을 제거 합니다.  
  
 사용자 데이터에서 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그는 다음과 같은 방법으로 구현 됩니다.  
  
-   TDE 및 사용자 데이터에서 마스킹 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그는 기본적으로 해제 합니다. 문에 자동으로 마스킹되 지 않습니다 어플라이언스에 데이터베이스 암호화를 사용 하지 않는 경우.  
  
-   사용자 데이터 마스킹을 설정 어플라이언스에서 TDE를 자동으로 활성화 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그.  
  
-   TDE를 사용 하지 않도록 설정 하더라도에서 마스킹 사용자 데이터는 영향을 주지 않습니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 활동 로그.  
  
-   마스킹 사용자 데이터를 명시적으로 설정할 수 있습니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 를 사용 하 여 활동 로그는 **sp_pdw_log_user_data_masking** 프로시저입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **sysadmin** 고정 데이터베이스 역할 또는 **CONTROL SERVER** 권한.  
  
## <a name="example"></a>예제  
 다음 예제에서는 어플라이언스에 마스킹 TDE 로그 사용자 데이터입니다.  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>관련 항목  
 [가 sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
