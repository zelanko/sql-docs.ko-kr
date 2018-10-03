---
title: (SQL Server Profiler) 추적을 일시 중지 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- pausing traces
- temporarily stopping traces
- traces [SQL Server], pausing
- stopping traces
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d213e6b680bfe0d020a7c95b4e3924ef5679d7e2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077103"
---
# <a name="pause-a-trace-sql-server-profiler"></a>추적 일시 중지(SQL Server Profiler)
  추적을 일시 중지하면 다시 시작할 때까지는 이벤트 데이터가 더 이상 캡처되지 않습니다.  
  
 추적을 일시 중지하면 다시 시작할 때까지는 이벤트 데이터가 더 이상 캡처되지 않습니다. 추적을 다시 시작하면 추적 작업이 재개됩니다. 다시 시작한 후 이전에 캡처한 데이터는 손실되지 않으며 추적이 다시 시작되면 데이터 캡처는 일시 중지되었던 시점부터 재개됩니다. 추적이 일시 중지된 동안 이름, 이벤트, 열 및 필터를 변경할 수 있습니다. 하지만 추적 데이터를 보낼 대상을 변경하거나 서버 연결을 변경할 수 없습니다.  
  
### <a name="to-pause-a-trace"></a>추적을 일시 중지하려면  
  
1.  실행 중인 추적이 포함된 창을 선택합니다.  
  
2.  **파일** 메뉴에서 **추적 일지 중지**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 프로파일러](sql-server-profiler.md)  
  
  
