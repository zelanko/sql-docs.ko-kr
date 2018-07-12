---
title: MSSQLSERVER_17887 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 30fe23973966927471bc21cb484b81ae9636e842
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425992"
---
# <a name="mssqlserver17887"></a>MSSQLSERVER_17887
    
## <a name="details"></a>설명  
  
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
  
  
