---
title: server_resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.service: sql-database
ms.reviewer: carlrab, edmaca
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 72e363b05e8f14dda535abd70e4218c949c42c91
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68133067"
---
# <a name="sysserver_resource_stats-azure-sql-database"></a>server_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Azure SQL Managed Instance에 대 한 CPU 사용량, IO 및 저장소 데이터를 반환 합니다. 데이터는 5분 간격 이내로 수집 및 집계됩니다. 15 초 보고 마다 하나의 행이 있습니다. 반환 되는 데이터에는 CPU 사용량, 저장소 크기, IO 사용률 및 관리 되는 인스턴스 SKU가 포함 됩니다. 기록 데이터는 약 14일 동안 보존됩니다.

**Server_resource_stats** 뷰는 데이터베이스가 연결 된 Azure SQL 관리 되는 인스턴스의 버전에 따라 다른 정의가 있습니다. 이러한 차이점과 새 서버 버전으로 업그레이드할 경우 애플리케이션에 필요한 모든 수정 사항을 고려하세요.
 
  
 다음 표에는 v12 서버에서 사용할 수 있는 열이 설명되어 있습니다.  
  
|열|데이터 형식|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|15 초 보고 간격의 시작을 나타내는 UTC 시간입니다.|  
|end_time|**datetime**|15 초 보고 간격의 끝을 나타내는 UTC 시간입니다.|
|resource_type|Nvarchar(128)|메트릭이 제공 되는 리소스의 유형입니다.|
|resource_name|nvarchar(128)|리소스의 이름입니다.|
|sku|nvarchar(128)|인스턴스의 서비스 계층을 Managed Instance 합니다. 가능한 값은 다음과 같습니다. <br><ul><li>범용</li></ul><ul><li>중요 비즈니스용</li></ul>|
|hardware_generation|nvarchar(128)|하드웨어 생성 식별자 (예: Gen 4 또는 Gen 5)|
|virtual_core_count|int|인스턴스당 가상 코어 수를 나타냅니다 (공개 미리 보기에서 8, 16 또는 24).|
|avg_cpu_percent|decimal (5, 2)|인스턴스가 사용 하는 Managed Instance 서비스 계층 한도의 백분율로 나타낸 평균 계산 사용률입니다. 인스턴스의 모든 데이터베이스에 대 한 모든 리소스 풀의 CPU 시간 합계를 계산 하 고 지정 된 간격으로 해당 계층의 사용 가능한 CPU 시간으로 나눈 값을 계산 합니다.|
|reserved_storage_mb|bigint|인스턴스당 예약 된 저장소 (고객이 관리 되는 인스턴스에 대해 구매한 저장소 공간 크기)|
|storage_space_used_mb|decimal (18, 2)|모든 관리 되는 인스턴스 데이터베이스 파일 (사용자 및 시스템 데이터베이스 포함)에서 사용 하는 저장소|
|io_request|bigint|간격 내에 있는 총 i/o 물리적 작업 수입니다.|
|io_bytes_read|bigint|간격 내에서 읽은 실제 바이트 수|
|io_bytes_written|bigint|간격 내에 쓰여진 실제 바이트 수|

 
> [!TIP]  
>  이러한 제한 및 서비스 계층에 대 한 자세한 컨텍스트는 [서비스 계층 Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)항목을 참조 하세요.  
    
## <a name="permissions"></a>사용 권한  
 이 보기는 **master** 데이터베이스에 연결할 수 있는 권한이 있는 모든 사용자 역할에 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **Server_resource_stats** 에서 반환 되는 데이터는 실행 중인 서비스 계층/성능 수준에 대해 허용 되는 최대 한도의 백분율로 표시 되는 바이트 또는 메가바이트 (열 이름에 표시 됨 avg_cpu)에서 사용 되는 합계로 표시 됩니다.  
 
## <a name="examples"></a>예  
 다음 예에서는 지난 1주일 동안 평균적으로 컴퓨팅 활용률의 80% 이상을 사용한 모든 데이터베이스를 반환합니다.  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT resource_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.server_resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY resource_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>참고 항목  
 [Managed Instance 서비스 계층](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)
