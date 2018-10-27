---
title: SQL Server 확장 이벤트를 사용 하 여 Analysis Services 모니터링 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 616cc1e633d6683283d62d6fb3b3434780d9a919
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147248"
---
# <a name="monitor-analysis-services-with-sql-server-extended-events"></a>SQL Server 확장 이벤트를 사용하여 Analysis Services 모니터링
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  확장 이벤트(*xEvents*)는 매우 적은 시스템 리소스를 사용하는 경량 추적 및 성능 모니터링 시스템으로 제품 및 테스트 서버 모두에서 문제를 진단하는 데 이상적인 도구입니다. 또한, 확장성이 뛰어나고 구성 가능하며 SQL Server 2016에서는 새롭게 기본적으로 제공되는 도구 지원을 통해 쉽게 사용할 수 있습니다. SQL Server Management Studio의 Analysis Services 인스턴스에 연결에서 SQL Server Profiler를 사용하는 방식과 유사하게 실시간 추적을 구성, 실행 및 모니터링할 수 있습니다. 향상된 도구가 추가되어 SQL Server Profiler에서 xEvent를 좀 더 적절하게 교체하고 데이터베이스 엔진 및 Analysis Services 작업에서 문제를 좀 더 대칭적으로 진단할 수 있습니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]뿐만 아니라, 이전 릴리스도 지원되기 때문에 XMLA 스크립팅을 통해  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 확장 이벤트 세션을 기존 방식으로 구성할 수도 있습니다.  
  
 [Extended Events](../../relational-databases/extended-events/extended-events.md)에 정의된 것처럼 특정 소비자를 대상으로 모든 Analysis Services 이벤트를 캡처할 수 있습니다.  
  
> [!NOTE]  
>  이 [간략한 비디오 소개](https://www.youtube.com/watch?v=ja2mOHWRVC0&index=1&list=PLv2BtOtLblH1YvzQ5YnjfQFr_oKEvMk19) 를 보거나 [지원 블로그 포스트](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx) 를 읽어 SQL Server 2016의 Analysis Services용 xEvents에 대해 자세히 알아보세요.  
  
  
##  <a name="bkmk_ssas_extended_events_ssms"></a> Management Studio를 사용하여 Analysis Services 구성  
 Management Studio는 테이블 형식 및 다차원 인스턴스에 사용자가 시작한 xEvent 세션을 포함하는 새로운 관리 폴더를 제공합니다. 한 번에 여러 세션을 실행할 수 있습니다. 그러나 현재 구현에서의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 확장된 이벤트 사용자 인터페이스는 기존 세션 업데이트 또는 재생을 지원하지 않습니다.  
  
 ![ssas_extended_events_ssms_start](../../analysis-services/instances/media/ssas-extended-events-ssms-start.png "ssas_extended_events_ssms_start")  
  
 **이벤트 선택**  
  
 캡처할 이벤트를 이미 알고 있는 경우 해당 이벤트를 추적에 추가하는 가장 쉬운 방법은 검색하는 것입니다. 그렇지 않으면 다음 이벤트가 모니터링 작업에 일반적으로 사용됩니다.  
  
-   **CommandBegin** 및 **CommandEnd**  
  
-   **QueryBegin**, **QueryEnd**및 **QuerySubcubeVerbose** (서버로 전송된 전체 MDX 또는 DAX 쿼리 표시) 그리고 쿼리에서 사용되는 리소스 및 반환되는 행의 수에 대한 통계의 경우 **ResourceUsage**  
  
-   **ProgressReportBegin** 및 **ProgressReportEnd** (처리 작업)  
  
-   **AuditLogin** 및 **AuditLogout** (클라이언트 응용 프로그램이 Analysis Services에 연결되는 사용자 ID 캡처).  
  
 **데이터 저장소 선택**  
  
 세션은 Management Studio의 창으로 실시간 스트리밍되거나 Power Query 또는 Excel을 사용하여 이후 분석으로 위해 파일에 저장될 수 있습니다.  
  
-   **event_file** 은 .xel 파일의 세션 데이터를 저장합니다.  
  
-   **event_stream** 은 Management Studio에서 **라이브 데이터 감시** 옵션을 활성화합니다.  
  
-   **ring_buffer** 는 서버가 실행 중인 경우 메모리에 세션 데이터를 저장합니다. 서버가 다시 시작되면 세션 데이터가 삭제됩니다.  
  
 **이벤트 필드 추가**  
  
 이벤트 필드가 포함되도록 세션을 구성하면 유용한 정보를 쉽게 볼 수 있습니다.  
  
 **구성** 은 대화 상자의 먼 쪽에 있는 옵션입니다.  
  
 ![ssas-xevents-configure](../../analysis-services/instances/media/ssas-xevents-configure.PNG "ssas-xevents-configure")  
  
 이벤트 필드 탭의 구성에서 **TextData** 를 선택하면 이벤트 옆에 서버에서 실행 중인 쿼리 등의 반환 값을 보여주는 이 필드가 표시됩니다.  
  
 원하는 이벤트 및 데이터 저장소에 대한 세션을 구성한 후 스크립트 단추를 클릭하면 파일, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 새 쿼리 및 클립보드 등 지원되는 대상 중 하나로 구성을 전송할 수 있습니다.  
  
 **세션 새로 고침**  
  
 세션을 만든 후에 Management Studio에서 세션 폴더를 새로 고침해야 생성한 세션을 볼 수 있습니다. event_stream을 구성한 경우 세션 이름을 마우스 오른쪽 단추로 클릭하고 **라이브 데이터 감시** 를 선택하면 서버 작업을 실시간 모니터링할 수 있습니다.  
  
##  <a name="bkmk_script_start"></a> Analysis Services에서 확장 이벤트를 시작하는 XMLA 스크립트  
 확장 이벤트 추적은 다음과 같은 XMLA 개체 만들기 스크립트 명령을 사용하여 설정할 수 있습니다.  
  
```  
<Execute …>  
   <Command>  
      <Batch …>  
         <Create …>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session …>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" …/>  
                        </event>  
                        <target package="PACKAGE0" name="asynchronous_file_target">  
                           <parameter name="filename" value="data_filename.xel"/>  
                           <parameter name="metadatafile" value="metadata_filename.xem"/>  
                        </target>  
                     </event_session>  
                  </ddl300_300:XEvent>  
               </Trace>  
            </ObjectDefinition>  
         </Create>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 여기에서 다음 요소는 추적 요구 사항에 따라 사용자가 정의합니다.  
  
 *trace_id*  
 이 추적의 고유 식별자를 정의합니다.  
  
 *trace_name*  
 이 추적에 지정된 이름으로, 대개 사람이 읽을 수 있는 추적에 대한 정의입니다. *trace_id* 값을 이름으로 사용하는 것이 일반적입니다.  
  
 *AS_event*  
 노출할 Analysis Services 이벤트입니다. 이벤트의 이름은 [Analysis Services 추적 이벤트](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events) 를 참조하세요.  
  
 *data_filename*  
 이벤트 데이터가 포함된 파일의 이름입니다. 추적을 반복적으로 보내는 경우 데이터를 덮어쓰지 않도록 이름 뒤에 타임스탬프가 추가됩니다.  
  
 *metadata_filename*  
 이벤트 메타데이터가 포함된 파일의 이름입니다. 추적을 반복적으로 보내는 경우 데이터를 덮어쓰지 않도록 이름 뒤에 타임스탬프가 추가됩니다.  
  
  
##  <a name="bkmk_script_stop"></a> Analysis Services에서 확장 이벤트를 중지하는 XMLA 스크립트  
 확장 이벤트 추적 개체를 중지하려면 다음과 같은 유사한 XMLA 개체 삭제 스크립트 명령을 사용하여 해당 개체를 삭제해야 합니다.  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch …>  
         <Delete …>  
            <Object>  
               <TraceID>trace_id</TraceID>  
            </Object>  
         </Delete>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 여기에서 다음 요소는 추적 요구 사항에 따라 사용자가 정의합니다.  
  
 *trace_id*  
 삭제할 추적의 고유 식별자를 정의합니다.  
  
  
## <a name="see-also"></a>관련 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
