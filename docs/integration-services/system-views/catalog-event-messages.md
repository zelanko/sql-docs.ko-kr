---
title: catalog.event_messages | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a31a654f-31e9-4da1-aabf-182b07848e36
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e19ca7fac23979ecd691ed6cab45fa2cfec9564
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912634"
---
# <a name="catalogevent_messages"></a>catalog.event_messages 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  작업 중 기록된 메시지에 대한 정보를 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|Event_message_ID|bigint|이벤트 메시지의 고유 ID입니다.|  
|Operation_id|bigint|작업의 유형입니다.<br /><br /> 작업 유형에 대한 목록은 [catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)를 참조하세요.|  
|Message_time|datetimeoffset(7)|메시지가 생성된 시간입니다.|  
|Message_type|smallint|표시된 메시지의 유형입니다. 메시지 유형에 대한 자세한 내용은 [catalog.operation_messages &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)를 참조하세요.|  
|Message_source_type|smallint|메시지의 원본입니다.|  
|message|nvarchar(max)|메시지의 텍스트입니다.|  
|Extended_info_id|bigint|작업 메시지와 관련된 추가 정보의 ID는 [catalog.extended_operation_info &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) 뷰에서 확인할 수 있습니다.|  
|Package_name|nvarchar(260)|패키지 파일의 이름입니다.|  
|Event_name|nvarchar(1024)|메시지에 연결된 런타임 이벤트입니다.|  
|Message_source_name|nvarchar(4000)|메시지의 원본인 패키지 구성 요소입니다.|  
|Message_source_id|nvarchar(38)|메시지 원본의 고유 ID입니다.|  
|Subcomponent_name|nvarchar(4000)|메시지의 원본인 데이터 흐름 구성 요소입니다.<br /><br /> [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 엔진에서 메시지를 반환하면 이 열에 SSIS.Pipeline이 표시됩니다.|  
|Package_path|nvarchar(max)|패키지 내 구성 요소의 고유 경로입니다.|  
|Execution_path|nvarchar(max)|부모 패키지에서 구성 요소가 실행되는 지점까지의 전체 경로입니다.<br /><br /> 이 경로도 구성 요소의 반복을 캡처합니다.|  
|threadID|int|메시지가 기록될 때 실행 중인 스레드의 ID입니다.|  
|Message_code|int|메시지에 연결된 코드입니다.|  
  
## <a name="remarks"></a>설명  
 이 뷰는 다음과 같은 메시지 원본 유형을 표시합니다.  
  
|**message_source_type**|Description|  
|-------------------------------|-----------------|  
|10|T-SQL 및 CLR 저장 프로시저와 같은 API 항목|  
|20|패키지(ISServerExec.exe)를 실행하는 데 사용되는 외부 프로세스|  
|30|패키지 수준 개체|  
|40|제어 흐름 태스크|  
|50|제어 흐름 컨테이너|  
|60|데이터 흐름 태스크|  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   작업에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="see-also"></a>참고 항목  
 [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
  
