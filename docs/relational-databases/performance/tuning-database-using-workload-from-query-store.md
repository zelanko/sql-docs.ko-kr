---
title: "쿼리 저장소의 작업을 사용하여 데이터베이스 튜닝 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Engine Tuning Advisor, Query Store
ms.assetid: 17107549-5073-4fa2-8ee7-5ed33b38821e
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7f89ed5e87b8fd51e8618a8559679225d91b32de
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="tuning-database-using-workload-from-query-store"></a>쿼리 저장소의 작업을 사용하여 데이터베이스 튜닝
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


SQL Server의 [쿼리 저장소](../../relational-databases/performance/how-query-store-collects-data.md) 기능은 쿼리, 계획 및 런타임 통계의 기록을 자동으로 캡처하고 이 정보를 데이터베이스에 저장합니다. [DTA(데이터베이스 엔진 튜닝 관리자)](../../relational-databases/performance/database-engine-tuning-advisor.md)는 쿼리 저장소를 사용하여 튜닝하기에 적합한 작업을 자동으로 선택하는 새로운 옵션을 지원합니다. 따라서 많은 사용자가 튜닝을 위한 작업을 명시적으로 수집하지 않아도 됩니다. 이 기능은 데이터베이스에서 쿼리 저장소 기능이 설정된 경우에만 사용할 수 있습니다. 
  
  이 기능은 SQL Server Management Studio 버전 **16.4** 이상에서 사용할 수 있습니다. 
  
<a name="how-to-tune-a-workload-from-query-store-in-database-engine-tuning-advisor-gui"></a>데이터베이스 엔진 튜닝 관리자 GUI에서 쿼리 저장소의 작업을 조정하는 방법
---
DTA GUI에서 이 기능을 사용하려면 **일반** 창에서 **쿼리 저장소** 라디오 단추를 선택합니다(아래 그림 참조).
![쿼리 저장소의 DTA 작업](../../relational-databases/performance/media/dta-workload-from-query-store.gif)
 
<a name="how-to-tune-a-workload-from-query-store-in-dtaexe-command-line-utility"></a>dta.exe 명령줄 유틸리티를 사용하여 쿼리 저장소의 작업을 튜닝하는 방법
---
명령줄(dta.exe)에서 **-iq** 옵션을 선택하여 쿼리 저장소의 작업을 선택합니다. 

쿼리 저장소에서 작업을 선택할 때 DTA의 동작을 튜닝하는 데 도움이 되는 명령줄을 통해 사용할 수 있는 두 가지 추가 옵션이 있습니다. 이러한 옵션은 GUI를 통해 사용할 수 없습니다.
  1. 튜닝할 작업 이벤트 수: 사용자는 **-n** 명령줄 인수를 사용하여 지정되는 이 옵션을 통해 쿼리 저장소의 이벤트 수를 튜닝할 수 있습니다. 기본적으로 DTA는 이 옵션에 1000 값을 사용합니다. DTA는 항상 가장 비용이 많이 드는 이벤트를 총 기간으로 선택합니다. 
  
  2. 튜닝할 이벤트의 시간 창: 쿼리 저장소에는 오래 전에 실행된 쿼리가 포함될 수 있으므로 이 옵션을 사용하면 DTA가 튜닝을 위해 쿼리를 실행해야 하는 과거 시간 창(시간)을 지정할 수 있습니다. 이 옵션은 **-I** 명령줄 인수를 사용하여 지정됩니다. 

자세한 내용은 [dta 유틸리티](../../tools/dta/dta-utility.md)를 참조하세요.

<a name="difference-between-using-workload-from-query-store-and-plan-cache"></a>쿼리 저장소와 계획 캐시 작업의 차이점 
--- 
쿼리 저장소와 계획 캐시 옵션의 차이점은 데이터베이스에 대해 실행된 쿼리가 쿼리 저장소에 더 오래 저장되어 있고 서버를 다시 시작한 후에도 지속된다는 것입니다. 반면에 계획 캐시에는 계획이 메모리에 캐시된 최근 실행 쿼리의 하위 집합만 포함됩니다. 서버가 다시 시작되면 계획 캐시의 항목이 삭제됩니다.

<a name="see-also"></a>참고 항목 
--- 
[데이터베이스 엔진 튜닝 관리자](../../relational-databases/performance/database-engine-tuning-advisor.md)     
[자습서: 데이터베이스 엔진 튜닝 관리자](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)     
[쿼리 저장소에서 데이터를 수집하는 방법](../../relational-databases/performance/how-query-store-collects-data.md)     
[쿼리 저장소 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)
