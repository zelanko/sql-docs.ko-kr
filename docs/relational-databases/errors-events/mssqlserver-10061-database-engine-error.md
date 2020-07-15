---
title: MSSQLSERVER_10061 | Microsoft 문서
description: 서버가 SQL Server의 클라이언트 요청에 응답하지 않았습니다. 오류에 대한 설명과 가능한 해결 방법을 확인합니다.
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "10061"
helpviewer_keywords:
- 10061 (Database Engine error)
ms.assetid: 729602f3-08df-474c-8740-8dea13c1eee3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cc775781dfce666ef663b2b3d36b4633524b30e5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781547"
---
# <a name="mssqlserver_10061"></a>MSSQLSERVER_10061
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|10061|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|서버에 대한 연결을 구성하는 동안 오류가 발생했습니다.  SQL Server에 연결할 때 기본 설정에서 SQL Server가 원격 연결을 허용하지 않기 때문에 이 오류가 발생할 수 있습니다. (공급자: TCP 공급자, 오류: 0 - 대상 머신에서 연결을 거부했으므로 연결하지 못했습니다.) (Microsoft SQL Server, 오류: 10061)|  
  
## <a name="explanation"></a>설명  
서버가 클라이언트 요청에 응답하지 않았습니다. 서버가 시작되지 않았기 때문에 이 오류가 발생했을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
서버가 시작되었는지 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 엔진 서비스 관리](~/database-engine/configure-windows/manage-the-database-engine-services.md)  
[클라이언트 프로토콜 구성](~/database-engine/configure-windows/configure-client-protocols.md)  
[네트워크 프로토콜 및 네트워크 라이브러리](~/sql-server/install/network-protocols-and-network-libraries.md)  
[클라이언트 네트워크 구성](~/database-engine/configure-windows/client-network-configuration.md)  
[클라이언트 프로토콜 구성](~/database-engine/configure-windows/configure-client-protocols.md)  
[서버 네트워크 프로토콜 설정 또는 해제](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
