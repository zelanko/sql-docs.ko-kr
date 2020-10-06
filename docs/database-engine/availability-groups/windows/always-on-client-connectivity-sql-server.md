---
title: 가용성 그룹에 대한 드라이버 및 클라이언트 연결 지원
description: '이 항목에서는 클라이언트 구성 및 설정에 대한 사전 요구 사항, 제한 사항 및 권장 사항을 비롯하여 Always On 가용성 그룹에 클라이언트를 연결할 때 고려해야 할 사항에 대해 설명합니다. '
ms.custom: seodec18
ms.date: 07/28/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], client connectivity
ms.assetid: b456448d-1757-48c8-8bbb-2d1c2d6d61e9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 10517361b14711595b08a2c4761a368666b764b1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726574"
---
# <a name="driver-and-client-connectivity-support-for-availability-groups"></a>가용성 그룹에 대한 드라이버 및 클라이언트 연결 지원
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 클라이언트 구성 및 설정에 대한 사전 요구 사항, 제한 사항 및 권장 사항을 비롯하여 Always On 가용성 그룹에 클라이언트를 연결할 때 고려해야 할 사항에 대해 설명합니다.  
  
 
##  <a name="client-connectivity-support"></a><a name="ClientConnSupport"></a> 클라이언트 연결 지원  
 아래의 섹션에서는 클라이언트 연결에 대한 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대해 설명합니다.  
  
 **드라이버 지원**  
  
 다음 표에는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 드라이버 지원이 요약되어 있습니다.  
  
|드라이버|다중 서브넷 장애 조치(Failover)|애플리케이션 의도|읽기 전용 라우팅|다중 서브넷 장애 조치(Failover): 보다 빠른 단일 서브넷 엔드포인트 장애 조치(Failover)|다중 서브넷 장애 조치(Failover): SQL 클러스터형 인스턴스에 대한 명명된 인스턴스 확인|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|yes|yes|yes|yes|yes|  
|SQL Native Client 11.0 OLEDB|예|yes|yes|예|예|  
|연결 패치가 포함된 .NET Framework 4.0이 있는 ADO.NET*|yes|yes|yes|yes|yes|  
|연결 패치가 포함된 .NET Framework 3.5 SP1이 있는 ADO.NET**|yes|yes|yes|yes|yes|  
|[Microsoft ODBC Driver 13.1+ for SQL Server](../../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)|yes|yes|yes|yes|yes|
|[Microsoft JDBC Driver 4.0+ for SQL Server](../../../connect/jdbc/microsoft-jdbc-driver-for-sql-server.md)|yes|yes|yes|yes|yes| 
|[SQL Server용 Microsoft OLE DB 드라이버](../../../connect/oledb/oledb-driver-for-sql-server.md)|예|예|예|예|예| 
  
 *.NET Framework 4.0: [https://support.microsoft.com/kb/2600211](https://support.microsoft.com/kb/2600211)이 있는 ADO.NET용 연결 패치를 다운로드합니다.  
  
 **.NET Framework 3.5 SP1: [https://support.microsoft.com/kb/2654347](https://support.microsoft.com/kb/2654347)이 있는 ADO.NET용 연결 패치를 다운로드합니다.  
 
 *SQL Server용 Microsoft OLE DB 드라이버를 다운로드합니다: [https://aka.ms/downloadmsoledbsql](../../../connect/oledb/download-oledb-driver-for-sql-server.md).  

> [!IMPORTANT]  
>  가용성 그룹 수신기에 연결하려면 클라이언트에서 TCP 연결 문자열을 사용해야 합니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [장애 조치(failover) 클러스터링 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드(영문)](/previous-versions/sql/sql-server-2012/hh781257(v=msdn.10))   
 [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](/archive/blogs/sqlalwayson/)   
 [Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 또는 Windows Server 2008 R2를 실행하는 컴퓨터에서 IPSec 연결을 다시 연결할 때 시간이 오래 지연 발생](https://support.microsoft.com/kb/980915)   
 [클러스터 서비스가 Windows Server 2008 R2에서 IPv6 IP 주소를 장애 조치하는 데 30초 정도 걸림(영문)](https://support.microsoft.com/kb/2578113)   
 [클러스터와 애플리케이션 서버 간에 라우터가 없는 경우 장애 조치(Failover) 작업이 느림](https://support.microsoft.com/kb/2582281)  
  
