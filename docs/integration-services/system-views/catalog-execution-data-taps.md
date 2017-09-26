---
title: catalog.execution_data_taps | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 54226c01-5b8f-4730-8a5f-1da2613f9689
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bc949b9b6111c65d6faa43a118efd03068630fe0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutiondatataps"></a>catalog.execution_data_taps
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  실행 중에 정의된 각 데이터 탭에 대한 정보를 표시 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|데이터 탭의 고유 ID(식별자)입니다.|  
|execution_id|**bigint**|실행 인스턴스의 고유 식별자(ID)입니다.|  
|package_path|**nvarchar(max)**|데이터 탭이 수행되는 데이터 흐름 태스크의 패키지 경로입니다.|  
|dataflow_path_id_string|**nvarchar(4000)**|데이터 흐름 경로의 ID 문자열입니다.|  
|dataflow_task_guid|**uniqueidentifier**|데이터 흐름 태스크의 고유 ID입니다.|  
|max_rows|**int**|캡처할 행의 수입니다. 이 값을 지정하지 않으면 모든 행이 캡처됩니다.|  
|filename|**nvarchar(4000)**|데이터 덤프 파일의 이름입니다. 자세한 내용은 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)을 참조하세요.|  
  
## <a name="permissions"></a>Permissions  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [패키지 실행을 위한 덤프 파일 생성](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
