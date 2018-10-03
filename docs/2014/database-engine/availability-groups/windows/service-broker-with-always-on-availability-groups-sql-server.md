---
title: Service Broker AlwaysOn 가용성 그룹 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Service Broker, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 881c20e5-1c99-44eb-b393-09fc5ea0f122
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2758227de47509e62c9f7874c70bbcf30e01d364
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191093"
---
# <a name="service-broker-with-alwayson-availability-groups-sql-server"></a>AlwaysOn 가용성 그룹이 포함된 Service Broker(SQL Server)
  이 항목에서는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]과 함께 작동하도록 Service Broker를 구성하는 방법에 대한 정보를 제공합니다.  
  
 **항목 내용:**  
  
-   [가용성 그룹의 서비스가 원격 메시지를 받기 위한 요구 사항](#ReceiveRemoteMessages)  
  
-   [가용성 그룹의 원격 서비스에 메시지를 보내기 위한 요구 사항](#SendRemoteMessages)  
  
##  <a name="ReceiveRemoteMessages"></a> 가용성 그룹의 서비스가 원격 메시지를 받기 위한 요구 사항  
  
1.  **가용성 그룹에 수신기가 있는지 확인합니다.**  
  
     자세한 내용은 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
2.  **Service Broker 엔드포인트가 존재하고 올바르게 구성되어 있는지 확인합니다.**  
  
     가용성 그룹에 대한 가용성 복제본을 호스팅하는 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 다음과 같이 Service Broker 엔드포인트를 구성해야 합니다.  
  
    -   LISTENER_IP를 'ALL'로 설정합니다. 이 설정을 사용하면 가용성 그룹 수신기에 바인딩된 모든 유효한 IP 주소에서 연결이 가능해집니다.  
  
    -   모든 호스트 서버 인스턴스에서 Service Broker 포트를 동일한 포트 번호로 설정합니다.  
  
        > [!TIP]  
        >  특정 서버 인스턴스에서 Service Broker 엔드포인트의 포트 번호를 보려면 **sys.tcp_endpoints** 카탈로그 뷰의 [port](/sql/relational-databases/system-catalog-views/sys-tcp-endpoints-transact-sql) 열을 쿼리합니다. 여기서 **type_desc** = 'SERVICE_BROKER'입니다.  
  
     다음 예에서는 기본 Service Broker 포트(4022)를 사용하며 모든 유효한 IP 주소를 수신하는 Windows 인증 Service Broker 엔드포인트를 만듭니다.  
  
    ```  
    CREATE ENDPOINT [SSBEndpoint]  
        STATE = STARTED  
        AS TCP  (LISTENER_PORT = 4022, LISTENER_IP = ALL )  
        FOR SERVICE_BROKER (AUTHENTICATION = WINDOWS)  
    ```  
  
     자세한 내용은 [CREATE ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)과 함께 작동하도록 Service Broker를 구성하는 방법에 대한 정보를 제공합니다.  
  
3.  **엔드포인트에 대한 CONNECT 권한을 부여합니다.**  
  
     Service Broker 엔드포인트에 대한 CONNECT 권한을 PUBLIC 또는 로그인으로 부여합니다.  
  
     다음 예에서는 `broker_endpoint`라는 Service Broker 엔드포인트에 대한 연결을 PUBLIC으로 부여합니다.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[broker_endpoint] TO [PUBLIC]  
    ```  
  
     자세한 내용은 [GRANT&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)과 함께 작동하도록 Service Broker를 구성하는 방법에 대한 정보를 제공합니다.  
  
4.  **msdb에 AutoCreatedLocal 경로 또는 특정 서비스에 대한 경로가 포함되어 있는지 확인합니다.**  
  
    > [!NOTE]  
    >  기본적으로 **msdb**를 비롯하여 각 사용자 데이터베이스에는 **AutoCreatedLocal**경로가 포함되어 있습니다. 이 경로는 임의의 서비스 이름 및 Broker 인스턴스와 일치하며 메시지가 현재 인스턴스 내에 배달되도록 지정합니다. **AutoCreatedLocal** 의 우선 순위는 원격 인스턴스와 통신하는 특정 서비스를 명시적으로 지정하는 경로의 우선 순위보다 낮습니다.  
  
     경로를 만드는 방법은 [버전의 온라인 설명서에 있는](http://msdn.microsoft.com/library/ms166090\(SQL.105\).aspx) Service Broker 라우팅 예 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 및 [CREATE ROUTE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-route-transact-sql)과 함께 작동하도록 Service Broker를 구성하는 방법에 대한 정보를 제공합니다.  
  
##  <a name="SendRemoteMessages"></a> 가용성 그룹의 원격 서비스에 메시지를 보내기 위한 요구 사항  
  
1.  **대상 서비스에 대한 경로를 만듭니다.**  
  
     다음과 같이 경로를 구성합니다.  
  
    -   ADDRESS를 서비스 데이터베이스를 호스팅하는 가용성 그룹의 수신기 IP 주소로 설정합니다.  
  
    -   PORT를 각 원격 SQL Server 인스턴스의 Service Broker 엔드포인트에 지정한 포트로 설정합니다.  
  
     다음 예에서는 `RouteToTargetService` 서비스에 대해 `ISBNLookupRequestService` 라는 경로를 만듭니다. 이 경로는 포트 4022를 사용하는 가용성 그룹 수신기 `MyAgListener`를 대상으로 합니다.  
  
    ```  
    CREATE ROUTE [RouteToTargetService] WITH   
    SERVICE_NAME = 'ISBNLookupRequestService',   
    ADDRESS = 'TCP://MyAgListener:4022';  
  
    ```  
  
     자세한 내용은 [CREATE ROUTE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-route-transact-sql)과 함께 작동하도록 Service Broker를 구성하는 방법에 대한 정보를 제공합니다.  
  
2.  **msdb에 AutoCreatedLocal 경로 또는 특정 서비스에 대한 경로가 포함되어 있는지 확인합니다.** 자세한 내용은 이 항목의 앞부분에 나오는 [가용성 그룹의 서비스가 원격 메시지를 받기 위한 요구 사항](#ReceiveRemoteMessages)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [CREATE ENDPOINT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
-   [CREATE ROUTE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-route-transact-sql)  
  
-   [GRANT&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [가용성 그룹의 생성 및 구성&#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [AlwaysOn 가용성 그룹 또는 데이터베이스 미러링에 대 한 로그인 계정 설정 &#40;SQL Server&#41;](../../database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [SQL Server Service Broker](../../configure-windows/sql-server-service-broker.md)  
  
  
