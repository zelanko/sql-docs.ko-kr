---
title: MSSQLSERVER_53 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "53"
helpviewer_keywords:
- 53 (Database Engine error)
ms.assetid: 1234f5a2-b3d1-425a-b29f-480fa792305f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1607d1b6122c4a703ee93cd17705807626e2f0db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867755"
---
# <a name="mssqlserver53"></a>MSSQLSERVER_53
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|53|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|서버에 대한 연결을 구성하는 동안 오류가 발생했습니다.  SQL Server에 연결할 때 기본 설정에서 SQL Server가 원격 연결을 허용하지 않기 때문에 이 오류가 발생할 수 있습니다. (공급자: 명명 된 파이프 공급자, 오류: 40-SQL Server에 연결을 열 수 없습니다) (.NET SqlClient 데이터 공급자)|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트가 서버에 연결할 수 없습니다. 이 오류는 클라이언트가 서버 이름을 확인할 수 없거나 서버 이름이 잘못되어 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 클라이언트에 올바른 서버 이름을 입력했는지 그리고 클라이언트에서 서버 이름을 확인할 수 있는지 검사합니다. TCP/IP 이름 확인을 검사하기 위해 Windows 운영 체제에서 **ping** 명령을 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [네트워크 프로토콜 및 네트워크 라이브러리](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [클라이언트 네트워크 구성](../../database-engine/configure-windows/client-network-configuration.md)   
 [클라이언트 프로토콜 구성](../../database-engine/configure-windows/configure-client-protocols.md)   
 [서버 네트워크 프로토콜 설정 또는 해제](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
