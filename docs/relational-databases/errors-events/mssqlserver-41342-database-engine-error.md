---
title: MSSQLSERVER_41342 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2e8136363205cf06a210f8a741ed8eb8debaaeb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673591"
---
# <a name="mssqlserver41342"></a>MSSQLSERVER_41342
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41342|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|HK_HW_NOT_SUPPORTED|  
|메시지 텍스트|시스템의 프로세서 모델은 *construct* 만들기를 지원하지 않습니다. 이 오류는 일반적으로 오래된 프로세서에서 발생합니다.|  
  
## <a name="explanation"></a>설명  
메모리 액세스에 최적화된 테이블에는 128비트 값에 대해 원자성 비교 및 교환 작업을 지원하는 프로세서 모델이 필요하며 프로세서 모델에서 CMPXCHG16B 어셈블리 명령어를 지원해야 합니다. 몇몇 이전 AMD 프로세서 모델은 CMPXCHG16B 명령어를 지원하지 않습니다. 또한 특정 가상화 환경에서는 기본적으로 이 명령어를 사용할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
프로세서를 업그레이드합니다. 프로세서에서 명령어를 지원하고 SQL Server를 가상 머신에서 실행하는 경우에는 CMPXCHG16B 명령어를 지원하도록 구성을 변경합니다.  
  
## <a name="see-also"></a>참고 항목  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
