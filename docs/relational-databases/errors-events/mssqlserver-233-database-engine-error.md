---
title: "MSSQLSERVER_233 | Microsoft 문서"
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
- "233"
helpviewer_keywords:
- 233 (Database Engine error)
ms.assetid: 201665dc-7ac8-4c19-90d3-33354c5caa72
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a029352dec1ac5a700b7ad5d048a9cb630347462
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver233"></a>MSSQLSERVER_233
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|233|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|서버에 성공적으로 연결되었지만 로그인 중 오류가 발생했습니다. (공급자: 공유 메모리 공급자, 오류: 0 - 파이프의 한쪽 끝에 프로세스가 없습니다.) (Microsoft SQL Server, 오류: 233)|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트가 서버에 연결할 수 없습니다. 서버가 원격 연결을 허용하도록 구성되어 있지 않기 때문에 이 오류가 발생했을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 도구를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 원격 연결을 허용하도록 합니다.  
  
## <a name="see-also"></a>참고 항목  
[네트워크 프로토콜 및 네트워크 라이브러리](~/sql-server/install/network-protocols-and-network-libraries.md)  
[클라이언트 네트워크 구성](~/database-engine/configure-windows/client-network-configuration.md)  
[클라이언트 프로토콜 구성](~/database-engine/configure-windows/configure-client-protocols.md)  
[서버 네트워크 프로토콜 설정 또는 해제](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  

