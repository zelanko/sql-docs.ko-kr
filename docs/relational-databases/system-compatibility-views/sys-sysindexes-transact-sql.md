---
title: sys.sysindexes (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysindexes
- sysindexes_TSQL
- sys.sysindexes
- sys.sysindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysindexes system table
- sys.sysindexes compatibility view
ms.assetid: f483d89c-35c4-4a08-8f8b-737fd80d13f5
author: rothja
ms.author: jroth
ms.openlocfilehash: 560b5ab5d85c7f2a69fb5062a6eacc6e5c85ee1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053441"
---
# <a name="syssysindexes-transact-sql"></a>sys.sysindexes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스 내의 각 인덱스 및 테이블마다 한 행을 포함합니다. XML 인덱스는 이 뷰에서 지원되지 않습니다. 분할 된 테이블 및 인덱스는이 뷰에서; 완전히 지원 되지 않습니다. 사용 된 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰를 대신 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|인덱스가 속한 테이블의 ID입니다.|  
|**상태**|**int**|시스템 상태 정보입니다.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**first**|**binary(6)**|첫 페이지 또는 루트 페이지에 대한 포인터입니다.<br /><br /> 사용 되지 않는 경우 **indid** = 0.<br /><br /> NULL = 인덱스를 분할 하면 **indid** > 1.<br /><br /> NULL = 테이블 때 분할 **indid** 0 또는 1입니다.|  
|**indid**|**smallint**|인덱스의 ID입니다.<br /><br /> 0 = 힙<br /><br /> 1 = 클러스터형 인덱스<br /><br /> > 1 = 비클러스터형 인덱스|  
|**root**|**binary(6)**|에 대 한 **indid** > = 1, **루트** 루트 페이지에 대 한 포인터입니다.<br /><br /> 사용 되지 않는 경우 **indid** = 0.<br /><br /> NULL = 인덱스를 분할 하면 **indid** > 1.<br /><br /> NULL = 테이블 때 분할 **indid** 0 또는 1입니다.|  
|**minlen**|**smallint**|행의 최대 크기입니다.|  
|**keycnt**|**smallint**|키 수입니다.|  
|**groupid**|**smallint**|개체가 만들어진 파일 그룹의 ID입니다.<br /><br /> NULL = 인덱스를 분할 하면 **indid** > 1.<br /><br /> NULL = 테이블 때 분할 **indid** 0 또는 1입니다.|  
|**dpages**|**int**|에 대 한 **indid** = 0 또는 **indid** = 1 이면 **dpages** 사용 되는 데이터 페이지의 수입니다.<br /><br /> 에 대 한 **indid** > 1 **dpages** 사용 되는 인덱스 페이지의 수입니다.<br /><br /> 0 = 인덱스를 분할 하면 **indid** > 1.<br /><br /> 0 = 테이블 때 분할 **indid** 0 또는 1입니다.<br /><br /> 행 오버플로가 발생할 경우 정확한 결과가 반환되지 않습니다.|  
|**reserved**|**int**|에 대 한 **indid** = 0 또는 **indid** = 1 이면 **예약 된** 모든 인덱스 및 테이블 데이터에 할당 된 페이지의 수입니다.<br /><br /> 에 대 한 **indid** > 1 **예약** 인덱스에 할당 된 페이지의 수입니다.<br /><br /> 0 = 인덱스를 분할 하면 **indid** > 1.<br /><br /> 0 = 테이블 때 분할 **indid** 0 또는 1입니다.<br /><br /> 행 오버플로가 발생할 경우 정확한 결과가 반환되지 않습니다.|  
|**used**|**int**|에 대 한 **indid** = 0 또는 **indid** = 1 이면 **사용** 의 모든 인덱스 및 테이블 데이터에 대해 사용 된 총 페이지 수입니다.<br /><br /> 에 대 한 **indid** > 1 **사용** 인덱스에 사용 되는 페이지의 수입니다.<br /><br /> 0 = 인덱스를 분할 하면 **indid** > 1.<br /><br /> 0 = 테이블 때 분할 **indid** 0 또는 1입니다.<br /><br /> 행 오버플로가 발생할 경우 정확한 결과가 반환되지 않습니다.|  
|**rowcnt**|**bigint**|기준 데이터 수준 행 개수 **indid** = 0 및 **indid** = 1입니다.<br /><br /> 0 = 인덱스를 분할 하면 **indid** > 1.<br /><br /> 0 = 테이블 때 분할 **indid** 0 또는 1입니다.|  
|**rowmodctr**|**int**|테이블에 대해 통계를 마지막으로 업데이트한 이후에 삽입, 삭제 또는 업데이트된 행의 총 수를 셉니다.<br /><br /> 0 = 인덱스를 분할 하면 **indid** > 1.<br /><br /> 0 = 테이블 때 분할 **indid** 0 또는 1입니다.<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는 **rowmodctr** 이전 버전과 완전히 호환 되지 않습니다. 자세한 내용은 설명 부분을 참조하세요.|  
|**reserved3**|**int**|0을 반환합니다.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved4**|**int**|0을 반환합니다.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xmaxlen**|**smallint**|행의 최대 크기입니다.|  
|**maxirow**|**smallint**|리프가 아닌 인덱스 행의 최대 크기입니다.<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는 **maxirow** 이전 버전과 완전히 호환 되지 않습니다.|  
|**OrigFillFactor**|**tinyint**|인덱스가 만들어질 때 사용되는 원래 채우기 비율 값입니다. 이 값은 유지 관리되지 않지만 인덱스를 다시 만들어야 하거나 사용한 채우기 비율 값을 기억할 수 없는 경우에 유용합니다.|  
|**StatVersion**|**tinyint**|0을 반환합니다.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved2**|**int**|0을 반환합니다.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**FirstIAM**|**binary(6)**|NULL = 인덱스가 분할됩니다.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**impid**|**smallint**|인덱스 구현 플래그입니다.<br /><br /> 0을 반환합니다.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**lockflags**|**smallint**|인덱스에 대해 고려된 잠금 세분성을 제약하는 데 사용합니다. 예를 들어 잠금 비용을 최소화하기 위해 일반적으로 읽기 전용인 조회 테이블을 테이블 수준의 잠금만 수행하도록 설정할 수 있습니다.|  
|**pgmodctr**|**int**|0을 반환합니다.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**keys**|**varbinary(816)**|인덱스 키를 구성하는 열의 열 ID 목록입니다.<br /><br /> NULL을 반환합니다.<br /><br /> 인덱스 키 열을 표시 하려면 사용 하 여 [sys.sysindexkeys](../../relational-databases/system-compatibility-views/sys-sysindexkeys-transact-sql.md)합니다.|  
|**name**|**sysname**|인덱스 또는 통계의 이름입니다. NULL을 반환 **indid** = 0. 응용 프로그램을 수정하여 NULL 힙 이름을 찾습니다.|  
|**statblob**|**image**|통계 BLOB(Binary Large Object)입니다.<br /><br /> NULL을 반환합니다.|  
|**maxlen**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**rows**|**int**|기준 데이터 수준 행 개수 **indid** = 0 및 **indid** = 1, 및 값에 대해 반복 됩니다 **indid** > 1.|  
  
## <a name="remarks"></a>설명  
 예약된 것으로 정의된 열은 사용할 수 없습니다.  
  
 열 **dpages**를 **예약**, 및 **사용 되는** 테이블이 나 인덱스에 ROW_OVERFLOW 할당 단위의 데이터가 있으면 정확한 결과 반환 하지 것입니다. 또한 각 인덱스에 대한 페이지 수는 개별적으로 추적되고 기본 테이블에서 집계되지 않습니다. 페이지 수를 보려면 다음을 사용 합니다 [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) 또는 [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) 카탈로그 뷰 또는 [sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) 동적 관리 뷰.  
  
 SQL Server 2000 및 이전 버전에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 행 수준의 수정 카운터를 유지 관리했습니다. 이러한 카운터는 이제 열 수준에서 유지 관리됩니다. 따라서 합니다 **rowmodctr** 열 계산 되 고 이전 버전의 결과 유사 하지만 정확 하지 않은 결과 생성 합니다.  
  
 값을 사용 하는 경우 **rowmodctr** 통계 업데이트 시기를 확인 하려면 다음 방법을 고려 하십시오.  
  
-   아무 작업도 하지 않습니다. 새 **rowmodctr** 값을 자주 참조 동작 가장 이전 버전의 결과 근접 하기 때문에 통계 업데이트 시기를 확인할 수 있습니다.  
  
-   AUTO_UPDATE_STATISTICS를 사용합니다. 자세한 내용은 참조 하십시오 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
-   제한 시간을 사용하여 통계의 업데이트 시기를 결정합니다. 예를 들어 매시간, 매일 또는 매주로 정합니다.  
  
-   응용 프로그램 수준 정보를 사용하여 통계의 업데이트 시기를 결정합니다. 예를 들어, 매번의 최대값은 **identity** 열 여 10,000 개 이상의 변경 또는 대량 삽입 작업이 때마다 수행 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
