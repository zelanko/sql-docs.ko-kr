---
title: SQL Server 확장 이벤트 (XEvents)를 사용 하 여 Analysis Services를 모니터링할 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b57cc2fe-52dc-4fa9-8554-5a866e25c6d7
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: eb67c1eca2b803c01a3716708f73afbb3861476a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182679"
---
# <a name="use-sql-server-extended-events-xevents-to-monitor-analysis-services"></a>SQL Server 확장 이벤트(XEvent)를 사용하여 Analysis Services 모니터링
  Analysis Services의 사용을 통해 추적 기능을 제공 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)합니다.  
  
 확장 이벤트는 서버 시스템에 대해 구성할 수 있는 확장성이 높은 이벤트 인프라입니다. 확장 이벤트는 성능 리소스를 적게 사용하는 간단한 성능 모니터링 시스템입니다.  
  
 모든 Analysis Services 이벤트를 캡처할 수 있습니다 및 대상에 정의 된 대로 특정 소비자에 게 [확장 이벤트](../../relational-databases/extended-events/extended-events.md), XEvents를 통해.  
  
## <a name="initiating-extended-events-in-analysis-services"></a>Analysis Services에서 확장 이벤트 시작  
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
 노출할 Analysis Services 이벤트입니다. 이벤트의 이름은 [Analysis Services 추적 이벤트](../trace-events/analysis-services-trace-events.md) 를 참조하세요.  
  
 *data_filename*  
 이벤트 데이터가 포함된 파일의 이름입니다. 추적을 반복적으로 보내는 경우 데이터를 덮어쓰지 않도록 이름 뒤에 타임스탬프가 추가됩니다.  
  
 *metadata_filename*  
 이벤트 메타데이터가 포함된 파일의 이름입니다. 추적을 반복적으로 보내는 경우 데이터를 덮어쓰지 않도록 이름 뒤에 타임스탬프가 추가됩니다.  
  
## <a name="stopping-extended-events-in-analysis-services"></a>Analysis Services에서 확장 이벤트 중지  
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
  
  