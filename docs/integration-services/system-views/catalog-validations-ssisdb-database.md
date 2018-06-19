---
title: catalog.validations(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: dbafe110-b480-48f3-b45f-31d71ca68f62
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4409c736d53617d87c6d2a36f1f50b4eab4ee2b3
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403885"
---
# <a name="catalogvalidations-ssisdb-database"></a>catalog.validations(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 모든 프로젝트 및 패키지 유효성 검사에 대한 자세한 정보를 표시합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|validation_id|**bigint**|유효성 검사의 고유 식별자(ID)입니다.|  
|environment_scope|**Char(1)**|유효성 검사에서 고려되는 환경 참조를 나타냅니다. 값이 `A`이면 프로젝트와 연결된 모든 환경 참조가 유효성 검사에 포함되고, 값이 `S`이면 단일 환경 참조만 포함됩니다. 또한 값이 `D`이면 아무 환경 참조도 포함되지 않습니다. 이 경우 유효성 검사를 통과하려면 각 매개 변수 값이 리터럴 기본값이어야 합니다.|  
|validate_type|**Char(1)**|수행할 유효성 검사의 유형입니다. 가능한 유효성 검사 유형은 종속성 유효성 검사(`D`) 또는 전체 유효성 검사(`F`)입니다. 패키지 유효성 검사는 항상 전체 유효성 검사입니다.|  
|folder_name|**nvarchar(128)**|해당 프로젝트가 있는 폴더의 이름입니다.|  
|project_name|**nvarchar(128)**|프로젝트의 이름입니다.|  
|project_lsn|**bigint**|유효성을 검사할 프로젝트의 버전입니다.|  
|use32bitruntime|**bit**|64비트 운영 체제에서 32비트 런타임을 사용하여 패키지를 실행해야 하는지 여부를 나타냅니다. 값이 `1`이면 32비트 런타임으로 실행이 수행됩니다. 값이 `0`이면 64비트 런타임으로 실행이 수행됩니다.|  
|reference_id|**bigint**|프로젝트에서 환경을 참조하는 데 사용된 프로젝트-환경 참조의 고유 ID입니다.|  
|operation_type|**smallint**|작업의 유형입니다. 이 뷰에 표시되는 작업은 프로젝트 유효성 검사(`300`) 및 패키지 유효성 검사(`301`)입니다.|  
|object_name|**nvarhcar(260)**|개체 이름입니다.|  
|object_type|**smallint**|개체의 유형입니다. 개체는 프로젝트(`20`) 또는 패키지(`30`)일 수 있습니다.|  
|object_id|**bigint**|작업의 영향을 받는 개체의 ID입니다.|  
|start_time|**datetimeoffset(7)**|작업이 시작된 시간입니다.|  
|end_time|**datetimeoffsset(7)**|작업이 종료된 시간입니다.|  
|상태|**int**|작업의 상태입니다. 가능한 값은 생성됨(`1`), 실행 중(`2`), 취소됨(`3`), 실패(`4`), 보류 중(`5`), 갑자기 종료됨(`6`), 성공(`7`), 중지 중(`8`) 및 완료(`9`)입니다.|  
|caller_sid|**varbinary(85)**|Windows 인증을 사용하여 로그온한 사용자의 보안 ID(SID)입니다.|  
|caller_name|**nvarchar(128)**|작업을 수행한 계정의 이름입니다.|  
|process_id|**int**|외부 프로세스의 프로세스 ID입니다(해당되는 경우).|  
|stopped_by_sid|**varbinary(85)**|작업을 중지한 사용자의 SID입니다.|  
|stopped_by_name|**nvarchar(128)**|작업을 중지한 사용자의 이름입니다.|  
|server_name|**nvarchar(128)**|Windows 서버 및 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 인스턴스 정보입니다.|  
|machine_name|**nvarchar(128)**|서버 인스턴스가 실행 중인 컴퓨터 이름입니다.|  
|dump_id|**uniqueidentifier**|실행 덤프의 ID입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 각 유효성 검사에 대한 하나의 행을 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   해당 작업에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
