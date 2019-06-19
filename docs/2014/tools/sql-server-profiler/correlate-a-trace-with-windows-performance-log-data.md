---
title: Windows 성능 로그 데이터와 추적의 상관 관계 지정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3c8a3d7a9888423d312d578784e1f7e1ff75434d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316306"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>Windows 성능 로그 데이터와 추적의 상관 관계 지정
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 Microsoft Windows 성능 로그를 열고 추적과의 상관 관계를 지정할 카운터를 선택한 다음 선택한 성능 카운터를 추적과 함께 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 그래픽 사용자 인터페이스에 표시할 수 있습니다. 추적 창에서 이벤트를 선택하면 선택한 추적 이벤트와 상관 관계가 있는 성능 로그 데이터가 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 의 시스템 모니터 데이터 창에서 빨간 세로 막대로 표시됩니다.  
  
 추적과 성능 카운터의 상관 관계를 지정하려면 **StartTime** 및 **EndTime** 데이터 열을 포함하는 추적 파일이나 테이블을 연 다음 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]**파일** 메뉴에서 **성능 데이터 가져오기**를 클릭합니다. 그러면 성능 로그를 열고 추적과의 상관 관계를 지정할 시스템 모니터 개체와 카운터를 선택할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [추적과 Windows 성능 로그 데이터의 상관 관계 지정&#40;SQL Server Profiler&#41;](correlate-a-trace-with-windows-performance-log-data.md)  
  
  
