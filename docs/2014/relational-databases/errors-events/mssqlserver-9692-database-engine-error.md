---
title: MSSQLSERVER_9692 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 661d7ab65afca258424af300debde328b8f01fee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62761705"
---
# <a name="mssqlserver_9692"></a>MSSQLSERVER_9692
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|9692|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SB2_CANT_LISTEN_PORT_IN_USE|  
|메시지 텍스트|다른 프로세스에 사용 중이므로 %S_MSG 프로토콜 전송이 포트 %d에서 수신할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 지정된 TCP 포트를 컴퓨터의 다른 프로그램에서 사용 중입니다.  
  
## <a name="user-action"></a>사용자 동작  
 를 `netstat -aon` 실행 하 여 포트를 사용 중인 프로그램을 확인 합니다. 해당 애플리케이션을 비활성화하거나 Service Broker에 다른 포트를 지정하십시오.  
  
  
