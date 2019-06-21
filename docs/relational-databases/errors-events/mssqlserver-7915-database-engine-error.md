---
title: MSSQLSERVER_7915 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 653deb1710937d37a11688d41eb378c0650e0a20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62796941"
---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7915|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|메시지 텍스트|복구: 개체 ID O_ID, 인덱스 ID I_ID, 파티션 ID PN_ID, 할당 단위 ID A_ID(TYPE 유형)에 대한 IAM 체인이 페이지 P_ID 앞에서 잘렸으므로 다시 작성됩니다.|  
  
## <a name="explanation"></a>설명  
REPAIR에서 전송한 이 정보 메시지는 지정된 IAM(Index Allocation Map) 체인이 패치되어 다시 작성될 수 있음을 나타냅니다. 패치 작업은 IAM 체인의 새 헤드를 할당하거나 체인에서 잘못된 페이지를 제거할 때 필요할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
없음  
  
