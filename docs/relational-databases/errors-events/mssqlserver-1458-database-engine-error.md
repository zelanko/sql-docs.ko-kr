---
title: MSSQLSERVER_1458 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 546d3e40d8b925d88344f6074d577b1b14c31092
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033432"
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1458|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBM_FAILREDO_ON_PRIMARY|  
|메시지 텍스트|'%.*ls' 데이터베이스의 주 복사본에 오류 %d, 상태 %d, 심각도 %d이(가) 발생했습니다. 데이터베이스 미러링이 일시 중지되었습니다. 오류 상태를 해결한 다음 미러링을 재개하십시오.|  
  
## <a name="explanation"></a>설명  
이 메시지는 주 데이터베이스에 오류가 발생하여 데이터베이스 미러링이 일시 중지되었음을 의미합니다.  
  
## <a name="user-action"></a>사용자 동작  
이러한 오류의 대부분은 자체적으로 수정됩니다. 문제가 지속되는 경우 일반적으로 데이터베이스 또는 서버 인스턴스를 다시 시작하면 문제가 해결됩니다. 자세한 내용은 이 메시지 앞에 나오는 관련 오류에 대한 각 파트너의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 확인하십시오.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 미러링 모니터링&#40;SQL Server&#41;](~/database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
