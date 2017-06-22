---
title: "MSSQLSERVER_10737 | Microsoft 문서"
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
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 591b8634e244f472fd5051fde842f4bf9428c4d4
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|MSSQLSERVER|  
|이벤트 ID|10737|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|메시지 텍스트|ALTER TABLE REBUILD 또는 ALTER INDEX REBUILD 문에서 DATA_COMPRESSION 절에 지정된 파티션이 있으면 PARTITION=ALL을 지정해야 합니다. PARTITION=ALL 절은 DATA_COMPRESSION 절에 하위 집합만 지정된 경우에도 테이블 또는 인덱스의 모든 파티션이 다시 작성되도록 지원하는 데 사용됩니다.|  
  
## <a name="user-action"></a>사용자 동작  
ALTER TABLE 또는 ALTER INDEX 문에 PARTITION=ALL 절을 추가하거나 REBUILD PARTITION = \<partition-number-expr> WITH (DATA_COMPRESSION={ON | OFF})를 사용하여 특정 파티션을 다시 작성하세요.  
  

