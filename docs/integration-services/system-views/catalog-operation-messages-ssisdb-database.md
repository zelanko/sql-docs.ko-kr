---
title: catalog.operation_messages(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- catalog.operation_messages view [Integration Services]
- operation_messages view [Integration Services]
ms.assetid: 0b3cbe38-ce24-47ca-83ef-6538a5299d1a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5f7d0441ad9c74f6d481138ea56c090e5689ed04
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogoperationmessages-ssisdb-database"></a>catalog.operation_messages(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에서 작업 중에 기록된 메시지를 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|operation_message_id|**bigint**|메시지의 고유 식별자(ID)입니다.|  
|operation_id|**bigint**|작업의 고유 ID입니다.|  
|message_time|**datetimeoffset(7)**|메시지가 생성된 시간입니다.|  
|message_type|**smallint**|표시된 메시지의 유형입니다.|  
|message_source_type|**smallint**|메시지 원본 유형의 ID입니다.|  
|message|**nvarchar(max)**|메시지의 텍스트입니다.|  
|extended_info_id|**bigint**|작업 메시지와 관련된 추가 정보의 ID는 [extended_operation_info](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) 뷰에서 확인할 수 있습니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 카탈로그에서 작업하는 동안 기록된 각 메시지에 대한 행을 표시합니다. 메시지는 서버, 패키지 실행 프로세스 또는 실행 엔진에서 생성할 수 있습니다.  
  
 이 뷰는 다음과 같은 메시지 유형을 표시합니다.  
  
|**message_type** 값|Description|  
|-----------------------------|-----------------|  
|-1|Unknown|  
|120|Error|  
|110|경고|  
|70|정보|  
|10|사전 유효성 검사|  
|20|사후 유효성 검사|  
|30|실행 전|  
|40|실행 후|  
|60|진행|  
|50|StatusChange|  
|100|QueryCancel|  
|130|TaskFailed|  
|90|진단|  
|200|사용자 지정|  
|140|DiagnosticEx<br /><br /> 이 이벤트는 패키지 실행 태스크가 자식 패키지를 실행할 때마다 기록됩니다. 이 이벤트 메시지는 자식 패키지에 전달된 매개 변수 값으로 구성됩니다.<br /><br /> DiagnosticEx에 대한 메시지 열 값은 XML 텍스트입니다.|  
|400|NonDiagnostic|  
|80|VariableValueChanged|  
  
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
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
