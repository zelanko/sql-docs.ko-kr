---
title: 링 버퍼를 사용하여 가용성 그룹에 대한 상태 정보 얻기
description: SQL Server 링 버퍼를 사용하여 Always On 가용성 그룹에 대한 특정 진단 정보를 얻습니다.
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 47bb7a1a-c0a5-473c-a7db-d9f4bf3ee650
author: rothja
ms.author: jroth
manager: jroth
ms.openlocfilehash: c69412f5433af83642a0337e49b98b19ecdbce62
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66789512"
---
# <a name="use-ring-buffers-to-obtain-health-information-about-always-on-availability-groups"></a>링 버퍼를 사용하여 Always On 가용성 그룹에 대한 상태 정보 얻기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server 링 버퍼 또는 sys.dm_os_ring_buffers DMV(동적 관리 뷰)에서 일부 진단 Always On 가용성 그룹 정보를 얻을 수 있습니다. 링 버퍼는 내부 진단에 대한 SQL Server 시스템 내에서 SQL Server 시작 및 레코드 경고 중 생성됩니다. 지원되지 않지만 문제를 해결할 때 귀중한 정보를 여전히 추출할 수 있습니다. 이러한 링 버퍼는 SQL Server가 중단되거나 손상되었을 때 다른 진단의 원본을 제공합니다.  
  
 다음 T-SQL(Transact-SQL) 쿼리는 가용성 그룹 링 버퍼에서 모든 이벤트 레코드를 검색합니다.  
  
```sql  
SELECT * FROM sys.dm_os_ring_buffers WHERE ring_buffer_type LIKE '%HADR%'  
```  
  
 데이터를 보다 잘 관리할 수 있도록 하기 위해 날짜 및 링 버퍼 형식에 따라 데이터를 필터링합니다. 다음 쿼리는 오늘 발생한 지정된 링 버퍼에서 레코드를 검색합니다.  
  
```sql  
DECLARE @runtime datetime  
SET @runtime = GETDATE()  
SELECT CONVERT (varchar(30), @runtime, 121) as data_collection_runtime,   
DATEADD (ms, -1 * (inf.ms_ticks - ring.[timestamp]), GETDATE()) AS ring_buffer_record_time,   
ring.[timestamp] AS record_timestamp, inf.ms_ticks AS cur_timestamp, ring.*   
FROM sys.dm_os_ring_buffers ring  
CROSS JOIN sys.dm_os_sys_info inf where ring_buffer_type='<RING_BUFFER_TYPE>'  
```  
  
 각 레코드의 레코드 열은 XML 형식의 진단 데이터를 포함합니다. XML 데이터는 링 버퍼 형식 간에 다릅니다. 각 링 버퍼 형식에 대한 자세한 내용은 [가용성 그룹 링 버퍼 형식](#BKMK_RingBufferTypes)을 참조하세요. XML 데이터를 읽기 쉽게 하려면 원하는 XML 요소를 추출하여 T-SQL 쿼리를 사용자 지정해야 합니다. 예를 들어 다음 쿼리는 RING_BUFFER_HADRDBMGR_API 링 버퍼에서 모든 이벤트를 검색하고 별도 테이블 열로 XML 데이터의 형식을 지정합니다.  
  
```sql  
WITH hadr(ts, type, record) AS  
(  
  SELECT timestamp AS ts, ring_buffer_type AS type, CAST(record AS XML) AS record   
  FROM sys.dm_os_ring_buffers WHERE ring_buffer_type = 'RING_BUFFER_HADRDBMGR_API'  
)  
SELECT   
  ts,  
  type,  
  record.value('(./Record/@id)[1]','bigint') AS [Record ID],  
  record.value('(./Record/@time)[1]','bigint') AS [Time],  
  record.value('(./Record/HadrDbMgrAPI/dbId)[1]', 'bigint') AS [DBID],  
  record.value('(/Record/HadrDbMgrAPI/API)[1]', 'varchar(50)') AS [API],  
  record.value('(/Record/HadrDbMgrAPI/Action)[1]', 'varchar(50)') AS [Action],  
  record.value('(/Record/HadrDbMgrAPI/role)[1]', 'int') AS [Role],  
  record.value('(/Record/Stack)[1]', 'varchar(100)') AS [Call Stack]  
FROM hadr  
ORDER BY record.value('(./Record/@time)[1]','bigint') DESC  
GO  
```  
  
##  <a name="BKMK_RingBufferTypes"></a> 가용성 그룹 링 버퍼 형식  
 sys.dm_os_ring_buffers에 네 개의 가용성 그룹 링 버퍼가 있습니다. 다음 표는 링 버퍼 형식 및 각 링 버퍼 형식에 대한 레코드 열 내용의 샘플을 설명합니다.  
  
 **RING_BUFFER_HADRDBMGR_API**  
  
 발생했거나 발생 중인 레코드 상태 전환 상태 전환을 보는 경우 objectType 값에 특히 주의해야 합니다.  
  
```xml  
<Record id="11" type="RING_BUFFER_HADRDBMGR_STATE" time="860243">  
  <HadrDbMgrState>  
    <objectType>HadrUsers</objectType>  
    <currentState>HDbMState_Starting</currentState>  
    <proposedState>HDbMState_Started</proposedState>  
    <targetState>HDbMState_Started</targetState>  
    <legalTransition>Y</legalTransition>  
    <role>1</role>  
  </HadrDbMgrState>  
</Record>  
```  
  
 **RING_BUFFER_HADRDBMGR_STATE**  
  
 Always On 작업에서 생성된 레코드 내부 메서드 또는 함수 호출 시작 및 종료 지점 모두를 포함하여 일시 중단, 다시 시작 또는 역할 변경과 같은 정보를 표시할 수 있습니다.  
  
```xml  
<Record id="45" type="RING_BUFFER_HADRDBMGR_STATE" time="1723487912">  
  <HadrDbMgrState>  
    <dbId>5</dbId>  
    <objectType>HadrDbMgr</objectType>  
    <currentState>HDbMState_Starting</currentState>  
    <proposedState>HDbMState_Started</proposedState>  
    <targetState>HDbMState_Started</targetState>  
    <legalTransition>Y</legalTransition>  
    <role>2</role>  
  </HadrDbMgrState>  
</Record>  
```  
  
 **RING_BUFFER_HADRDBMGR_COMMIT**  
  
```xml  
<Record id="0" type="RING_BUFFER_HADRDBMGR_COMMIT" time="1723475368">  
  <HadrDbMgrCommitPolicy>  
    <dbId>5</dbId>  
    <replicaId>883a18f5-97d5-450f-8f8f-9983a4fa5299</replicaId>  
    <dbHardenPolicy>KillAll</dbHardenPolicy>  
    <dbSyncConfig>0x0</dbSyncConfig>  
    <syncPartnerCount>0</syncPartnerCount>  
    <minSyncPartnerConfig>0</minSyncPartnerConfig>  
    <partnerHardenPolicy>KillAll</partnerHardenPolicy>  
    <partnerSyncConfig>0x0</partnerSyncConfig>  
    <logBlock>0x0000000000000000</logBlock>  
    <leaseExpired>Y</leaseExpired>  
    <partnerChange>N</partnerChange>  
    <role>2</role>  
  </HadrDbMgrCommitPolicy>  
</Record>  
```  
  
 **RING_BUFFER_HADR_TRANSPORT_STATE**  
  
```xml  
<Record id="3" type="RING_BUFFER_HADR_TRANSPORT_STATE" time="1723485399">  
  <HadrTransportState>  
    <agId>08264B79-D10B-412F-B38D-CA07B08E9BD8</agId>  
    <localArId>883A18F5-97D5-450F-8F8F-9983A4FA5299</localArId>  
    <targetArId>628D6349-72DD-4D18-A6E1-1272645660BA</targetArId>  
    <currentState>HadrSession_Configuring</currentState>  
    <targetState>HadrSession_Connected</targetState>  
    <legalTransition>Y</legalTransition>  
  </HadrTransportState>  
</Record>  
```  
  
## <a name="parse-xml-data-from-a-ring-buffer"></a>링 버퍼에서 XML 데이터 구문 분석  
 쿼리에서 [값&#40;&#41; 메서드&#40;xml 데이터 형식&#41;](~/t-sql/xml/value-method-xml-data-type.md)을 사용하여 검사하는 링 버퍼에서 레코드 필드를 구문 분석할 수 있습니다. 이 메서드를 사용하려면 먼저 링 버퍼의 레코드 열을 XML로 [캐스팅](~/t-sql/functions/cast-and-convert-transact-sql.md)해야 합니다. 예를 들어 아래 쿼리는 RING_BUFFER_HADRDBMGR_API를 이 메서드를 사용하여 읽을 수 있는 형식으로 구문 분석하는 방법을 보여줍니다.  
  
```sql 
WITH hadr(ts, type, record) AS  
   (SELECT timestamp AS ts, ring_buffer_type AS type, CAST(record AS XML) AS record   
FROM sys.dm_os_ring_buffers   
WHERE ring_buffer_type = 'RING_BUFFER_HADRDBMGR_API')  
SELECT ts,  
type,  
record.value('(./Record/@id)[1]','bigint') AS [Record id],  
record.value('(./Record/@time)[1]','bigint') AS [Time],  
record.value('(./Record/HadrDbMgrAPI/dbId)[1]', 'bigint') AS [dbid],  
record.value('(/Record/HadrDbMgrAPI/API)[1]', 'varchar(50)') AS [API],  
record.value('(/Record/HadrDbMgrAPI/Action)[1]', 'varchar(50)') AS [Action],  
record.value('(/Record/HadrDbMgrAPI/role)[1]', 'int') AS [Role],  
record.value('(/Record/Stack)[1]', 'varchar(100)') AS [Call Stack]  
FROM hadr  
ORDER BY record.value('(./Record/@time)[1]','bigint') DESC  
GO  
```  
  
  
