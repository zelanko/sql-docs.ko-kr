---
title: "MSSQLSERVER_7711 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 7711 (Database Engine error)
ms.assetid: a5c7cd6e-18d6-47ef-902b-db9dd64bba34
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6faacaf1a80fb4a2f3364da82936521691452db5
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver7711"></a>MSSQLSERVER_7711
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7711|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PRT_RANGE_OVERLAP|  
|메시지 텍스트|DATA_COMPRESSION 옵션이 테이블이나 인덱스 또는 해당 파티션 중 하나에 대해 두 번 이상 지정되었습니다.|  
  
## <a name="explanation"></a>설명  
다음 문 중 하나에서 DATA_COMPRESSION 옵션을 사용할 때 오류가 발생했습니다.  
  
-   CREATE TABLE  
  
-   ALTER TABLE  
  
-   CREATE  INDEX  
  
-   ALTER INDEX  
  
해당 테이블이나 인덱스가 분할된 경우 DATA_COMPRESSION 옵션이 최소한 하나 이상의 파티션에 대해 두 번 이상 나열되었고, 테이블이나 인덱스가 분할되지 않은 경우 DATA_COMPRESSION 옵션이 두 번 이상 나열되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
분할된 테이블이나 인덱스의 경우 DATA_COMPRESSION 옵션이 각 파티션에 대해 한 번만 지정되었는지 확인하고, 분할되지 않은 테이블이나 인덱스의 경우 문에서 DATA_COMPRESSION 옵션을 한 번만 사용합니다.  
  

