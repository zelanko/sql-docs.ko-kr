---
title: sys.dm_external_script_requests | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_requests
- sys.dm_external_script_requests_TSQL
- dm_external_script_requests
- dm_external_script_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_requests dynamic management view
ms.assetid: e7e7c50f-b8b2-403c-b8c8-1955da5636c3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54c572acac645146e3db18195a0dbe5b794effdc
ms.sourcegitcommit: c2322c1a1dca33b47601eb06c4b2331b603829f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50743191"
---
# <a name="sysdmexternalscriptrequests"></a>sys.dm_external_script_requests
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

외부 스크립트를 실행 중인 각 활성 작업자 계정 행을 반환합니다.
  
> [!NOTE] 
>  
> 이 동적 관리 뷰 (DMV)는 설치 하 고 외부 스크립트 실행을 지 원하는 기능을 사용 하도록 설정 하는 경우에 사용할 수 있습니다. 자세한 내용은 [SQL Server 2016에서 R Services](../../advanced-analytics/r/sql-server-r-services.md) 하 고 [Machine Learning 서비스 (R, Python) SQL Server 2017의](../../advanced-analytics/what-is-sql-server-machine-learning.md)합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**고유 식별자**|외부 스크립트 요청을 전송한 프로세스 ID입니다. 받은 프로세스 ID에 해당 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]|  
|language|**nvarchar**|지원되는 스크립트 언어를 나타내는 키워드입니다. |  
|degree_of_parallelism|**int**|생성된 병렬 프로세스의 수를 나타내는 숫자입니다. 이 값은 요청된 병렬 프로세스의 수와 다를 수 있습니다.|  
|external_user_name|**nvarchar**|스크립트가 실행된 Windows 작업자 계정입니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
> [!NOTE]
>   
>  외부 스크립트를 실행하는 사용자에게는 추가 권한 EXECUTE ANY EXTERNAL SCRIPT가 있어야 합니다. 하지만 이 DMV는 이 권한이 없는 관리자가 사용할 수 있습니다. 
  
## <a name="remarks"></a>Remarks  

이 뷰는 스크립트 언어 식별자를 사용하여 필터링할 수 있습니다.

또한 이 뷰는 스크립트를 실행하는 작업자 계정을 반환합니다. 외부 스크립트를 사용 하는 작업자 계정에 대 한 자세한 (SQLRUserGroup) 섹션에서 처리에 사용 된 Id 참조 [SQL Server Machine Learning Services의 확장성 프레임 워크에 대 한 보안 개요](../../advanced-analytics/concepts/security.md#sqlrusergroup)합니다.

**external_script_request_id** 필드에서 반환되는 GUID는 또한 임시 파일이 저장되는 보안 디렉터리의 파일 이름을 나타냅니다. MSSQLSERVER01과 같은 작업자 계정은 각각 단일 SQL 로그인 또는 Windows 사용자를 나타내며 여러 스크립트 요청을 실행하는 데 사용할 수 있습니다. 기본적으로 이러한 임시 파일은 요청된 스크립트가 완료된 후 정리됩니다.
 
이 DMV는 활성 프로세스만 모니터링하며, 이미 완료된 스크립트에 대해서는 보고할 수 없습니다. 스크립트 기간을 추적해야 하는 경우에는 스크립트에 타이밍 정보를 추가하고 스크립트 실행의 일부로 캡처하는 것이 좋습니다.

## <a name="examples"></a>예  
  
### <a name="viewing-the-currently-active-r-scripts-for-a-particular-process"></a>특정 프로세스에 대한 현재 활성 R 스크립트 보기 
 다음 예제에서는 현재 인스턴스에서 실행 중인 외부 스크립트 실행 수를 표시합니다.  
  
```  
SELECT external_script_request_id 
  , [language]
  , degree_of_parallelism
  , external_user_name
FROM sys.dm_external_script_requests; 
```  

결과  


external_script_request_id  |language  |degree_of_parallelism  |external_user_name  
---------|---------|---------|---------
183EE6FC-7399-4318-AA2E-7A6C68E435A8     |     R    |      1   |  MSSQLSERVER01       


  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

