---
title: MSSQLSERVER_9692 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7041aa3e2262932541c4d81fe93dd1d9a740c97a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67903811"
---
# <a name="mssqlserver_9692"></a>MSSQLSERVER_9692
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
**netstat -aon**을 실행하여 포트를 사용하고 있는 프로그램을 확인하세요. 해당 애플리케이션을 비활성화하거나 Service Broker에 다른 포트를 지정하십시오.  
  
