---
title: 템플릿
titleSuffix: SQl Server Profiler
description: SQL Server Profiler에서 제공하는 미리 정의된 템플릿 및 사용 방법을 알아봅니다. 사용자 정의 템플릿을 만들고 기본 템플릿을 변경하는 방법을 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: b674e491-dc58-47a1-acdd-7028e9a201fc
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 69b3baf3c5c1f19120dff76608d273cfa0cb79e0
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88713991"
---
# <a name="sql-server-profiler-templates"></a>SQL Server Profiler 템플릿

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 추적에 포함할 이벤트 클래스와 데이터 열을 정의하는 템플릿을 만들 수 있습니다. 템플릿을 정의하고 저장한 후 선택한 각 이벤트 클래스에 대한 데이터를 기록하는 추적을 실행할 수 있습니다. 하나의 템플릿을 많은 추적에 사용할 수 있지만 템플릿 자체는 실행되지 않습니다.  

[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 특정 추적을 위해 사용될 가능성이 있는 추적 템플릿을 미리 정의하여 이벤트 클래스를 쉽게 구성할 수 있도록 제공합니다. 예를 들어 Standard 템플릿을 사용하여 로그인, 로그아웃, 완료된 일괄 처리 및 연결 정보를 기록하는 일반적인 추적을 만들 수 있습니다. 이 템플릿을 수정하지 않고 그대로 사용하여 추적을 실행할 수 있으며 이벤트 구성이 서로 다른 추가 템플릿에 대한 시작점으로 삼을 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하면 미리 정의된 템플릿 외에도 기본적으로 이벤트 클래스가 포함되어 있지 않은 빈 템플릿에서 추적을 만들 수 있습니다. 계획한 추적이 미리 정의된 템플릿의 구성과 비슷하지 않을 때는 빈 추적 템플릿을 사용하는 것이 좋습니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 다양한 서버 유형을 추적할 수 있습니다. 예를 들어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 추적할 수 있습니다.  하지만 포함할 수 있는 이벤트 클래스는 각 서버 유형에 따라 다릅니다. 따라서 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 서버 유형에 따라 다른 템플릿을 유지하여 선택한 서버 유형과 일치하는 특정 템플릿을 사용할 수 있게 합니다.  
  
## <a name="predefined-templates"></a>미리 정의된 템플릿  
 Standard(기본) 템플릿 외에 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에는 특정한 유형의 이벤트를 모니터링하기 위한 여러 개의 미리 정의된 템플릿이 포함되어 있습니다. 다음 표에서는 미리 정의된 템플릿, 그 용도 및 정보를 캡처하는 이벤트 클래스를 나열합니다.  
  
|템플릿 이름|템플릿 용도|이벤트 클래스|  
|-------------------|----------------------|-------------------|  
|SP_Counts|시간별로 저장 프로시저 실행 동작을 캡처합니다.|**SP:Starting**|  
|Standard|추적을 만들기 위한 일반적인 시작 지점입니다. 실행되는 모든 저장 프로시저와 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리를 캡처합니다. 일반적인 데이터베이스 서버 활동을 모니터링하는 데 사용합니다.|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Completed**<br /><br /> **SQL:BatchCompleted**<br /><br /> **SQL:BatchStarting**|  
|TSQL|클라이언트가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 로 전송하는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문과 전송된 시간을 캡처합니다. 클라이언트 애플리케이션을 디버깅하는 데 사용합니다.|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SQL:BatchStarting**|  
|TSQL_Duration|클라이언트가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 로 전송하는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문과 실행 시간(밀리초)을 캡처하고 이 문들을 기간별로 그룹화합니다. 느린 쿼리를 식별하는 데 사용합니다.|**RPC:Completed**<br /><br /> **SQL:BatchCompleted**|  
|TSQL_Grouped|[!INCLUDE[tsql](../../includes/tsql-md.md)] 로 전송된 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문과 전송 시간을 캡처합니다. 문을 전송한 사용자 또는 클라이언트를 기준으로 정보를 그룹화합니다. 특정 클라이언트 또는 사용자가 전송한 쿼리를 조사하는 데 사용합니다.|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SQL:BatchStarting**|  
|TSQL_Locks|클라이언트가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 로 전송하는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문을 예외 잠금 이벤트와 함께 캡처합니다. 교착 상태, 잠금 제한 시간 및 잠금 에스컬레이션 이벤트를 해결하는 데 사용합니다.|**Blocked Process Report**<br /><br /> **SP:StmtCompleted**<br /><br /> **SP:StmtStarting**<br /><br /> **SQL:StmtCompleted**<br /><br /> **SQL:StmtStarting**<br /><br /> **Deadlock Graph**<br /><br /> **Lock:Cancel**<br /><br /> **Lock:Deadlock**<br /><br /> **Lock:Deadlock Chain**<br /><br /> **Lock:Escalation**<br /><br /> **Lock:Timeout (timeout>0)**|  
|TSQL_Replay|추적이 재생될 경우 필요한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 대한 세부 정보를 캡처합니다. 벤치마크 테스트와 같이 반복되는 튜닝을 수행하는 데 사용합니다.|**CursorClose**<br /><br /> **CursorExecute**<br /><br /> **CursorOpen**<br /><br /> **CursorPrepare**<br /><br /> **CursorUnprepare**<br /><br /> **Audit Login**<br /><br /> **Audit Logout**<br /><br /> **Existing Connection**<br /><br /> **RPC Output Parameter**<br /><br /> **RPC:Completed**<br /><br /> **RPC:Starting**<br /><br /> **Exec Prepared SQL**<br /><br /> **Prepare SQL**<br /><br /> **SQL:BatchCompleted**<br /><br /> **SQL:BatchStarting**|  
|TSQL_SPs|실행 중인 모든 저장 프로시저에 대한 세부 정보를 캡처합니다. 저장 프로시저의 구성 요소 단계를 분석하는 데 사용합니다. 프로시저가 다시 컴파일 중이라고 생각되면 **SP:Recompile** 이벤트를 추가합니다.|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SP:Completed**<br /><br /> **SP:Starting**<br /><br /> **SP:StmtStarting**<br /><br /> **SQL:BatchStarting**|  
|튜닝|저장 프로시저와 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리 실행에 대한 정보를 캡처합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자가 데이터베이스를 튜닝할 때 작업으로 사용할 수 있는 추적 출력을 생성하는 데 사용합니다.|**RPC:Completed**<br /><br /> **SP:StmtCompleted**<br /><br /> **SQL:BatchCompleted**|  
  
 이벤트 클래스에 대한 자세한 내용은 [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md)를 참조하십시오.  
  
## <a name="default-template"></a>기본 템플릿  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 **Standard** 템플릿을 새 추적에 적용되는 기본 템플릿으로 자동 지정합니다. 하지만 미리 정의된 템플릿 또는 사용자 정의 템플릿으로 기본 템플릿을 변경할 수 있습니다. 기본 템플릿을 변경하려면 템플릿을 만들거나 편집할 때 **추적 템플릿 속성** 대화 상자의 **일반** 탭에서 **선택한 서버 유형에 대한 기본 템플릿으로 사용** 확인란을 선택합니다.  
  
 **추적 템플릿 속성** 대화 상자는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **파일** 메뉴에서 **템플릿**을 선택한 다음, **새 템플릿** 또는 **템플릿 편집**을 클릭하면 열 수 있습니다.  
  
> [!NOTE]  
>  기본 템플릿은 지정된 서버 유형에만 사용할 수 있습니다. 한 가지 서버 유형의 기본값을 변경해도 다른 서버 유형의 기본 템플릿에는 영향을 미치지 않습니다. 특정 서버용 기본 템플릿을 설정하는 방법은 [추적 정의 기본값 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [추적 템플릿 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [추적 템플릿 수정&#40;SQL Server Profiler&#41;](./modify-trace-templates.md?view=sql-server-ver15)   
 [추적 템플릿 내보내기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)   
 [추적 템플릿 가져오기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
