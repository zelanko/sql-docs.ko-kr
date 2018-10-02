---
title: 필터 설정 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.filtersettings.f1
ms.assetid: 1b401d7d-db8a-4ba1-acb1-b8dec14e3311
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a0f38fd7a404e991cd6c87fd303cb03658f8b235
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734651"
---
# <a name="filter-settings"></a>필터 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **필터 설정** 대화 상자를 사용하여 복제 모니터에서 표에 사용할 필터를 정의할 수 있습니다. 예를 들어 **모든 구독** 탭에서 활성 상태인 구독만 표시하려면 **열 이름** 열에서 **상태** 를, **연산자** 열에서 **같음** 을, **값1** 열에서 **활성** 을 선택합니다. 하나 이상의 열을 기준으로 필터를 정의하면 필터 조건과 일치하는 행만 표에 표시되도록 필터가 적용됩니다.  
  
## <a name="options"></a>Options  
 **상태**  
 필터링할 열의 이름을 선택합니다. 하나 이상의 열을 필터 기준으로 사용할 수 있습니다.  
  
 **같음**  
 **작거나 같음**등의 필터에 대한 연산자를 선택합니다.  
  
 **값1** 및 **값2**  
 필터 값을 입력하거나 선택합니다. 대부분의 연산자는 **값1** 열에만 값을 입력하면 되지만 **사이** 및 **사이에 있지 않음** 연산자는 **값2** 열에도 값을 입력해야 합니다.  
  
 **필터 지우기**  
 정의된 필터를 모두 지우려면 이 단추를 클릭합니다. 단일 필터를 제거하려면 필터 행을 선택하고 Delete 키를 누릅니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
