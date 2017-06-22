---
title: "MSSQLSERVER_17194 | Microsoft 문서"
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
- "17194"
helpviewer_keywords:
- 17194 (Database Engine error)
ms.assetid: 0d03eb20-28a7-4ceb-8903-7f9420a620f7
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f33e6e16d4f62e7b39afe3b5cd9b57ce13d15a1a
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17194"></a>MSSQLSERVER_17194
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17194|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|서버에서 로그인에 필요한 SSL 공급자 라이브러리를 로드할 수 없습니다. 연결이 닫혔습니다. SSL은 관리자가 서버를 구성한 방식에 따라 로그인 시퀀스 또는 모든 통신을 암호화하는 데 사용됩니다. 온라인 설명서에서 다음 오류 메시지에 대한 정보를 확인하세요.:  0xXXXX. [클라이언트: 11.11.11.11]|  
  
## <a name="explanation"></a>설명  
이 오류는 클라이언트가 연결을 닫았음을 나타내며 연결 제한 시간이 초과되어 발생할 수 있습니다. 이 오류 메시지에는 근본 문제를 설명하는 운영 체제의 값이 표시됩니다.  
  
## <a name="user-action"></a>사용자 동작  
메시지의 오류 코드가 0x2746(10진수 값 10054)이면 일반적으로 시간이 초과되어 클라이언트가 연결을 다시 설정했음을 의미합니다. 이 오류를 해결하려면 클라이언트나 호출 프로그램에서 연결 제한 시간을 늘립니다.  
  
다른 오류 메시지 값에 대해 사용 가능한 해결 방법을 확인하려면 운영 체제 명령 **net helpmsg**를 사용하고 오류 코드의 10진수 값을 지정합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 방법에 대한 자세한 내용은 [서버 네트워크 구성](~/database-engine/configure-windows/server-network-configuration.md) 및 [클라이언트 네트워크 구성](~/database-engine/configure-windows/client-network-configuration.md)을 참조하세요.  
  
## <a name="internal-only"></a>내부 전용  

