---
title: cdc. change_tables (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.change_tables
- cdc.change_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.change_tables
ms.assetid: 3525a5f5-8d8b-46a8-b334-4b7cd9fb7c21
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 585ebf4a2a01160eec18c4af8f6d25ec4480ddb7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820078"
---
# <a name="cdcchange_tables-transact-sql"></a>cdc.change_tables(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 내의 각 변경 테이블에 대해 한 개의 행을 반환합니다. 변경 테이블은 원본 테이블에서 변경 데이터 캡처를 사용하도록 설정할 때 생성됩니다. 시스템 테이블은 직접 쿼리하지 않는 것이 좋습니다. 대신, [sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) 저장 프로시저를 실행 합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|변경 테이블의 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 경우 이 열은 항상 0을 반환합니다.|  
|**source_object_id**|**int**|변경 데이터 캡처를 사용하도록 설정한 원본 테이블의 ID입니다.|  
|**capture_instance**|**sysname**|인스턴스별 추적 개체의 이름을 지정하는 데 사용되는 캡처 인스턴스의 이름입니다. 기본적으로 이름은 원본 스키마 이름에 *schemaname_sourcename*형식으로 된 원본 테이블 이름과 함께 파생 됩니다.|  
|**start_lsn**|**binary(10)**|변경 테이블의 변경 데이터를 쿼리할 때 하위 엔드포인트를 나타내는 LSN(로그 시퀀스 번호)입니다.<br /><br /> NULL = 하위 엔드포인트가 설정되지 않았습니다.|  
|**end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]의 경우 이 열은 항상 NULL을 반환합니다.|  
|**supports_net_changes**|**bit**|변경 테이블에서 순 변경에 대한 쿼리 지원을 사용하도록 설정되어 있습니다.|  
|**has_drop_pending**|**bit**|원본 테이블이 삭제되었다는 알림이 캡처 프로세스에 수신되었습니다.|  
|**role_name**|**sysname**|변경 데이터에 대한 액세스를 제어하는 데 사용되는 데이터베이스 역할의 이름입니다.<br /><br /> NULL = 역할이 사용되지 않습니다.|  
|**index_name**|**sysname**|원본 테이블의 행을 고유하게 식별하는 데 사용되는 인덱스 이름입니다. **index_name** 은 원본 테이블의 기본 키 인덱스 이름 이거나, 원본 테이블에 변경 데이터 캡처가 설정 된 경우 지정 된 고유 인덱스의 이름입니다.<br /><br /> NULL = 변경 데이터 캡처를 사용하도록 설정할 때 원본 테이블에 기본 키가 없었고 고유한 인덱스가 지정되지 않았습니다.<br /><br /> 참고: 기본 키가 있는 테이블에 변경 데이터 캡처가 설정 되어 있는 경우 변경 데이터 캡처 기능은 순 변경의 설정 여부에 관계 없이 인덱스를 사용 합니다. 변경 데이터 캡처를 사용하도록 설정한 후에는 기본 키를 수정할 수 없습니다. 테이블에 기본 키가 없는 경우에도 변경 데이터 캡처를 사용하도록 설정할 수 있지만 순 변경 설정을 false로 설정해야만 합니다. 변경 데이터 캡처를 사용하도록 설정한 후 기본 키를 만들 수 있습니다. 또한 변경 데이터 캡처에서는 기본 키를 사용하지 않으므로 기본 키를 수정할 수 있습니다.|  
|**filegroup_name**|**sysname**|변경 테이블이 있는 파일 그룹의 이름입니다.<br /><br /> NULL = 변경 테이블이 데이터베이스의 기본 파일 그룹에 있습니다.|  
|**create_date**|**datetime**|원본 테이블이 사용되도록 설정된 날짜입니다.|  
|**partition_switch**|**bit**|변경 데이터 캡처가 설정 된 테이블에 대해 **ALTER table** 의 **SWITCH PARTITION** 명령을 실행할 수 있는지 여부를 나타냅니다. 0은 파티션 전환이 차단되었음을 나타냅니다. 분할되지 않은 테이블은 항상 1을 반환합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
