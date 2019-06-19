---
title: catalog.executable_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 3dda28d6-10d8-4294-9b5e-a6048c07faf9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 34c282905f5314772a11318bf7c3eb60650e96fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65714956"
---
# <a name="catalogexecutablestatistics"></a>catalog.executable_statistics 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  실행 파일의 각 반복을 포함하여 실행되는 각 실행 파일에 대한 행을 표시합니다.  
  
 실행 개체는 사용자가 패키지의 제어 흐름에 추가하는 태스크 또는 컨테이너입니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|Statistics_id|BIGINT|데이터의 고유 ID입니다.|  
|Execution_id|BIGINT|실행 인스턴스의 고유 ID입니다.<br /><br /> catalog.executions 뷰는 실행에 대한 추가 정보를 제공합니다. 자세한 내용은 [catalog.executions &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)를 참조하세요.|  
|Executable_id|BIGINT|패키지 구성 요소의 고유 ID입니다.<br /><br /> catalog.executables 뷰는 실행 파일에 대한 추가 정보를 제공합니다. 자세한 내용은 [catalog.executables](../../integration-services/system-views/catalog-executables.md)를 참조하세요.|  
|Execution_path|nvarchar(max)|구성 요소의 각 반복을 포함하는 패키지 구성 요소의 전체 실행 경로입니다.|  
|Start_time|datetimeoffset(7)|실행 파일이 실행 전 단계에 진입하는 시간입니다.|  
|End_time|datetimeoffset(7)|실행 파일이 실행 후 단계에 진입하는 시간입니다.|  
|Execution_duration|ssNoversion|실행 파일이 실행에 소비한 시간입니다. 값은 밀리초 단위입니다.|  
|Execution_result|SMALLINT|가능한 값은 다음과 같습니다.<br /><br /> 0(성공)<br /><br /> 1(실패)<br /><br /> 2(완료)<br /><br /> 3(취소됨)|  
|Execution_value|sql_variant|실행에 의해 반환되는 값입니다. 사용자 정의 값입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
  
