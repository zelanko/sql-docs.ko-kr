---
title: catalog.event_messages | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a31a654f-31e9-4da1-aabf-182b07848e36
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a0db5ace2a95bea93189cb48378b01a4ba599942
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogeventmessages"></a>catalog.event_messages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  작업 중 기록된 메시지에 대한 정보를 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|Event_message_ID|bigint|이벤트 메시지의 고유 ID입니다.|  
|Operation_id|bigint|작업의 유형입니다.<br /><br /> 작업 유형 목록은 참조 [catalog.operations &#40; SSISDB 데이터베이스 &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md).|  
|Message_time|datetimeoffset(7)|메시지가 생성된 시간입니다.|  
|Message_type|smallint|표시된 메시지의 유형입니다. 메시지 유형에 대 한 자세한 내용은 참조 [catalog.operation_messages &#40; SSISDB 데이터베이스 &#41; ](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md).|  
|Message_source_type|smallint|메시지의 원본입니다.|  
|message|nvarchar(max)|메시지의 텍스트입니다.|  
|Extended_info_id|bigint|작업 메시지 관련 추가 정보의 ID에서 발견 된 [catalog.extended_operation_info &#40; SSISDB 데이터베이스 &#41; ](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) 보기.|  
|Package_name|nvarchar(260)|패키지 파일의 이름입니다.|  
|Event_name|nvarchar (1024)|메시지에 연결된 런타임 이벤트입니다.|  
|Message_source_name|nvarchar(4000)|메시지의 원본인 패키지 구성 요소입니다.|  
|Message_source_id|nvarchar(38)|메시지 원본의 고유 ID입니다.|  
|Subcomponent_name|nvarchar(4000)|메시지의 원본인 데이터 흐름 구성 요소입니다.<br /><br /> [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 엔진에서 메시지를 반환하면 이 열에 SSIS.Pipeline이 표시됩니다.|  
|Package_path|nvarchar(max)|패키지 내 구성 요소의 고유 경로입니다.|  
|Execution_path|nvarchar(max)|부모 패키지에서 구성 요소가 실행되는 지점까지의 전체 경로입니다.<br /><br /> 이 경로도 구성 요소의 반복을 캡처합니다.|  
|threadID|int|메시지가 기록될 때 실행 중인 스레드의 ID입니다.|  
|Message_code|int|메시지에 연결된 코드입니다.|  
  
## <a name="remarks"></a>주의  
 이 뷰는 다음과 같은 메시지 원본 유형을 표시합니다.  
  
|**message_source_type**|Description|  
|-------------------------------|-----------------|  
|10|T-SQL 및 CLR 저장 프로시저와 같은 API 항목|  
|20|패키지(ISServerExec.exe)를 실행하는 데 사용되는 외부 프로세스|  
|30|패키지 수준 개체|  
|40|제어 흐름 태스크|  
|50|제어 흐름 컨테이너|  
|60|데이터 흐름 태스크|  
  
## <a name="permissions"></a>Permissions  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   작업에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할입니다.  
  
-   멤버 자격에는 **sysadmin** 서버 역할입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
  

