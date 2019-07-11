---
title: Always On 클라이언트 연결(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: d8a1b81d60ef691e02d4b69cc71fa961bbaddf18
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793426"
---
# <a name="always-on-client-connectivity-sql-server"></a>Always On 클라이언트 연결(SQL Server)
  이 항목에서는 클라이언트 구성 및 설정에 대한 사전 요구 사항, 제한 사항 및 권장 사항을 비롯하여 AlwaysOn 가용성 그룹에 클라이언트를 연결할 때 고려해야 할 사항에 대해 설명합니다.  
  
 
  
##  <a name="ClientConnSupport"></a> 클라이언트 연결 지원  
 아래의 섹션에서는 클라이언트 연결에 대한 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대해 설명합니다.  
  
 **드라이버 지원**  
  
 다음 표에는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 드라이버 지원이 요약되어 있습니다.  
  
|드라이버|다중 서브넷 장애 조치(Failover)|애플리케이션 의도|읽기 전용 라우팅|다중 서브넷 장애 조치(failover): 보다 빠른 단일 서브넷 엔드포인트 장애 조치(Failover)|다중 서브넷 장애 조치(failover): SQL 클러스터형 인스턴스에 대한 명명된 인스턴스 확인|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|예|예|예|예|예|  
|SQL Native Client 11.0 OLEDB|아니오|예|예|아니오|아니요|  
|연결 패치가 포함 된.NET Framework 4.0이 있는 ADO.NET **<sup>*</sup>** |사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|  
|연결 패치가 포함 된.NET Framework 3.5 SP1이 있는 ADO.NET **<sup>** </sup>** |사용자 계정 컨트롤|예|예|예|예|  
|SQL Server용 Microsoft JDBC Driver 4.0|예|예|예|예|사용자 계정 컨트롤|  
  
 **<sup>*</sup>**  .NET Framework 4.0이 있는 ADO.NET 용 연결 패치 다운로드: [ https://support.microsoft.com/kb/2600211 ](https://support.microsoft.com/kb/2600211)합니다.  
  
 **<sup>** </sup>* *.NET Framework 3.5 SP1이 있는 ADO.NET 용 연결 패치 다운로드: [ https://support.microsoft.com/kb/2654347 ](https://support.microsoft.com/kb/2654347)합니다.  
  
> [!IMPORTANT]  
>  가용성 그룹 수신기에 연결하려면 클라이언트에서 TCP 연결 문자열을 사용해야 합니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  

  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [장애 조치 클러스터링 및 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [필수 구성 요소, 제한 사항 및 AlwaysOn 가용성 그룹에 대 한 권장 사항 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Microsoft SQL Server AlwaysOn 솔루션 가이드 고가용성 및 재해 복구](https://go.microsoft.com/fwlink/?LinkId=227600)   
 [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](https://blogs.msdn.com/b/sqlalwayson/)   
 [Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 또는 Windows Server 2008 R2를 실행하는 컴퓨터에서 IPSec 연결을 다시 연결할 때 시간이 오래 지연 발생](https://support.microsoft.com/kb/980915)   
 [클러스터 서비스가 Windows Server 2008 R2에서 IPv6 IP 주소를 장애 조치하는 데 30초 정도 걸림(영문)](https://support.microsoft.com/kb/2578113)   
 [클러스터와 애플리케이션 서버 간에 라우터가 없는 경우 장애 조치(Failover) 작업이 느림](https://support.microsoft.com/kb/2582281)  
  
  
