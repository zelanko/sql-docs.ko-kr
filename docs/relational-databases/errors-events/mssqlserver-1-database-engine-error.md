---
title: "MSSQLSERVER_-1 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "-1"
helpviewer_keywords:
- -1 (Database Engine error)
ms.assetid: bad25b91-eaed-46c0-a5b7-71117a32304c
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4ad7c2405b50c97e9d26f047089bc5069a3bc20
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver-1"></a>MSSQLSERVER_-1
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|-1|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|서버에 대한 연결을 구성하는 동안 오류가 발생했습니다.  기본 설정 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 원격 연결이 허용되지 않기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 때 이 오류가 발생할 수 있습니다. (공급자: SQL 네트워크 인터페이스, 오류: 28 - 서버가 요청한 프로토콜을 지원하지 않습니다.) (Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 오류: -1)|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트가 서버에 연결할 수 없습니다. 이 오류는 다음과 같은 이유로 인해 발생할 수 있습니다.  
  
-   지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름이 올바르지 않습니다.  
  
-   TCP, 즉 명명된 파이프 프로토콜이 활성화되어 있지 않습니다.  
  
-   서버의 방화벽에서 연결을 거부했습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스(sqlbrowser)가 시작되지 않았습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 오류를 해결하려면 다음 동작 중 하나를 수행합니다.  
  
-   연결 문자열에 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름의 철자를 확인합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 도구를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TCP 또는 명명된 파이프 프로토콜을 통한 원격 연결을 허용하도록 구성합니다. 원격 연결을 허용하는 방법에 대한 자세한 내용은 [서버 네트워크 프로토콜 설정 또는 해제](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)를 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 서버 인스턴스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 포트 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 포트(UDP 1434)를 열도록 방화벽을 구성했는지 확인합니다.  
  
-   서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 시작되었는지 확인합니다.  
  
## <a name="see-also"></a>관련 항목:  
[데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[클라이언트 프로토콜 구성](~/database-engine/configure-windows/configure-client-protocols.md)  
[네트워크 프로토콜 및 네트워크 라이브러리](~/sql-server/install/network-protocols-and-network-libraries.md)  
[클라이언트 네트워크 구성](~/database-engine/configure-windows/client-network-configuration.md)  
[클라이언트 프로토콜 구성](~/database-engine/configure-windows/configure-client-protocols.md)  
[서버 네트워크 프로토콜 설정 또는 해제](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  

