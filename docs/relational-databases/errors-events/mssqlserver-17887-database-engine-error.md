---
title: MSSQLSERVER_17887 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: caf58e486706913fbaa8016e142f6aefc8bded3b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68137209"
---
# <a name="mssqlserver_17887"></a>MSSQLSERVER_17887
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17887|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SRV_IO_COMP_LISTENER_NONYIELDING|  
|메시지 텍스트|IO 완료 수신기(0x%lx) 작업자 0x%p이(가) 노드 %ld에서 잠긴 것 같습니다. 대략적인 CPU 사용량: 커널 %I64dms, 사용자 %I64dms, 간격: %I64d.|  
  
## <a name="explanation"></a>설명  
네트워크 읽기/쓰기 이벤트에 대해 I/O 완료 루틴을 실행할 때 지정된 노드의 I/O 완료 포트 수신기에 문제가 있을 수 있음을 나타냅니다. 이 오류는 I/O 완료 루틴이 실행될 때 I/O 완료 포트 수신기가 반환되면 더 이상 발생하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
Microsoft CSS(고객 지원 서비스)에 문의합니다.  
  
