---
title: 이벤트 추적 및 재생 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7b40ddaddc652f5b5e37fc23b1330ebd8f92c475
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753835"
---
# <a name="tracing-and-replaying-events"></a>이벤트 추적 및 재생
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Smo에서 **추적** 및 **재생** 개체를 <xref:Microsoft.SqlServer.Management.Trace> 네임 스페이스에 대 한 프로그래밍 방식의 액세스를 제공 합니다 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 인스턴스를모니터링에사용되는기능을[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. 각 이벤트에 대한 데이터를 캡처하고 파일이나 테이블에 저장하여 나중에 분석할 수 있습니다. 예를 들어 프로덕션 환경을 모니터링하여 어느 프로시저가 너무 늦게 실행되어 성능 저하를 유발하는지 확인할 수 있습니다.  
  
 합니다 **추적** 하 고 **재생** 인스턴스에서 추적을 만드는 데 사용할 수 있는 개체의 집합을 제공 하는 개체 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 이러한 개체는 사용자의 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대한 추적을 수동으로 만드는 데 사용할 수 있습니다. 또한 SMO **추적** 개체를 모니터링 하 여 생성 된 테이블과 SQL 추적 파일을 읽는 데 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 또는 DTS 로깅을 합니다.  
  
 SMO **Trace** 개체를 사용하면 다음 작업을 수행할 수 있습니다.  
  
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
  
 추적 데이터를 **추적** 하 고 **재생** 개체는 SMO 응용 프로그램에서 사용할 수 있습니다 또는 사용 하 여 수동으로 검사할 수 있습니다 [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)합니다. 추적 데이터가 과도 호환 되는 [SQL 추적](../../../relational-databases/sql-trace/sql-trace.md) 도 추적 기능을 제공 하는 저장 프로시저입니다.  
  
 SMO 추적 개체는 Microsoft.SQLServer.ConnectionInfo.dll 파일에 대한 참조가 필요한 <xref:Microsoft.SqlServer.Management.Trace> 네임스페이스에 있습니다.  
  
 **추적** 및 **재생** 개체 필요는 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> 개체의 인스턴스를 사용 하 여 연결할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 합니다 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) 개체를 [Microsoft.SqlServer.Management.Common](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common) 네임 스페이스는 Microsoft.SQLServer.ConnectionInfo.dll 파일에 대 한 참조가 필요 합니다.  
  
> [!NOTE]  
>  64비트 플랫폼에서는 **Trace** 및 **Replay** 개체가 지원되지 않습니다.  
  
  
