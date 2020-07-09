---
title: MSSQLSERVER_2511 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c28be4ae43225cc4593291285c09115829be8da2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780440"
---
# <a name="mssqlserver_2511"></a>MSSQLSERVER_2511
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|2511|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_KEYS_OUT_OF_ORDER|  
|메시지 텍스트|테이블 오류: 개체 ID %d, 인덱스 ID %d, 파티션 ID %I64d, 할당 단위 ID %I64d(%.*ls 유형). 페이지 %S_PGID, 슬롯 %d 및 %d의 키가 잘못되었습니다.|  
  
## <a name="explanation"></a>설명  
지정된 인덱스에서 잘못된 키가 검색되었습니다. 키가 포함되어 있는 페이지가 손상되었을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
ALTER INDEX REBUILD 문을 사용하여 지정된 인덱스를 다시 작성하십시오.  
  
