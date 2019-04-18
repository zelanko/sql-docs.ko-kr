---
title: sys.dm_tcp_listener_states (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tcp_listener_states
- dm_tcp_listener_states
- sys.dm_tcp_listener_states_TSQL
- dm_tcp_listener_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.dm_tcp_listener_states dynamic management view
ms.assetid: 9997ffed-a4c1-428f-8bac-3b9e4b16d7cf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f45c634b2a5ab057fd9c2ae878e544a6b7d84f7f
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59671349"
---
# <a name="sysdmtcplistenerstates-transact-sql"></a>sys.dm_tcp_listener_states(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  각 TCP 수신기에 대한 동적 상태 정보를 포함하는 행을 반환합니다.  
  
> [!NOTE]
> 가용성 그룹 수신기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 수신기와 동일한 포트를 수신할 수 있습니다. 이 경우 수신기는 별도로 나열되며 Service Broker 수신기의 경우와 동일합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**listener_id**|**int**|수신기의 내부 id입니다. Null을 허용하지 않습니다.<br /><br /> 기본 키입니다.|  
|**ip_address**|**nvarchar(48)**|온라인 상태이고 현재 수신 중인 수신기 IP 주소입니다. IPv4 및 IPv6가 허용됩니다. 수신기에서 두 주소 유형을 모두 처리하는 경우 별도로 나열됩니다. IPv4 와일드 카드 이며 "0.0.0.0"으로 표시 됩니다. 으로 표시 되는 IPv6 와일드 카드 ":".<br /><br /> Null을 허용하지 않습니다.|  
|**is_ipv4**|**bit**|IP 주소 유형<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
|**port**|**int**|수신기가 수신 중인 포트 번호입니다. Null을 허용하지 않습니다.|  
|**type**|**tinyint**|수신기 유형이며 다음 중 하나입니다.<br /><br /> 0 = [!INCLUDE[tsql](../../includes/tsql-md.md)]<br /><br /> 1 = Service Broker<br /><br /> 2 = 데이터베이스 미러링<br /><br /> Null을 허용하지 않습니다.|  
|**type_desc**|**nvarchar(20)**|설명은 합니다 **형식**하나씩의:<br /><br /> TSQL<br /><br /> SERVICE_BROKER<br /><br /> DATABASE_MIRRORING<br /><br /> Null을 허용하지 않습니다.|  
|**state**|**tinyint**|가용성 그룹 수신기의 상태이며 다음 중 하나입니다.<br /><br /> 1 = 온라인. 수신기가 요청을 수신 및 처리 중입니다.<br /><br /> 2 = 다시 시작 보류 중. 수신기가 오프라인 상태이며 다시 시작을 보류 중입니다.<br /><br /> 가용성 그룹 수신기가 서버 인스턴스와 동일한 포트를 수신 중인 경우 두 수신기의 상태는 항상 동일합니다.<br /><br /> Null을 허용하지 않습니다.<br /><br /> 참고: 이 열의 값 TSD_listener 개체에서 제공 됩니다. 열을 TDS_listener 오프 라인 상태 이면 상태에 대해 쿼리할 수 없습니다 때문에 오프 라인 상태를 지원 하지 않습니다.|  
|**state_desc**|**nvarchar(16)**|에 대 한 설명을 **상태**하나씩입니다.<br /><br /> ONLINE<br /><br /> PENDING_RESTART<br /><br /> Null을 허용하지 않습니다.|  
|**start_time**|**datetime**|수신기가 시작된 시간을 나타내는 타임스탬프입니다. Null을 허용하지 않습니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [AlwaysOn 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Always On 가용성 그룹 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
