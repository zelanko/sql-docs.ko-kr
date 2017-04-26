---
title: "MSSQLSERVER_-2 | Microsoft 문서"
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
- "-2"
helpviewer_keywords:
- -2 (Database Engine error)
ms.assetid: f37a7b7d-26e1-4b9e-bcb4-57f7805393d2
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b6b67d08a3f8beb88d44499c4b3975d88038feb4
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver-2"></a>MSSQLSERVER_-2
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|-2|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|제한 시간이 만료되었습니다.  작업이 완료되기 전에 제한 시간이 초과되었거나 서버가 응답하지 않습니다. (Microsoft SQL Server, 오류: -2)|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트가 서버에 연결할 수 없습니다. 서버의 방화벽에서 연결을 거부했기 때문에 이 오류가 발생했을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 서버 인스턴스에 있는 방화벽이 연결을 허용하도록 구성되어 있는지 확인합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server 액세스를 허용하도록 Windows 방화벽 구성](~/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
[데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[클라이언트 프로토콜 구성](~/database-engine/configure-windows/configure-client-protocols.md)  
[네트워크 프로토콜 및 네트워크 라이브러리](~/sql-server/install/network-protocols-and-network-libraries.md)  
[클라이언트 네트워크 구성](~/database-engine/configure-windows/client-network-configuration.md)  
[클라이언트 프로토콜 구성](~/database-engine/configure-windows/configure-client-protocols.md)  
[서버 네트워크 프로토콜 설정 또는 해제](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  

