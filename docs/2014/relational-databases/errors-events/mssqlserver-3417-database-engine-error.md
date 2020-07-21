---
title: MSSQLSERVER_3417 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c7eb6f5cc94cf23355897776965defd7d35dc79b
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551578"
---
# <a name="mssqlserver_3417"></a>MSSQLSERVER_3417
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3417|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|REC_BADMASTER|  
|메시지 텍스트|master 데이터베이스를 복구할 수 없습니다. SQL Server를 실행할 수 없습니다. 전체 백업에서 master 데이터베이스를 복원하거나 master 데이터베이스를 복구 또는 다시 작성하십시오. master 데이터베이스를 다시 작성하는 방법은 SQL Server 온라인 설명서를 참조하십시오.|  
  
## <a name="explanation"></a>설명  
 SQL Server에서 **master** 데이터베이스를 시작할 수 없습니다. **master** 또는 **tempdb**를 온라인 상태로 만들 수 없으면 SQL Server를 실행할 수 없습니다. 이 오류는 보통 다른 오류 뒤에 나옵니다. 오류 로그를 검토하여 근본 원인을 찾으십시오.  
  
## <a name="user-action"></a>사용자 동작  
 데이터베이스 백업을 복원하거나 데이터베이스를 복구하십시오.  
  
  
