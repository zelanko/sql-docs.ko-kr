---
title: sys. sp_cdc_cleanup_change_table (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_cleanup_change_table
- sp_cdc_cleanup_change_table_TSQL
- sys.sp_cdc_cleanup_change_table
- sys.sp_cdc_cleanup_change_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_cleanup_change_tables
- sp_cdc_cleanup_change_tables
ms.assetid: 02295794-397d-4445-a3e3-971b25e7068d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ac10ff9accd4cac39caef8139406319701026e79
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891175"
---
# <a name="syssp_cdc_cleanup_change_table-transact-sql"></a>sys.sp_cdc_cleanup_change_table(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  지정 된 *low_water_mark* 값을 기준으로 현재 데이터베이스의 변경 테이블에서 행을 제거 합니다. 이 저장 프로시저는 변경 테이블 정리 프로세스를 직접 관리하려는 사용자를 위해 제공됩니다. 이 프로시저는 변경 테이블에 있는 데이터의 모든 소비자에게 영향을 주므로 사용할 때 주의해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_cdc_cleanup_change_table   
  [ @capture_instance = ] 'capture_instance',   
  [ @low_water_mark = ] low_water_mark ,  
  [ @threshold = ]'delete threshold'  
```  
  
## <a name="arguments"></a>인수  
 [ @capture_instance =] '*capture_instance*'  
 변경 테이블과 연결된 캡처 인스턴스의 이름입니다. *capture_instance* 는 **sysname**이며 기본값은 없고 NULL 일 수 없습니다.  
  
 현재 데이터베이스에 있는 캡처 인스턴스의 이름을 *capture_instance* 합니다.  
  
 [ @low_water_mark =] *low_water_mark*  
 *캡처 인스턴스에*대 한 새 하위 워터 마크로 사용할 LSN (로그 시퀀스 번호)입니다. *low_water_mark* 는 **binary (10)** 이며 기본값은 없습니다.  
  
 값이 null이 아닌 경우에는이 값이 [cdc. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) 테이블에 있는 현재 항목의 start_lsn 값으로 나타나야 합니다. cdc.lsn_time_mapping에 있는 다른 항목의 커밋 시간이 새 하위 워터마크에서 식별한 항목과 동일한 경우 해당 항목 그룹과 연결된 최소 LSN이 하위 워터마크로 지정됩니다.  
  
 값을 명시적으로 NULL로 설정 하면 *캡처 인스턴스의* 현재 *하위 워터 마크가* 정리 작업의 상한을 정의 하는 데 사용 됩니다.  
  
 [ @threshold =] '*임계값 삭제*'  
 정리 시 단일 문을 사용하여 삭제할 수 있는 삭제 항목의 최대 수입니다. *delete_threshold* 는 **bigint**이며 기본값은 5000입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 sys.sp_cdc_cleanup_change_table은 다음 작업을 수행합니다.  
  
1.  @low_water_mark매개 변수가 NULL이 아닌 경우 *캡처 인스턴스에* 대 한 start_lsn 값을 새 *하위 워터 마크로*설정 합니다.  
  
    > [!NOTE]  
    >  새 하위 워터마크는 저장 프로시저 호출에 지정된 하위 워터마크가 아닐 수 있습니다. cdc.lsn_time_mapping 테이블에 있는 다른 항목이 동일한 커밋 시간을 공유하는 경우 항목 그룹에 표시된 최소 LSN이 조정된 하위 워터마크로 선택됩니다. @low_water_mark매개 변수가 NULL 이거나 현재 하위 워터 마크가 새 lowwatermark 마크 보다 큰 경우 캡처 인스턴스에 대 한 start_lsn 값이 변경 되지 않은 상태로 유지 됩니다.  
  
2.  __$start_lsn 값이 하위 워터마크보다 작은 변경 테이블 항목이 삭제됩니다. 단일 트랜잭션에서 삭제되는 행 수를 제한하는 데 삭제 임계값이 사용됩니다. 항목을 성공적으로 삭제하지 못하는 오류가 발생하면 이 오류가 보고만 되고 캡처 인스턴스 하위 워터마크에서 호출을 기준으로 변경되었을 수 있는 내용에는 영향을 주지 않습니다.  

 다음과 같은 경우 sys.sp_cdc_cleanup_change_table을 사용합니다.  
  
-   정리 에이전트 작업에서 삭제 실패를 보고하는 경우  
  
     관리자는 이 저장 프로시저를 명시적으로 실행하여 실패한 작업을 다시 시도할 수 있습니다. 지정 된 캡처 인스턴스에 대 한 정리를 다시 시도 하려면 sp_cdc_cleanup_change_table를 실행 하 고 매개 변수에 대해 NULL을 지정 @low_water_mark 합니다.  
  
-   정리 에이전트 작업에서 사용하는 단순 보존 기반 정책이 적합하지 않은 경우  
  
     이 저장 프로시저는 단일 캡처 인스턴스의 정리를 수행하므로 개별 캡처 인스턴스에 따라 정리 규칙을 조정하는 사용자 지정 정리 전략을 작성하는 데 사용할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [fn_cdc_get_min_lsn &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [sys.fn_cdc_increment_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)  
  
  
