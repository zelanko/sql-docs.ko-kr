---
title: sys.server_resource_stats (Azure SQL Database) | Microsoft Docs
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
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 2a0a1f82685cb107902c8065f2f696f615ad3930
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2019
ms.locfileid: "58566512"
---
# <a name="sysserverresourcestats-azure-sql-database"></a>sys.server_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Azure SQL 관리 되는 인스턴스의 CPU 사용량, IO 및 storage 데이터를 반환합니다. 데이터는 5분 간격 이내로 수집 및 집계됩니다. 보고 15 초 마다 한 행씩이 있습니다. 반환 되는 데이터는 CPU 사용량, 저장소 크기, IO 사용률 및 관리 되는 인스턴스 SKU 포함 합니다. 기록 데이터는 약 14일 동안 보존됩니다.

합니다 **sys.server_resource_stats** 보기에는 데이터베이스와 연결 된 Azure SQL 관리 되는 인스턴스의 버전에 따라 다른 정의가 포함 됩니다. 이러한 차이점과 새 서버 버전으로 업그레이드할 경우 응용 프로그램에 필요한 모든 수정 사항을 고려하세요.
 
  
 다음 표에는 v12 서버에서 사용할 수 있는 열이 설명되어 있습니다.  
  
|열|데이터 형식|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|15 초 보고 간격의 시작을 나타내는 UTC 시간|  
|end_time|**datetime**|15 초 보고 간격의 끝을 나타내는 UTC 시간|
|resource_type|Nvarchar(128)|메트릭에 제공 되는 리소스의 형식|
|resource_name|nvarchar(128)|리소스의 이름입니다.|
|sku|nvarchar(128)|인스턴스의 인스턴스 서비스 계층을 관리 합니다. 가능한 값은 다음과 같습니다. <br><ul><li>범용</li></ul><ul><li>중요 비즈니스용</li></ul>|
|hardware_generation|nvarchar(128)|하드웨어 세대 식별자: Gen 4 또는 Gen 5 등|
|virtual_core_count|ssNoversion|(8, 16 또는 24 공개 미리 보기로 제공) 인스턴스 당 가상 코어 수를 나타냅니다.|
|avg_cpu_percent|decimal(5,2)|인스턴스에서 사용 하는 관리 되는 인스턴스 서비스 계층 한도의 백분율로 평균 계산 사용률입니다. 인스턴스의 모든 데이터베이스에 대 한 모든 리소스 풀의 CPU 시간의 합계 계산 이며 지정된 된 간격에 해당 계층에 대 한 사용 가능한 CPU 시간으로 나눈 값입니다.|
|reserved_storage_mb|BIGINT|예약 인스턴스 당 저장소 (저장소 공간 관리 되는 인스턴스에 대 한 구매 고객)|
|storage_space_used_mb|decimal(18,2)|모든 관리 되는 인스턴스 데이터베이스의 파일 (데이터베이스 사용자와 시스템 데이터베이스 포함)에서 사용 된 저장소|
|io_request|BIGINT|총 i/o 간격 내에서 실제 작업|
|io_bytes_read|BIGINT|간격 내에서 읽은 실제 바이트 수|
|io_bytes_written|BIGINT|간격 내에 기록 하는 실제 바이트 수|

 
> [!TIP]  
>  이러한 제한 및 서비스 계층에 대 한 더 많은 컨텍스트 항목을 참조 하세요 [관리 되는 인스턴스 서비스 계층](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tier)합니다.  
    
## <a name="permissions"></a>사용 권한  
 이 보기는 연결할 수 있는 권한이 있는 모든 사용자 역할에 사용할 수는 **마스터** 데이터베이스입니다.  
  
## <a name="remarks"></a>Remarks  
 반환한 데이터 **sys.server_resource_stats** 이외의 avg_cpu 최대 허용 되는 서비스에 대 한 한도의 백분율로 표현 된 바이트 또는 메가바이트 (열 이름에 명시)에 사용 되는 총으로 표현 됩니다 실행 중인 계층/성능 수준입니다.  
 
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
    
## <a name="see-also"></a>관련 항목  
 [인스턴스 서비스 계층 관리](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tier)
