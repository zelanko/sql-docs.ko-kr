---
title: MSSQLSERVER_33128 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 33128 (Database Engine error)
ms.assetid: 12c1096f-d120-439b-85f3-f794859503c9
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 108c49e59102814e56056ce96b3643c2cd754c76
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172417"
---
# <a name="mssqlserver33128"></a>MSSQLSERVER_33128
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|33128|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SEC_DEPRECATED_ALGO|  
|메시지 텍스트|암호화가 실패했습니다. 키에 사용된 ' %. * ls 알고리즘은 더 이상 지원되지 않습니다.|  
  
## <a name="explanation"></a>설명  
 이 메시지는 RC4 또는 RC4_128 암호화 알고리즘을 참조할 때 발생합니다. RC4 및 RC4_128은 약한 알고리즘이며 더 이상 사용되지 않습니다. 대신 AES 알고리즘 같은 강력한 알고리즘을 사용하는 것이  
  
 데이터베이스 호환성 수준이 90 또는 100인 경우 작업이 성공하고 Deprecation 이벤트가 발생하며 메시지가 링 버퍼에만 나타납니다.  
  
 데이터베이스 호환성 수준이 110 이상인 경우 해독 작업이 성공하고 Deprecation 이벤트가 발생하며 메시지가 링 버퍼에만 나타납니다. 암호화 작업이 실패하고 Deprecation 이벤트가 발생하며 메시지가 사용자에게 표시되고 링 버퍼에도 나타납니다.  
  
> [!NOTE]  
>  링 버퍼는 문서화가 완전하게 완료되지 않은 내부 구성 요소이며 고객은 사용할 수 없습니다. 링 버퍼의 메시지는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 고객 지원 서비스에 문의할 때 유용합니다. 링 버퍼를 보려면 sys.dm_os_ring_buffers 동적 관리 뷰를 쿼리하세요.  
  
|State|Description|  
|-----------|-----------------|  
|1|RC4 키는 기본 제공 encryptbykey() 함수에서 사용됩니다. 기본 제공 함수는 NULL을 반환합니다. 이 메시지는 링 버퍼에만 나타납니다.|  
|2|RC4 키는 기본 제공 decryptbykey() 함수에서 사용됩니다. 이 메시지는 링 버퍼에만 나타납니다.|  
|3|사용되지 않는 RC4 키가 대칭 키로 암호화되었습니다. 이 메시지는 사용자에게 표시되고 링 버퍼에 나타납니다. 사용되지 않는 RC4 대칭 키는 호환성 수준 110에서 변경할 수 없습니다. 암호화 작업에는 RC4 이외의 키를 사용하십시오. 필요한 경우 이전 버전과의 호환성 수준을 90 또는 100으로 설정하십시오.|  
|4|RC4 이외의 키가 사용되지 않는 RC4 대칭 키로 암호화되었습니다. 이 메시지는 사용자에게 표시되고 링 버퍼에 나타납니다. RC4 이외의 대칭 키를 사용하도록 응용 프로그램을 수정하거나 이전 버전과의 호환성 수준을 90 또는 100으로 설정하십시오.|  
|5|사용되지 않는 RC4 키가 대칭 키로 해독되었습니다. 이 메시지는 링 버퍼에만 나타납니다.|  
|6|RC4 이외의 키가 RC4 대칭 키로 해독되었습니다. 이 메시지는 링 버퍼에만 나타납니다.|  
|7|RC4 대칭 키가 인증서로 암호화되었습니다. 이 메시지는 사용자에게 표시되고 링 버퍼에 나타납니다.|  
|8|RC4 대칭 키가 인증서로 해독되었습니다. 이 메시지는 링 버퍼에만 나타납니다.|  
|9|RC4 대칭 키가 EKM 키로 암호화되었습니다.|  
|10|RC4 대칭 키가 EKM 키로 해독되었습니다. 이 메시지는 링 버퍼에만 나타납니다.|  
  
## <a name="user-action"></a>사용자 동작  
 대신 AES 알고리즘 같은 강력한 알고리즘을 사용하는 것이 좋습니다.  
  
 ALTER DATABASE SET COMPATIBILITY_LEVEL을 사용하여 데이터베이스 호환성 수준을 100으로 설정합니다. 이 옵션은 사용하지 않는 것이 좋습니다.  
  
  