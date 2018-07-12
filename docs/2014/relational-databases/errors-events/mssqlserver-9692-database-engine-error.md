---
title: MSSQLSERVER_9692 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d885e4da6d2da28a7e14fd82062e548f8b36b829
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424942"
---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
    
## <a name="details"></a>설명  
  
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
 실행 `netstat -aon` 프로그램 포트를 사용 하는 확인할 수 있습니다. 해당 응용 프로그램을 비활성화하거나 Service Broker에 다른 포트를 지정하십시오.  
  
  
