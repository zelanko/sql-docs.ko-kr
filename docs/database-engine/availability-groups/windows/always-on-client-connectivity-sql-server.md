---
title: "Always On 클라이언트 연결(SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "가용성 그룹 [SQL Server], 수신기"
  - "가용성 그룹 [SQL Server], 필수 구성 요소 및 제한 사항"
  - "가용성 그룹 [SQL Server], 클라이언트 연결"
ms.assetid: b456448d-1757-48c8-8bbb-2d1c2d6d61e9
caps.latest.revision: 22
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 21
---
# Always On 클라이언트 연결(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 클라이언트 구성 및 설정에 대한 사전 요구 사항, 제한 사항 및 권장 사항을 비롯하여 Always On 가용성 그룹에 클라이언트를 연결할 때 고려해야 할 사항에 대해 설명합니다.  
  
 **항목 내용**  
  
-   [클라이언트 연결 지원](#ClientConnSupport)  
  
-   [관련 태스크](#RelatedTasks)  
  
##  <a name="ClientConnSupport"></a> 클라이언트 연결 지원  
 아래의 섹션에서는 클라이언트 연결에 대한 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대해 설명합니다.  
  
 **드라이버 지원**  
  
 다음 표에는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 드라이버 지원이 요약되어 있습니다.  
  
|드라이버|다중 서브넷 장애 조치(Failover)|응용 프로그램 의도|읽기 전용 라우팅|다중 서브넷 장애 조치(Failover): 보다 빠른 단일 서브넷 끝점 장애 조치(Failover)|다중 서브넷 장애 조치(Failover): SQL 클러스터형 인스턴스에 대한 명명된 인스턴스 확인|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|예|예|예|예|예|  
|SQL Native Client 11.0 OLEDB|아니요|예|예|아니요|아니요|  
|연결 패치가 포함된 .NET Framework 4.0이 있는 ADO.NET*|예|예|예|예|예|  
|연결 패치가 포함된 .NET Framework 3.5 SP1이 있는 ADO.NET**|예|예|예|예|예|  
|SQL Server용 Microsoft JDBC Driver 4.0|예|예|예|예|예|  
  
 *.NET Framework 4.0이 있는 ADO.NET용 연결 패치 다운로드: [http://support.microsoft.com/kb/2600211](http://support.microsoft.com/kb/2600211)  
  
 **.NET Framework 3.5 SP1이 있는 ADO.NET용 연결 패치 다운로드: [http://support.microsoft.com/kb/2654347](http://support.microsoft.com/kb/2654347)  
  
> [!IMPORTANT]  
>  가용성 그룹 수신기에 연결하려면 클라이언트에서 TCP 연결 문자열을 사용해야 합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
## 참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [장애 조치(failover) 클러스터링 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners, client connectivity, application failover.md)   
 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](http://go.microsoft.com/fwlink/?LinkId=227600)   
 [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](http://blogs.msdn.com/b/sqlAlways%20On/)   
 [Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 또는 Windows Server 2008 R2를 실행 중인 컴퓨터에서 IPSec를 다시 연결할 때 긴 시간 지연 발생](http://support.microsoft.com/kb/980915)   
 [클러스터 서비스가 Windows Server 2008 R2에서 IPv6 IP 주소를 장애 조치하는 데 30초 정도 걸림](http://support.microsoft.com/kb/2578113)   
 [클러스터와 응용 프로그램 서버 사이에 라우터가 없는 경우 장애 조치(Failover) 작업이 느려짐](http://support.microsoft.com/kb/2582281)  
  
  