---
title: cdc입니다. &lt;capture_instance&gt;_CT (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- cdc
- cdc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.<capture_instance>_CT
ms.assetid: 979c8110-3c54-4e76-953c-777194bc9751
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: deb54a835c5c163061b371e8629b95ed0bfcdce9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="cdcltcaptureinstancegtct-transact-sql"></a>cdc입니다. &lt;capture_instance&gt;_CT (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  원본 테이블에서 변경 데이터 캡처를 활성화할 때 생성된 변경 테이블입니다. 이 테이블은 원본 테이블에 대해 수행된 각 삽입 및 삭제 작업당 한 개의 행을, 업데이트 작업당 두 개의 행을 반환합니다. 원본 테이블이 활성화될 때 변경 테이블의 이름이 지정되지 않을 경우 이름이 파생됩니다. 이름의 형식은 cdc입니다. *capture_instance*_CT 여기서 *capture_instance* 원본 테이블의 스키마 이름 및 형식에서 원본 테이블 이름을 *schema_table*합니다. 예를 들어 경우 테이블 **Person.Address** 에 **AdventureWorks** 변경 데이터 캡처에 대 한 예제 데이터베이스를 사용 하면 파생된 변경 테이블 이름은 **cdc. Person_Address_CT**합니다.  
  
 하는 것이 좋습니다 있습니다 **쿼리하지 않는 시스템 테이블 직접**합니다. 대신, 실행 된 [cdc.fn_cdc_get_all_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) 및 [cdc.fn_cdc_get_net_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) 함수입니다.  
  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|변경에 대한 커밋 트랜잭션과 연관된 LSN(로그 시퀀스 번호)입니다.<br /><br /> 동일한 트랜잭션에서 커밋된 변경의 커밋 LSN은 모두 동일합니다. 예를 들어 원본 테이블에서 delete 작업을 두 개의 행을 제거 하는 경우 변경 테이블 포함 됩니다 두 개의 행을 동일한 **__ $start_lsn** 값입니다.|  
|**__ $ end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 이 열은 항상 NULL입니다.|  
|**__$seqval**|**binary(10)**|트랜잭션 내 행 변경을 정렬하는 데 사용되는 시퀀스 값입니다.|  
|**__$operation**|**int**|변경과 연관된 DML(데이터 조작 언어) 작업을 식별합니다. 다음 중 하나일 수 있습니다.<br /><br /> 1 = 삭제<br /><br /> 2 = 삽입<br /><br /> 3 = 업데이트(이전 값)<br /><br /> 열 데이터는 update 문을 실행하기 전의 행 값을 가집니다.<br /><br /> 4 = 업데이트(새 값)<br /><br /> 열 데이터는 update 문을 실행한 후의 행 값을 가집니다.|  
|**__$update_mask**|**varbinary(128)**|변경된 열을 식별하는 변경 테이블의 열 서수를 기준으로 하는 비트 마스크입니다.|  
|*\<captured source table columns>*|다양함|변경 테이블의 나머지 열은 캡처 인스턴스가 생성될 때 캡처된 열로 식별된 원본 테이블의 열입니다. 캡처된 열 목록에 아무 열도 지정하지 않으면 원본 테이블의 모든 열이 이 테이블에 포함됩니다.|  
|**__ $ command_id** |**int** |트랜잭션 내에서 작업 순서를 추적합니다. |  
  
## <a name="remarks"></a>주의  

`__$command_id` 열이 열 버전 2016 통해 2012 누적 업데이트에 도입 되었습니다. 버전 및 다운로드 정보에 대 한 참조에서 기술 자료 문서 3030352 [수정: 변경 테이블은 올바르지 않게 정렬 되었기 올바르게 업데이트에 대 한 Microsoft SQL Server 데이터베이스에 대 한 변경 데이터를 사용 하도록 설정한 후 행 캡처](https://support.microsoft.com/help/3030352/fix-the-change-table-is-ordered-incorrectly-for-updated-rows-after-you)합니다.  자세한 내용은 참조 [CDC 기능을 바꾸어 벗어나지 SQL Server 2012, 2014 및 2016 용 최신 CU로 업그레이드 한 후](https://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/)합니다.

## <a name="captured-column-data-types"></a>캡처된 열 데이터 형식  
 이 테이블에 포함된 캡처된 열의 데이터 형식과 값은 다음 항목을 제외하고 해당하는 원본 열과 동일합니다.  
  
-   **타임 스탬프** 로 정의 **binary (8)**합니다.  
  
-   **Identity** 열으로 정의 됩니다 **int** 또는 **bigint**합니다.  
  
 그러나 이러한 열의 값은 원본 열 값과 같습니다.  
  
### <a name="large-object-data-types"></a>큰 개체 데이터 형식  
 데이터 형식의 열 **이미지**, **텍스트**, 및 **ntext** 항상 할당 된 **NULL** 경우이 값 __ $operation = 1 또는 \_ \_$operation = 3입니다. 데이터 형식의 열 **varbinary (max)**, **varchar (max)**, 또는 **nvarchar (max)** 할당 되는 **NULL** 값으로 \_ \_$operation = 3을 업데이트 하는 동안 해당 열이 변경 하지 않는 한 합니다. 때 \_ \_$operation = 1, 이러한 열에는 삭제할 때 해당 값이 할당 됩니다. 항상 캡처 인스턴스에 포함 되는 계산된 열 값을 가질 **NULL**합니다.  
  
 기본적으로 단일 INSERT, UPDATE, WRITETEXT 또는 UPDATETEXT 문에서 캡처된 열에 추가할 수 있는 최대 크기는 65,536바이트(64KB)입니다. 사용 하 여 더 큰 LOB 데이터를 지 원하는 데이 크기를 늘리려면는 [최대 텍스트 복제 크기 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md) 더 큰 최대 크기를 지정 합니다. 자세한 내용은 [Configure the max text repl size Server Configuration Option](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)을 참조하세요.  
  
## <a name="data-definition-language-modifications"></a>데이터 정의 언어 수정  
 열을 추가, 삭제와 같은 원본 테이블에 대 한 DDL 수정은에 기록 되는 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) 테이블입니다. 이러한 변경 내용은 변경 테이블에는 적용되지 않습니다. 즉 변경 테이블의 정의는 일정하게 유지됩니다. 변경 테이블에 열을 삽입할 때 캡처 프로세스는 원본 테이블과 연관된 캡처된 열 목록에 표시되지 않는 열은 무시합니다. 원본 테이블에 더 이상 없는 캡처된 열 목록에 열이 표시되는 경우 해당 열에는 Null 값이 할당됩니다.  
  
 원본 테이블에 있는 열의 데이터 형식을 변경에 기록 됩니다는 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) 테이블입니다. 이 변경은 변경 테이블의 정의를 바꿉니다. 캡처 프로세스에서 원본 테이블에 적용된 DDL 변경에 대한 로그 레코드가 발견되면 변경 테이블에 있는 캡처된 열의 데이터 형식이 수정됩니다.  
  
 원본 테이블에 있는 캡처된 열의 데이터 형식을 수정할 때 데이터 형식의 크기가 줄어드는 경우에는 다음 절차에 따라 변경 테이블에서 해당 열이 성공적으로 수정될 수 있는지 확인하십시오.  
  
1.  원본 테이블의 열에서 수정할 값을 업데이트하여 계획된 데이터 형식 크기에 맞춥니다. 예를 들어에서 데이터 형식을 변경 하면 **int** 를 **smallint**에 맞는 크기로 값을 업데이트는 **smallint** 범위, 32, 767 자로-32, 768입니다.  
  
2.  변경 테이블에서 해당 열에 동일한 업데이트 작업을 수행합니다.  
  
3.  새 데이터 형식을 지정하여 원본 테이블을 변경합니다. 데이터 형식 변경이 변경 테이블로 성공적으로 전파됩니다.  
  
## <a name="data-manipulation-language-modifications"></a>데이터 조작 언어 수정  
 변경 데이터 캡처가 활성화된 원본 테이블에서 삽입, 업데이트 및 삭제 작업을 수행하면 데이터베이스 트랜잭션 로그에 이러한 DML 작업에 대한 레코드가 기록됩니다. 변경 데이터 캡처 프로세스는 트랜잭션 로그에서 이러한 변경 내용에 대한 정보를 검색하고 변경 테이블에 하나 또는 두 개의 행을 추가하여 변경 내용을 기록합니다. 일반적으로 변경 테이블 항목의 커밋은 단일 항목이 아니라 변경 내용 그룹에 대해 수행되어야 하지만 항목은 원본 테이블에 커밋된 순서와 동일하게 변경 테이블 추가됩니다.  
  
 변경 테이블 항목 내에서 **__ $start_lsn** 열은 커밋 LSN을 원본 테이블에 변경 내용과 연결 된 기록 하는 데 사용 됩니다 및 **__ $seqval 열** 내의 변경을 정렬 하는 데 사용 해당 트랜잭션입니다. 이러한 메타데이터 열은 원본 변경 내용의 커밋 순서가 유지되도록 하는 데 사용될 수 있습니다. 캡처 프로세스가 해당 변경 정보를 트랜잭션 로그에서 가져오기 때문에 변경 테이블 항목은 해당 원본 테이블 변경 내용과 동기적으로 나타나지 않습니다. 대신 캡처 프로세스가 트랜잭션 로그에서 관련 변경 항목을 처리한 후 해당 변경 내용이 비동기적으로 나타납니다.  
  
 삽입 및 삭제 작업의 경우 업데이트 마스크에 있는 모든 비트가 설정됩니다. 업데이트 작업의 경우 업데이트 이전 행 및 업데이트 이후 행에서 업데이트 마스크가 수정되어 업데이트 중 변경된 열을 반영합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)  
  
  
