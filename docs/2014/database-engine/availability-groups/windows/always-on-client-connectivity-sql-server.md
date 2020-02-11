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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67793426"
---
# <a name="always-on-client-connectivity-sql-server"></a>Always On 클라이언트 연결(SQL Server)
  이 항목에서는 클라이언트 구성 및 설정에 대한 사전 요구 사항, 제한 사항 및 권장 사항을 비롯하여 AlwaysOn 가용성 그룹에 클라이언트를 연결할 때 고려해야 할 사항에 대해 설명합니다.  
  
 
  
##  <a name="ClientConnSupport"></a> 클라이언트 연결 지원  
 아래의 섹션에서는 클라이언트 연결에 대한 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 지원에 대해 설명합니다.  
  
 **드라이버 지원**  
  
 다음 표에는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 드라이버 지원이 요약되어 있습니다.  
  
|드라이버|다중 서브넷 장애 조치(Failover)|애플리케이션 의도|읽기 전용 라우팅|다중 서브넷 장애 조치(Failover): 보다 빠른 단일 서브넷 엔드포인트 장애 조치(Failover)|다중 서브넷 장애 조치(Failover): SQL 클러스터형 인스턴스에 대한 명명된 인스턴스 확인|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|yes|yes|yes|yes|yes|  
|SQL Native Client 11.0 OLEDB|예|yes|yes|예|예|  
|연결 패치를 사용 하는 .NET Framework 4.0 ADO.NET**<sup>*</sup>** |yes|yes|yes|yes|yes|  
|.NET Framework 3.5 s p 1과 연결 패치가 있는 ADO.NET**<sup>**</sup>** |yes|yes|yes|yes|yes|  
|SQL Server용 Microsoft JDBC Driver 4.0|yes|yes|yes|yes|yes|  
  
 **<sup>*</sup>**.NET Framework 4.0: [https://support.microsoft.com/kb/2600211](https://support.microsoft.com/kb/2600211)를 사용 하 여 ADO .net 용 연결 패치를 다운로드 합니다.  
  
 **<sup>**</sup>* * .NET Framework 3.5 SP1: [https://support.microsoft.com/kb/2654347](https://support.microsoft.com/kb/2654347)를 사용 하 여 ADO.NET에 대 한 연결 패치를 다운로드 합니다.  
  
> [!IMPORTANT]  
>  가용성 그룹 수신기에 연결하려면 클라이언트에서 TCP 연결 문자열을 사용해야 합니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  

  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [장애 조치 (Failover) 클러스터링 및 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server에 대 한 필수 조건, 제한 사항 및 권장 사항&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [고가용성 및 재해 복구를 위한 AlwaysOn 솔루션 가이드 Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=227600)   
 [SQL Server AlwaysOn 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](https://blogs.msdn.com/b/sqlalwayson/)   
 [Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 또는 Windows Server 2008 R2를 실행하는 컴퓨터에서 IPSec 연결을 다시 연결할 때 시간이 오래 지연 발생](https://support.microsoft.com/kb/980915)   
 [클러스터 서비스가 Windows Server 2008 R2에서 IPv6 IP 주소를 장애 조치하는 데 30초 정도 걸림(영문)](https://support.microsoft.com/kb/2578113)   
 [클러스터와 애플리케이션 서버 간에 라우터가 없는 경우 장애 조치(Failover) 작업이 느림](https://support.microsoft.com/kb/2582281)  
  
  
