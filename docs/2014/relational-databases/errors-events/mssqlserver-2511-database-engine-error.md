---
title: MSSQLSERVER_2511 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1748e8b483eecee43da921bd268d419408924af3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868969"
---
# <a name="mssqlserver2511"></a>MSSQLSERVER_2511
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2511|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_KEYS_OUT_OF_ORDER|  
|메시지 텍스트|테이블 오류: 개체 ID %d, 인덱스 ID %d, 파티션 ID %I64d, 할당 단위 ID %I64d (형식 %. * ls). 페이지 %S_PGID, 슬롯 %d 및 %d의 키가 잘못되었습니다.|  
  
## <a name="explanation"></a>설명  
 지정된 인덱스에서 잘못된 키가 검색되었습니다. 키가 포함되어 있는 페이지가 손상되었을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 ALTER INDEX REBUILD 문을 사용하여 지정된 인덱스를 다시 작성하십시오.  
  
  
