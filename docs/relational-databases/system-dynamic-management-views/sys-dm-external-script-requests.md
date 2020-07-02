---
title: sys. dm_external_script_requests | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: a6fa4a695dd8d15efa6ba2f3a6c7e1ef66d3dfa3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734616"
---
# <a name="sysdm_external_script_requests"></a>sys.dm_external_script_requests
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

외부 스크립트를 실행 중인 각 활성 작업자 계정 행을 반환합니다.
  
> [!NOTE]
> 이 DMV (동적 관리 뷰)는 외부 스크립트 실행을 지 원하는 기능을 설치 하 고 사용 하도록 설정한 경우에만 사용할 수 있습니다. 자세한 내용은 [Machine Learning Services (r, Python) SQL Server 2017 이상](../../machine-learning/sql-server-machine-learning-services.md), [SQL Server 2016의 R SERVICES](../../machine-learning/r/sql-server-r-services.md)및 [Azure SQL Managed Instance의 Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 참조 하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**고유 식별자**|외부 스크립트 요청을 전송한 프로세스 ID입니다. 이는 SQL 인스턴스를 받은 프로세스 ID에 해당 합니다.|  
|language|**nvarchar**|지원되는 스크립트 언어를 나타내는 키워드입니다. |  
|degree_of_parallelism|**int**|생성된 병렬 프로세스의 수를 나타내는 숫자입니다. 이 값은 요청된 병렬 프로세스의 수와 다를 수 있습니다.|  
|external_user_name|**nvarchar**|스크립트가 실행된 Windows 작업자 계정입니다.|  
  
## <a name="permissions"></a>사용 권한

 `VIEW SERVER STATE`서버에 대 한 권한이 필요 합니다.  
  
> [!NOTE]
> 외부 스크립트를 실행 하는 사용자에 게는 추가 권한이 있어야 `EXECUTE ANY EXTERNAL SCRIPT` 하지만이 사용 권한이 없는 관리자는이 DMV를 사용할 수 있습니다. 
  
## <a name="remarks"></a>설명  

이 뷰는 스크립트 언어 식별자를 사용하여 필터링할 수 있습니다.

또한 이 뷰는 스크립트를 실행하는 작업자 계정을 반환합니다. 외부 스크립트에서 사용 하는 작업자 계정에 대 한 자세한 내용은 [SQL Server Machine Learning Services 확장성 프레임 워크의 보안 개요](../../machine-learning/concepts/security.md#sqlrusergroup)에서 처리에 사용 되는 Id (SQLRUserGroup) 섹션을 참조 하세요.

**external_script_request_id** 필드에서 반환되는 GUID는 또한 임시 파일이 저장되는 보안 디렉터리의 파일 이름을 나타냅니다. 각 작업자 계정 (예: MSSQLSERVER01)은 단일 SQL 로그인 또는 Windows 사용자를 나타내며 여러 스크립트 요청을 실행 하는 데 사용 될 수 있습니다. 기본적으로 이러한 임시 파일은 요청된 스크립트가 완료된 후 정리됩니다.

이 DMV는 활성 프로세스만 모니터링하며, 이미 완료된 스크립트에 대해서는 보고할 수 없습니다. 스크립트 기간을 추적해야 하는 경우에는 스크립트에 타이밍 정보를 추가하고 스크립트 실행의 일부로 캡처하는 것이 좋습니다.

## <a name="examples"></a>예제  
  
### <a name="viewing-the-currently-active-scripts-for-a-particular-process"></a>특정 프로세스에 대 한 현재 활성 스크립트 보기

 다음 예제에서는 현재 인스턴스에서 실행 중인 외부 스크립트 실행 수를 표시합니다.  
  
```sql
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

## <a name="see-also"></a>참고 항목

+ [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [실행 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
