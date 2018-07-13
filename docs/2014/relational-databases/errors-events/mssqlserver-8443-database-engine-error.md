---
title: MSSQLSERVER_8443 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2e2f275c073750ba3998299c41375d8ecc5eb6ea
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414362"
---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8443|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SB_DIALOG_WO_CONV_GROUP|  
|메시지 텍스트|ID가 '%.*ls'이고 시작자가 %d인 대화가 누락된 대화 그룹 '%.\*ls'을(를) 참조합니다. DBCC CHECKDB를 실행하여 데이터베이스를 분석 및 복구하십시오.|  
  
## <a name="explanation"></a>설명  
 메타데이터 계층에서 대화 그룹에 대해 NULL을 반환했습니다. 데이터베이스가 일부 손상되었으며 가능한 손상 원인 중 하나는 디스크 오류입니다.  
  
## <a name="user-action"></a>사용자 동작  
 DBCC CHECKDB를 복구 모드로 실행하여 데이터베이스를 일관된 상태로 복구하십시오. 필요한 경우 일관성을 복원하기 위해 메시지를 삭제할 수도 있습니다. 시스템 오류 로그를 조사하여 시스템 내의 다른 실패로 인해 이 오류가 발생했는지 확인하십시오.  
  
  
