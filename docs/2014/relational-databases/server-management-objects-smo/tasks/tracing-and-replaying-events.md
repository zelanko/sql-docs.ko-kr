---
title: 이벤트 추적 및 재생 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eb1d3f67ef90dcadfeb0dc976672af615b4efbba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230693"
---
# <a name="tracing-and-replaying-events"></a>이벤트 추적 및 재생
  SMO에서 <xref:Microsoft.SqlServer.Management.Trace> 네임스페이스의 `Trace` 및 `Replay` 개체는 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 기능에 대한 프로그래밍 방식 액세스를 제공합니다. 이 기능은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 모니터링하는 데 사용됩니다. 각 이벤트에 대한 데이터를 캡처하고 파일이나 테이블에 저장하여 나중에 분석할 수 있습니다. 예를 들어 프로덕션 환경을 모니터링하여 어느 프로시저가 너무 늦게 실행되어 성능 저하를 유발하는지 확인할 수 있습니다.  
  
 `Trace` 및 `Replay` 개체는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 추적을 만드는 데 사용할 수 있는 개체 집합을 제공합니다. 이러한 개체는 사용자의 응용 프로그램에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대한 추적을 수동으로 만드는 데 사용할 수 있습니다. 또한 SMO `Trace` 개체를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 또는 DTS 로깅을 모니터링하여 만든 SQL 추적 파일 및 테이블을 읽을 수 있습니다.  
  
 SMO `Trace` 개체를 사용하면 다음 작업을 수행할 수 있습니다.  
  
-   추적을 만듭니다.  
  
-   추적에 대한 필터를 설정합니다.  
  
-   추적할 이벤트를 설정합니다.  
  
-   추적을 중지하거나 시작합니다.  
  
-   추적 파일과 추적 테이블을 읽습니다.  
  
-   추적 관련 이벤트에 대한 정보를 가져옵니다.  
  
-   추적 관련 필터에 대한 정보를 가져옵니다.  
  
-   추적 데이터를 프로그래밍 방식으로 조작합니다.  
  
-   추적 테이블과 추적 파일을 씁니다.  
  
-   추적 파일 또는 추적 테이블을 재생합니다.  
  
 추적 데이터를 `Trace` 하 고 `Replay` 개체는 SMO 응용 프로그램에서 사용할 수 있습니다 또는 사용 하 여 수동으로 검사할 수 있습니다 [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)합니다. 추적 데이터가 과도 호환 되는 [SQL 추적](../../sql-trace/sql-trace.md) 도 추적 기능을 제공 하는 저장 프로시저입니다.  
  
 SMO 추적 개체는 Microsoft.SQLServer.ConnectionInfo.dll 파일에 대한 참조가 필요한 <xref:Microsoft.SqlServer.Management.Trace> 네임스페이스에 있습니다.  
  
 `Trace` 및 `Replay` 개체 필요는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> 개체의 인스턴스를 사용 하 여 연결할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체는 Microsoft.SQLServer.ConnectionInfo.dll 파일에 대한 참조가 필요한 <xref:Microsoft.SqlServer.Management.Common> 네임스페이스에 있습니다.  
  
> [!NOTE]  
>  64비트 플랫폼에서는 `Trace` 및 `Replay` 개체가 지원되지 않습니다.  
  
  
