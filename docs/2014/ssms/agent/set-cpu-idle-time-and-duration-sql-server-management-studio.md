---
title: CPU 유휴 상태 시간 및 지속 시간 설정(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CPU [SQL Server], idle conditions
- time [SQL Server], CPU idle and duration
- duration of CPU idle [SQL Server]
- SQL Server Agent, CPU idle conditions
- idle time [SQL Server]
ms.assetid: 8647b465-d899-4cc7-9640-134a506d0a2e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a355108635799d03c2859b6c47eaaf8acc87dc7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63185549"
---
# <a name="set-cpu-idle-time-and-duration-sql-server-management-studio"></a>CPU 유휴 상태 시간 및 지속 시간 설정(SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 서버의 CPU 유휴 상태 판단 기준을 정의하는 방법에 대해 설명합니다. CPU 유휴 정의는 에이전트가 이벤트 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 응답 하는 방법에 영향을 줍니다. 예를 들어 CPU 유휴 상태 판단 기준을 평균 CPU 사용량이 10% 이하로 떨어져서 10분 동안 이 수준을 유지하는 것으로 가정해 보세요. 그런 다음 서버 CPU가 유휴 상태 판단 기준에 도달할 때마다 작업이 실행되도록 정의하면 해당 작업은 CPU 사용량이 10% 이하로 떨어져서 10분 동안 이 수준을 유지할 때 시작됩니다. 이 작업이 사용 중인 서버 성능에 상당한 영향을 주는 경우 CPU 유휴 상태 판단 기준 정의 방법이 중요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-set-cpu-idle-time-and-duration"></a>CPU 유휴 시간 및 기간을 설정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음, 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **고급** 페이지를 선택합니다.  
  
3.  **CPU 유휴 상태 판단 기준**에서 다음을 수행합니다.  
  
    -   **CPU 유휴 상태 판단 기준 정의**를 선택합니다.  
  
    -   **평균 CPU 사용량이 다음 미만인 경우** (모든 CPU에서) 상자에 백분율(%)을 지정합니다. 이 옵션은 CPU가 유휴 상태로 간주되기 전에 도달해야 하는 사용량 수준을 설정합니다.  
  
    -   **다음 시간 미만인 경우** 상자에 시간(초)을 지정합니다. 이 옵션은 CPU가 유휴 상태로 간주되기 전에 최소 CPU 사용량을 유지해야 하는 지속 기간을 설정합니다.  
  
  
