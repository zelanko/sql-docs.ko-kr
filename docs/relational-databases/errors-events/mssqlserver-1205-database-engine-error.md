---
title: MSSQLSERVER_1205 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 402d3a3cdb3d1c8eb52feaede9ff1115e745c563
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68116027"
---
# <a name="mssqlserver_1205"></a>MSSQLSERVER_1205
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1205|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LK_VICTIM|  
|메시지 텍스트|트랜잭션(프로세스 ID %d)이 %.*ls 리소스에서 다른 프로세스와의 교착 상태가 발생하여 실행이 중지되었습니다. 트랜잭션을 다시 실행하십시오.|  
  
## <a name="explanation"></a>설명  
리소스가 별도의 트랜잭션에서 충돌하는 순서대로 액세스되면 교착 상태가 발생합니다. 다음은 그 예입니다.  
  
-   Transaction2가 **Table2.Row2**를 업데이트하는 동안 Transaction1이 **Table1.Row1**을 업데이트합니다.  
  
-   Transaction1이 **Table2.Row2**의 업데이트를 시도하지만 Transaction2가 커밋되지 않아 차단됩니다.  
  
-   이제 Transaction2가 **Table1.Row1**의 업데이트를 시도하지만 Transaction1이 커밋되지 않아 차단됩니다.  
  
-   Transaction1은 Transaction2가 완료되기를 기다리지만 Transaction2는 Transaction1이 완료되기를 기다리므로 교착 상태가 발생합니다.  
  
시스템에서는 이 '교착 상태'를 감지하면 관련된 트랜잭션 중 하나를 '희생자'로 선택하고 이 메시지를 보낸 후 희생자의 트랜잭션을 롤백합니다.  
  
## <a name="user-action"></a>사용자 동작  
트랜잭션을 다시 실행하십시오. 교착 상태가 발생하지 않도록 애플리케이션을 수정할 수도 있습니다. 교착 상태가 발생한 트랜잭션을 다시 실행하면 동시에 실행 중인 작업이 무엇인지에 따라 성공할 수도 있습니다.  
  
교착 상태를 방지하거나 발생하지 않도록 하려면 모든 트랜잭션이 동일한 순서(**Table1**에 액세스한 뒤 **Table2**에 액세스)로 행에 액세스하도록 하세요. 이렇게 하면 차단이 발생할 수는 있으나 교착 상태는 발생하지 않습니다.  
  
