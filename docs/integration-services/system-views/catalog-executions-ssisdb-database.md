---
title: catalog.executions(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- executions view [Integration Services]
- catalog.executions view [Integration Services]
ms.assetid: 879f13b0-331d-4dee-a079-edfaca11ae5b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 448c5ad08939be34ade1dd55b28b1d8f354c98c2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85672370"
---
# <a name="catalogexecutions-ssisdb-database"></a>catalog.executions(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 패키지 실행 인스턴스를 표시합니다. 패키지 실행 태스크로 실행되는 패키지는 부모 패키지와 같은 실행 인스턴스에서 실행됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|execution_id|**bigint**|실행 인스턴스의 고유 식별자(ID)입니다.|  
|folder_name|**sysname(nvarchar(128))**|프로젝트가 있는 폴더의 이름입니다.|  
|project_name|**sysname(nvarchar(128))**|프로젝트의 이름입니다.|  
|package_name|**nvarchar(260)**|실행 중에 시작된 첫 번째 패키지의 이름입니다.|  
|reference_id|**bigint**|실행 인스턴스에서 참조하는 환경입니다.|  
|reference_type|**char(1)**|환경을 프로젝트와 같은 폴더(상대 참조)에서 찾을 수 있는지, 아니면 다른 폴더(절대 참조)에서 찾을 수 있는지를 나타냅니다. 값이 `R`이면 상대 참조를 사용하여 환경을 찾고, 값이 `A`이면 절대 참조를 사용하여 환경을 찾습니다.|  
|environment_folder_name|**nvarchar(128)**|환경이 있는 폴더의 이름입니다.|  
|environment_name|**nvarchar(128)**|실행 중에 참조된 환경의 이름입니다.|  
|project_lsn|**bigint**|실행 인스턴스에 해당하는 프로젝트의 버전입니다. 이 번호는 순차적이지 않을 수 있습니다.|  
|executed_as_sid|**varbinary(85)**|실행 인스턴스를 시작한 사용자의 SID입니다.|  
|executed_as_name|**nvarchar(128)**|실행 인스턴스를 시작하는 데 사용된 데이터베이스 보안 주체의 이름입니다.|  
|use32bitruntime|**bit**|64비트 운영 체제에서 32비트 런타임을 사용하여 패키지를 실행해야 하는지 여부를 나타냅니다. 값이 `1`이면 32비트 런타임으로 실행이 수행됩니다. 값이 `0`이면 64비트 런타임으로 실행이 수행됩니다.|  
|object_type|**smallint**|개체의 유형입니다. 개체는 프로젝트(`20`) 또는 패키지(`30`)일 수 있습니다.|  
|object_id|**bigint**|작업의 영향을 받는 개체의 ID입니다.|  
|상태|**int**|작업의 상태. 가능한 값은 생성됨(`1`), 실행 중(`2`), 취소됨(`3`), 실패(`4`), 보류 중(`5`), 갑자기 종료됨(`6`), 성공(`7`), 중지 중(`8`) 및 완료(`9`)입니다.|  
|start_time|**datetimeoffset**|실행 인스턴스가 시작된 시간입니다.|  
|end_time|**datetimeoffsset**|실행 인스턴스가 종료된 시간입니다.|  
|caller_sid|**varbinary(85)**|Windows 인증을 사용하여 로그온한 사용자의 보안 ID(SID)입니다.|  
|caller_name|**nvarchar(128)**|작업을 수행한 계정의 이름입니다.|  
|process_id|**int**|외부 프로세스의 프로세스 ID입니다(해당되는 경우).|  
|stopped_by_sid|**varbinary(85)**|실행 인스턴스를 중지한 사용자의 보안 ID(SID)입니다.|  
|stopped_by_name|**nvarchar(128)**|실행 인스턴스를 중지한 사용자의 이름입니다.|  
|total_physical_memory_kb|**bigint**|실행이 시작될 때 서버의 실제 메모리 전체 크기(MB)입니다.|  
|available_physical_memory_kb|**bigint**|실행이 시작될 때 서버의 가용 실제 메모리 전체 크기(MB)입니다.|  
|total_page_file_kb|**bigint**|실행이 시작될 때 서버의 페이지 메모리 전체 크기(MB)입니다.|  
|available_page_file_kb|**bigint**|실행이 시작될 때 서버의 가용 페이지 메모리 전체 크기(MB)입니다.|  
|cpu_count|**int**|실행이 시작될 때 서버의 논리적 CPU 수입니다.|  
|server_name|**nvarchar(128)**|Windows 서버 및 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 인스턴스 정보입니다.|  
|machine_name|**nvarchar(128)**|서버 인스턴스가 실행 중인 컴퓨터 이름입니다.|  
|dump_id|**uniqueidentifier**|실행 덤프의 ID입니다.|  
  
## <a name="remarks"></a>설명  
 이 뷰는 카탈로그의 각 실행 인스턴스에 대한 행을 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
