---
title: 열 정렬 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.sortcolumns.f1
ms.assetid: 66b44b6c-10a5-4e3f-a97b-7568609c88ac
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7a1be23bebd3055c6c8e40664d37d666a4f09467
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908378"
---
# <a name="sort-columns"></a>열 정렬
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **열 정렬** 대화 상자를 사용하여 복제 모니터에서 하나 이상의 열을 기준으로 표를 정렬할 수 있습니다. 복제 모니터 표의 열 머리글을 클릭하여 단일 열을 기준으로 정렬할 수도 있습니다. 예를 들어 **모든 구독** 탭에서 구독을 상태별로 정렬한 다음 연결 유형별로 정렬하려면 다음 단계를 수행합니다.  
  
1.  표의 첫 번째 행에서 **열 이름** 열의 **상태** 를 선택하고 **정렬 순서** 열에서 값을 선택합니다.  
  
2.  표의 두 번째 행에서 **열 이름** 열의 **연결 유형** 을 선택하고 **정렬 순서** 열에서 값을 선택합니다.  

## <a name="options"></a>옵션  
 **상태**  
 정렬 기준으로 사용할 열의 이름입니다. 하나 이상의 열을 기준으로 정렬할 수 있습니다. **게시** 탭의 **현재 평균 성능** 또는 **현재 가장 낮은 성능** 열은 해당 값이 계산되는 방식 때문에 정렬 기준으로 사용할 수 없습니다.  
  
 **정렬 순서**  
 **오름차순** 또는 **내림차순**값을 지정합니다.  
  
 **모두 지우기**  
 정렬 표에서 모든 행을 제거합니다. 단일 행을 제거하려면 행을 선택하고 Delete 키를 누릅니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
