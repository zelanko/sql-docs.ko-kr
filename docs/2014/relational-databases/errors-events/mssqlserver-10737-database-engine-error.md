---
title: MSSQLSERVER_10737 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7d89c05ebd0b181b63f66fa0e0e0db99d54b952
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62916147"
---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>설명  
  
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
  
