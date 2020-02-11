---
title: 이벤트 추적 및 재생 Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d83b716d9919bf322097b8ded8409950982d961c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70148354"
---
# <a name="tracing-and-replaying-events"></a>이벤트 추적 및 재생
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO에서 <xref:Microsoft.SqlServer.Management.Trace> 네임 스페이스의 **추적** 및 **재생** 개체는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]인스턴스를 모니터링 하는 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 데 사용 되는 기능에 대 한 프로그래밍 방식의 액세스를 제공 합니다. 각 이벤트에 대한 데이터를 캡처하고 파일이나 테이블에 저장하여 나중에 분석할 수 있습니다. 예를 들어 프로덕션 환경을 모니터링하여 어느 프로시저가 너무 늦게 실행되어 성능 저하를 유발하는지 확인할 수 있습니다.  
  
 **추적** 및 **재생** 개체는 인스턴스에 대 한 추적을 만드는 데 사용할 수 있는 개체 집합을 제공 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 이러한 개체는 사용자의 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 대한 추적을 수동으로 만드는 데 사용할 수 있습니다. 또한 SMO **추적** 개체를 사용 하 여, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]또는 DTS 로깅을 모니터링 하 여 만든 SQL 추적 파일 및 테이블을 읽을 수 있습니다.  
  
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
  
 
  **Trace** 및 **Replay** 개체의 추적 데이터는 SMO 애플리케이션에서 사용하거나 [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md)를 사용하여 수동으로 검사할 수 있습니다. 추적 데이터는 추적 기능을 제공하는 [SQL Trace](../../../relational-databases/sql-trace/sql-trace.md) 저장 프로시저에서도 사용할 수 있습니다.  
  
 SMO 추적 개체는 Microsoft.SQLServer.ConnectionInfo.dll 파일에 대한 참조가 필요한 <xref:Microsoft.SqlServer.Management.Trace> 네임스페이스에 있습니다.  
  
 **추적** 및 **재생** 개체를 사용 하려면 [](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> 인스턴스와의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]연결을 설정 하는 ServerConnection 개체가 필요 합니다. ServerConnection 개체는 ConnectionInfo 파일에 대 한 참조를 필요로 하는 [](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) 네임 스페이스에 상주 [합니다.](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common)  
  
> [!NOTE]  
>  64비트 플랫폼에서는 **Trace** 및 **Replay** 개체가 지원되지 않습니다.  
  
  
