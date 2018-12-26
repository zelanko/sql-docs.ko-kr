---
title: LocalDBStartInstance 함수 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- LocalDBStartInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: cb325f5d-10ee-4a56-ba28-db0074ab3926
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 99bec66e77a8ac5fd742ffb85b6f87dfefe88510
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159563"
---
# <a name="localdbstartinstance-function"></a>LocalDBStartInstance 함수
  지정한 SQL Server Express LocalDB 인스턴스를 시작합니다.  
  
 **헤더 파일:** sqlncli.h  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT LocalDBStartInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           LPWSTR wszSqlConnection,   
           LPDWORD lpcchSqlConnection   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 *pInstanceName*  
 [입력] 시작할 LocalDB 인스턴스의 이름입니다.  
  
 *dwFlags*  
 [입력] 나중에 사용하도록 예약되어 있습니다. 현재 0으로 설정해야 합니다.  
  
 *wszSqlConnection*  
 [출력] LocalDB 인스턴스에 연결 문자열을 저장할 버퍼입니다.  
  
 *lpcchSqlConnection*  
 [입력/출력] 출력 시 후행 Null을 포함하여 문자의 *wszSqlConnection* 버퍼 크기를 포함합니다. 출력 시 지정된 버퍼 크기가 너무 작은 경우 후행 Null을 포함하여 문자에 필요한 버퍼 크기를 포함합니다.  
  
## <a name="returns"></a>반환 값  
 S_OK  
 함수가 성공했습니다.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB가 컴퓨터에 설치되어 있지 않습니다.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 지정한 입력 매개 변수 중 한 개 이상이 잘못되었습니다.  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 지정한 인스턴스 이름이 잘못되었습니다.  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../express-localdb-error-messages/localdb-error-unknown-instance.md)  
 인스턴스가 없습니다.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 지정한 버퍼 *wszSqlConnection* 이 너무 작습니다.  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../express-localdb-error-messages/localdb-error-wait-timeout.md)  
 동기화 잠금을 획득하려고 시도하는 동안 제한 시간이 발생했습니다.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 인스턴스를 저장할 경로가 MAX_PATH보다 깁니다.  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 사용자 프로필 폴더를 검색할 수 없습니다.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 인스턴스 폴더에 액세스할 수 없습니다.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 인스턴스 레지스트리에 액세스할 수 없습니다.  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 인스턴스 레지스트리를 수정할 수 없습니다.  
  
 [LOCALDB_ERROR_CANNOT_CREATE_SQL_PROCESS](../express-localdb-error-messages/localdb-error-cannot-create-sql-process.md)  
 SQL Server에 대한 프로세스를 만들 수 없습니다.  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 SQL Server 프로세스가 시작되었지만 SQL Server 시작이 실패했습니다.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 인스턴스 구성이 손상되었습니다.  
  
 [LOCALDB_ERROR_AUTO_INSTANCE_CREATE_FAILED](../express-localdb-error-messages/localdb-error-auto-instance-create-failed.md)  
 자동 인스턴스를 만들 수 없습니다. 자세한 오류 정보는 Windows 애플리케이션 이벤트 로그를 참조하십시오.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 예기치 않은 오류가 발생했습니다. 자세한 내용은 이벤트 로그를 참조하십시오.  
  
## <a name="details"></a>설명  
 연결 버퍼 인수(*wszSqlConnection*) 및 연결 버퍼 크기 인수(*lpcchSqlConnection*)는 선택 사항입니다. 다음 표에서는 이러한 인수를 사용하기 위한 옵션과 해당 결과를 보여 줍니다.  
  
|버퍼|버퍼 크기|이유|작업|  
|------------|-----------------|---------------|------------|  
|NULL|NULL|사용자가 인스턴스를 시작하려고 하지만 파이프 이름은 필요하지 않습니다.|인스턴스를 시작합니다(파이프 반환 없음, 필요한 버퍼 크기 반환 없음).|  
|NULL|있음|사용자가 출력 버퍼 크기를 요청합니다. 다음 호출에서 사용자는 실제 시작을 요청할 수 있습니다.|필요한 버퍼 크기를 반환합니다(시작 없음, 파이프 반환 없음). 결과는 S_OK입니다.|  
|있음|NULL|허용되지 않으며 잘못된 입력입니다.|반환된 결과는 LOCALDB_ERROR_INVALID_PARAMETER입니다.|  
|있음|있음|사용자가 인스턴스를 시작하려고 하며 인스턴스가 시작된 후 인스턴스에 연결하기 위해 파이프 이름이 필요합니다.|버퍼 크기를 검사하고, 인스턴스를 시작하며 버퍼의 파이프 이름을 반환합니다. <br />버퍼 크기 인수는 종료 Null을 포함하지 않은 “server=” 문자열을 반환합니다.|  
  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Express LocalDB 헤더 및 버전 정보](sql-server-express-localdb-header-and-version-information.md)  
  
  
