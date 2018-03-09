---
title: "LocalDBStopInstance 함수 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- LocalDBStopInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 4bd73187-0aac-4f03-ac54-2b78e41917e5
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bde22cf301e05030402df861a137ae0c5070d2c4
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="localdbstopinstance-function"></a>LocalDBStopInstance 함수
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
지정한 SQL Server Express LocalDB 인스턴스의 실행을 중지합니다.  
  
 **헤더 파일:** sqlncli.h  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT LocalDBStopInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           ULONG ulTimeout   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 *pInstanceName*  
 [입력] 중지할 LocalDB 인스턴스의 이름입니다.  
  
 *dwFlags*  
 [입력] 인스턴스를 중지할 방법을 지정하는 플래그 값 중 하나 또는 값의 조합입니다.  
  
 사용 가능한 플래그:  
  
 LOCALDB_SHUTDOWN_KILL_PROCESS  
 프로세스 중지 운영 체제 명령을 사용하여 즉시 종료합니다.  
  
 LOCALDB_SHUTDOWN_WITH_NOWAIT  
 WITH NOWAIT 옵션 Transact-SQL 명령을 사용하여 종료합니다.  
  
 플래그를 설정하지 않은 경우 LocalDB 인스턴스는 SHUTDOWN Transact-SQL 명령을 사용하여 종료됩니다. 두 플래그를 모두 설정한 경우 LOCALDB_SHUTDOWN_KILL_PROCESS 플래그가 우선적으로 사용됩니다.  
  
 *ulTimeout*  
 [입력] 이 작업이 완료될 때까지 대기할 시간(초)입니다. 이 값이 0인 경우 이 함수는 LocalDB 인스턴스가 중지될 때까지 대기하지 않고 즉시 반환됩니다.  
  
## <a name="returns"></a>반환 값  
 S_OK  
 함수가 성공했습니다.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB가 컴퓨터에 설치되어 있지 않습니다.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 지정한 입력 매개 변수 중 한 개 이상이 잘못되었습니다.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 지정한 인스턴스 이름이 잘못되었습니다.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-instance.md)  
 인스턴스가 없습니다.  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../../relational-databases/express-localdb-error-messages/localdb-error-wait-timeout.md)  
 동기화 잠금을 획득하려고 시도하는 동안 제한 시간이 발생했습니다.  
  
 [LOCALDB_ERROR_INSTANCE_STOP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-instance-stop-failed.md)  
 지정된 시간 내에 중지 작업을 완료하지 못했습니다.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 인스턴스를 저장할 경로가 MAX_PATH보다 깁니다.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 사용자 프로필 폴더를 검색할 수 없습니다.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 인스턴스 폴더에 액세스할 수 없습니다.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 인스턴스 레지스트리에 액세스할 수 없습니다.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 인스턴스 구성이 손상되었습니다.  
  
 [LOCALDB_ERROR_CALLER_IS_NOT_OWNER](../../relational-databases/express-localdb-error-messages/localdb-error-caller-is-not-owner.md)  
 API 호출자는 LocalDB 인스턴스 소유자가 아닙니다.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 예기치 않은 오류가 발생했습니다. 자세한 내용은 이벤트 로그를 참조하십시오.  
  
## <a name="remarks"></a>주의  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Express LocalDB 헤더 및 버전 정보](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
