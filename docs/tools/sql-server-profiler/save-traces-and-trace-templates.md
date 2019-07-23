---
title: 추적 및 추적 템플릿 저장 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- exporting trace templates
- importing trace templates
- SQL Server Profiler, templates
ms.assetid: 957e6bf8-e7a3-4a59-a1cd-0a41538a8158
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9d3c8a9ddcaa11f4bcfae6e5abd4c000f1ffbdba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928740"
---
# <a name="save-traces-and-trace-templates"></a>추적 및 추적 템플릿 저장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  추적 파일의 저장과 추적 템플릿의 저장을 구분하는 것은 중요합니다. 추적 파일 저장은 캡처된 데이터를 지정한 장소로 저장하는 것이며 추적 템플릿 저장은 지정한 데이터 열, 이벤트 클래스 또는 필터 등의 추적 정의를 저장하는 것입니다.  
  
## <a name="saving-traces"></a>추적 저장  
 캡처한 데이터를 나중에 분석하거나 재생해야 하는 경우 캡처한 이벤트 데이터를 파일 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 테이블에 저장합니다. 추적 파일을 사용하여 다음을 수행할 수 있습니다.  
  
-   추적 파일이나 추적 테이블을 사용하여 데이터베이스 엔진 튜닝 관리자의 입력으로 사용되는 작업을 만들 수 있습니다.  
  
-   추적 파일을 사용하여 이벤트를 캡처하고 추적 파일을 지원 공급자에게 분석용으로 보낼 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 쿼리 처리 도구를 사용하여 데이터를 액세스하거나 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에서 데이터를 볼 수 있습니다. **sysadmin** 고정 서버 역할의 멤버이거나 테이블을 만든 사람만 추적 테이블에 직접 액세스할 수 있습니다.  
  
> [!NOTE]  
>  추적 데이터를 테이블에 캡처하는 것은 파일에 캡처하는 것보다 느립니다. 그러므로 추적 데이터를 파일에 캡처해 추적 파일을 열고 추적을 추적 테이블로 저장하는 것이 좋습니다.  
  
 추적 파일을 사용할 때 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 추적 정의가 아니라 캡처한 이벤트 데이터를 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적(\*.trc) 파일로 저장합니다. 이 확장명은 추적 파일이 저장될 때 지정한 다른 확장명에 관계없이 자동으로 파일 끝에 추가됩니다. 예를 들어 **Trace.dat** 라는 추적 파일을 지정하면 이렇게 만든 파일은 **Trace.dat.trc** 로 저장됩니다.  
  
> [!IMPORTANT]  
>  SHOWPLAN, ALTER TRACE 또는 VIEW SERVER STATE 권한이 있는 사용자는 실행 계획 출력에 캡처된 쿼리를 볼 수 있습니다. 이러한 쿼리에는 암호 같은 중요한 정보가 포함되어 있을 수 있습니다. 따라서 **db_owner** 고정 데이터베이스 역할의 멤버나 **sysadmin** 고정 서버 역할의 멤버 같이 중요한 정보를 볼 지위에 있는 사용자에게만 이러한 권한을 부여하는 것이 좋습니다. 또한 실행 계획 파일을 저장하거나 실행 계획 관련 이벤트가 포함된 파일을 추적할 때는 NTFS 파일 시스템이 적용된 위치만 사용하고 중요한 정보를 볼 지위에 있는 사용자에게만 해당 위치에 대한 액세스 권한을 부여하는 것이 좋습니다.  
  
## <a name="saving-templates"></a>템플릿 저장  
 추적의 템플릿 정의에는 추적을 만드는 데 사용된 이벤트 클래스, 데이터 열, 필터 및 나머지 속성(캡처된 이벤트 데이터 제외)이 포함됩니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 데이터베이스 엔진 튜닝 관리자가 물리적 데이터베이스 설계를 튜닝하는 데 사용할 수 있는 작업 만들기와 같은 특정 작업 및 일반적인 추적 작업에 대해 미리 정의된 시스템 템플릿을 제공합니다. 사용자 정의 템플릿을 만들고 저장할 수도 있습니다.  
  
### <a name="importing-and-exporting-templates"></a>템플릿 가져오기 및 내보내기  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 템플릿을 한 서버에서 다른 서버로 가져오거나 내보낼 수 있습니다. 템플릿을 내보내면 기존 템플릿의 사본이 지정한 디렉터리로 이동됩니다. 템플릿을 가져오면 지정한 템플릿의 사본이 생성됩니다. 이러한 템플릿은 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에 표시될 때 템플릿 이름 뒤에 오는 단어 "(user)"로 시스템 템플릿과 구분할 수 있습니다. 미리 정의된 시스템 템플릿은 덮어쓰거나 직접 수정할 수 없습니다.  
  
### <a name="analyzing-performance-with-templates"></a>템플릿으로 성능 분석  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 자주 모니터링하는 경우 템플릿을 사용하여 성능을 분석할 수 있습니다. 템플릿은 매번 같은 이벤트 데이터를 캡처하고 같은 추적 정의를 사용하여 같은 이벤트를 모니터링합니다. 추적을 만들 때마다 이벤트 클래스와 데이터 열을 정의할 필요가 없습니다. 또한 다른 사용자에게 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트를 모니터링하는 데 사용하도록 템플릿을 줄 수도 있습니다. 예를 들어 지원 공급자는 고객에게 템플릿을 제공할 수 있습니다. 고객은 템플릿을 사용하여 필요한 이벤트 데이터를 캡처해 지원 공급자에게 분석을 위해 보낼 수 있습니다.  
  
 **파일에 추적 저장**  
  
 [추적 결과를 파일에 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
 [sp_trace_create&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [테이블에 추적 결과 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)   
 [추적 템플릿 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [실행 중인 추적으로부터 템플릿 파생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [추적 파일 또는 추적 테이블에서 템플릿 파생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [추적 템플릿 내보내기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)   
 [추적 템플릿 가져오기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
  
