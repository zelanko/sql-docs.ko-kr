---
title: Service Broker 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Service Broker [SMO]
ms.assetid: b29d7432-d1e5-4bb6-b544-57b3a9430f95
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e74e1530efc8e6000a9edf8882cf37cc60b1f1e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63226194"
---
# <a name="managing-service-broker"></a>Service Broker 관리
  SMO에서 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 개체는 `Microsoft.SqlServer.Management.Smo.Broker` 네임스페이스에 있기 때문에 Microsoft.SqlServer.Smo.dll에 대한 참조가 필요합니다. 클래스 정보를 지원하려면 Microsoft.SqlServer.ServiceBrokerEnum.dll에 대한 참조도 필요합니다.  
  
 SMO는 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 구현에 대한 프로그래밍 방식 관리(DDL)를 허용하는 일련의 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 개체를 제공합니다. 프로그래밍 방식 관리에는 메시지 유형, 계약, 큐 및 서비스를 정의하는 작업이 포함됩니다. SMO는 데이터 조작용 도구가 아니라 관리 도구이므로 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 메시지를 보내고 받는 것은 지원하지 않습니다.  
  
 SMO에서 <xref:Microsoft.SqlServer.Management.Smo.Database.ServiceBroker%2A> 개체는 최상위 클래스이고 이 클래스 아래에 모든 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 기능이 포함됩니다. 분산 메시징 애플리케이션에 참여하는 각 데이터베이스에 대해서는 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 를 구현해야 합니다. 따라서 <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> 개체는 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체의 자식이 됩니다.  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> 개체는 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 구현을 정의하는 데 사용되는 다음 개체의 컬렉션을 포함합니다.  
  
-   
  <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageType> 개체는 메시지의 내용을 정의하는 메시지 유형을 나타냅니다.  
  
-   
  <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageTypeMapping> 개체는 특정 대화의 메시지 방향 및 유형을 지정하는 계약을 나타냅니다.  
  
-   
  <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceQueue> 개체는 메시지를 보내기 전과 메시지가 수신된 후 메시지를 저장합니다. 이 개체는 서비스 간의 비동기 통신을 지원하며 같은 대화 그룹의 메시지를 자동으로 잠그는 등의 기타 유용한 기능을 제공합니다.  
  
-   
  <xref:Microsoft.SqlServer.Management.Smo.Broker.BrokerService> 개체는 대화에 대한 주소 지정 가능 엔드포인트인 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 서비스를 나타냅니다. 
  [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 메시지는 한 서비스에서 다른 서비스로 전송됩니다. 서비스는 메시지를 보관할 큐를 지정하고 대상이 될 수 있는 서비스에 계약을 지정합니다.  
  
-   
  <xref:Microsoft.SqlServer.Management.Smo.Broker.RemoteServiceBinding> 개체는 [!INCLUDE[ssSB](../../../includes/sssb-md.md)]가 원격 서비스와의 통신 시 사용하는 보안 및 인증 설정을 나타냅니다.  
  
-   
  <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceRoute> 개체는 서비스 및 서비스가 정의된 데이터베이스에 대한 위치 정보가 포함된 [!INCLUDE[ssSB](../../../includes/sssb-md.md)] 경로를 나타냅니다. 메시지를 배달하려면 경로가 있어야 합니다. 각 데이터베이스에는 현재 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스를 위치로 지정하는 경로가 기본적으로 포함되어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>   
 [SQL Server Service Broker](../../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
