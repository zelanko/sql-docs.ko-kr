---
title: sys.bandwidth_usage (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- bandwidth_usage
- sys.bandwidth_usage
- bandwidth_usage_TSQL
- sys.bandwidth_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.bandwidth_usage
- bandwidth_usage
ms.assetid: 43ed8435-f059-4907-b5c0-193a258b394a
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 046e9e651daeb2946538ff5ae269aaad27666fd0
ms.sourcegitcommit: 97340deee7e17288b5eec2fa275b01128f28e1b8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55421310"
---
# <a name="sysbandwidthusage-azure-sql-database"></a>sys.bandwidth_usage(Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

> [!NOTE]
> 이만 적용 됩니다 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11.* *  
  
 각 데이터베이스에 사용 되는 네트워크 대역폭에 대 한 정보를 반환 합니다는  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11 데이터베이스 서버**합니다. 지정된 데이터베이스에 대해 반환된 각 행에는 1시간 동안 이루어진 단일 방향 및 클래스 사용이 요약되어 있습니다.  
  
 **이 사용 되지를 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]입니다.**  
  
 합니다 **sys.bandwidth_usage** 뷰는 다음 열을 포함 합니다.  
  
|Column Name|Description|  
|-----------------|-----------------|  
|**time**|대역폭을 소비하는 시간입니다. 이 뷰의 행은 시간당 기준입니다. 예를 들어 2009-09-19 02:00:00.000은 2009년 9월 19일 오전 2시부터 오전 3시까지 소비한 대역폭을 의미합니다.|  
|**database_name**|대역폭을 사용한 데이터베이스의 이름입니다.|  
|**direction**|사용된 대역폭의 유형은 다음 중 하나입니다.<br /><br /> 수신: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]로 들어오는 데이터입니다.<br /><br /> 송신: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 나가는 데이터입니다.|  
|**class**|사용된 대역폭의 클래스는 다음 중 하나입니다.<br />내부: Azure 플랫폼 내에서 이동하는 데이터입니다.<br />외부: Azure 플랫폼에서 나가는 데이터입니다.<br /><br /> 이 클래스는 데이터베이스가 지역 간의 연속 복사 관계([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)])에 참여하는 경우에만 반환됩니다. 지정된 된 데이터베이스가 연속 복사 관계에 참여 하지 않습니다, 경우에 "Interlink" 행 반환 되지 않습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "주의" 섹션을 참조하세요.|  
|**time_period**|사용이 발생 하는 기간에는 최대 또는 OffPeak입니다. 피크 시간은 서버 제조 지역을 기준으로 합니다. 예를 들어, 'US_Northwest' 지역에서 만든 서버인 경우 피크 시간은 태평양 표준시로 오전 10시에서 오후 6시 사이로 정의됩니다.|  
|**quantity**|사용된 대역폭 양입니다(KB).|  
  
## <a name="permissions"></a>사용 권한

 이 보기는 에서만 사용할 수는 **마스터** 데이터베이스 서버 수준 보안 주체 로그인 합니다.  
  
## <a name="remarks"></a>Remarks  
  
### <a name="external-and-internal-classes"></a>External 및 Internal 클래스

 지정된 된 시간에 사용 되는 각 데이터베이스는 **sys.bandwidth_usage** 뷰 클래스와 대역폭 사용량의 방향을 표시 하는 행을 반환 합니다. 다음 예에서는 지정된 데이터베이스에 대해 노출될 수 있는 데이터를 보여 줍니다. 이 예에서 시간은 2012-04-21 17:00:00이고 피크 시간 중에 발생합니다. 데이터베이스 이름은 Db1입니다. 이 예에서 **sys.bandwidth_usage** 다음과 같이 Ingress 및 Egress 방향과 External 및 Internal 클래스의 모든 4 가지 조합에 대 한 행을 반환 했습니다.  
  
|Time|database_name|direction|class|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Ingress|External|Peak|66|  
|2012-04-21 17:00:00|Db1|송신|External|Peak|741|  
|2012-04-21 17:00:00|Db1|수신|Internal|Peak|1052|  
|2012-04-21 17:00:00|Db1|Egress|내부|Peak|3525|  
  
### <a name="interpreting-data-direction-for-includessgeodrincludesssgeodr-mdmd"></a>[!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]에 대한 데이터 방향 해석

 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]의 경우 논리 master 데이터베이스의 양쪽 연속 복사 관계에 대역폭 사용 데이터가 표시됩니다. 따라서 해석 하 고 송신 방향 지표 쿼리 하는 데이터베이스의 관점에서 해야 합니다. 예를 들어 복제 스트림을 대상 서버에 원본 서버에서 1 MB의 데이터를 전송 하는 것이 좋습니다. 이 경우 원본 서버에서 1 MB 수에 합산 전송 된 총 데이터 하 고 대상 서버에서 1 MB는 수신 된 데이터로 기록 됩니다.  
  
> [!NOTE]  
> 전송된 다량의 데이터는 사용자 데이터 흐름의 방향으로 원본 서버에서 대상 서버로 전송된 것입니다. 그러나 경우에 따라 다른 방향으로 전송해야 하는 데이터 전송도 있습니다.  
