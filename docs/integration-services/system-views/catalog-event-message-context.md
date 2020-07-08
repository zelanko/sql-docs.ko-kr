---
title: catalog.event_message_context | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 273a54f8-b107-4f36-9461-2b475644760d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c8094953924958f8f00db6d03ebafef0435223de
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85673240"
---
# <a name="catalogevent_message_context"></a>catalog.event_message_context 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버의 실행에 대한 실행 이벤트 메시지와 연결된 조건에 대한 정보를 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|Context_id|bigint|오류 컨텍스트의 고유 ID입니다.|  
|Event_message_id|bigint|컨텍스트와 관련된 메시지의 고유 ID입니다.|  
|Context_depth|int|수준이 증가함에 따라 컨텍스트가 오류에서 더 멀어집니다. 오류가 발생하면 컨텍스트 수준이 1에서 시작합니다. 값 0은 실행이 시작되기 전의 패키지 상태를 나타냅니다.|  
|Package_path|Nvarchar(max)|컨텍스트 원본의 패키지 경로입니다.|  
|Context_type|smallint|컨텍스트의 원본인 개체의 유형입니다. 컨텍스트 유형 목록은 **주의** 섹션을 참조하십시오.|  
|Context_source_name|Nvarchar(4000)|컨텍스트의 원본인 개체의 이름입니다.|  
|Context_source_id|Nvarchar(38)|컨텍스트의 원본인 개체의 고유 ID입니다.|  
|Property_name|Nvarchar(4000)|컨텍스트의 원본에 연결된 속성의 이름입니다.|  
|Property_value|Sql_variant|컨텍스트의 원본에 연결된 속성 값입니다.|  
  
## <a name="remarks"></a>설명  
 다음 표에서는 컨텍스트 유형을 나열합니다.  
  
||||  
|-|-|-|  
|컨텍스트 유형 값|유형 이름|Description|  
|10|Task|오류가 발생할 당시의 태스크 상태입니다.|  
|20|파이프라인|파이프라인 구성 요소의 오류: 원본, 대상 또는 변환 구성 요소.|  
|30|시퀀스|시퀀스의 상태입니다.|  
|40|For 루프|For Loop의 상태입니다.|  
|50|Foreach 루프|Foreach Loop의 상태입니다.|  
|60|패키지|오류가 발생할 당시의 패키지 상태입니다.|  
|70|변수|변수 값|  
|80|ODBC 대상 편집기|연결 관리자의 속성입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   작업에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
  
