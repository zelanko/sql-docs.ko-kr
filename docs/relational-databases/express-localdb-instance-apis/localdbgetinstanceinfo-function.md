---
title: LocalDBGetInstanceInfo 함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBGetInstanceInfo
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 231706f5-26c6-42eb-ab47-315df6b8f824
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b392098091a3a439271a6f01a28ae152405e17b7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789499"
---
# <a name="localdbgetinstanceinfo-function"></a>LocalDBGetInstanceInfo 함수
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  인스턴스가 존재하는지 여부, 인스턴스가 사용하는 LocalDB 버전, 인스턴스가 실행되는지 여부 등과 같이 지정한 SQL Server Express LocalDB 인스턴스에 대한 정보를 반환합니다.  
  
 이 정보는 다음 정의가 포함 된 **Localdbinstanceinfo**라는 **구조체** 에서 반환 됩니다.  
  
```  
typedef struct _LocalDBInstanceInfo  
{  
      // Contains the size of the LocalDBInstanceInfo struct  
      DWORD  cbLocalDBInstanceInfoSize;  
  
      // Holds the instance name  
      TLocalDBInstanceNamewszInstanceName;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // TRUE if the instance configuration registry is corrupted, FALSE otherwise  
      BOOLbConfigurationCorrupted;  
  
      // TRUE if the instance is running at the moment, FALSE otherwise  
      BOOL   bIsRunning;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
  
      // Holds the date and time when the instance was started for the last time  
      FILETIME ftLastStartUTC;  
  
      // Holds the name of the TDS named pipe to connect to the instance  
      WCHARwszConnection;  
  
      // TRUE if the instance is shared, FALSE otherwise  
      BOOLbIsShared;  
  
      // Holds the shared name for the instance (if the instance is shared)  
      TLocalDBInstanceNamewszSharedInstanceName;  
  
      // Holds the SID of the instance owner (if the instance is shared)  
      WCHARwszOwnerSID;   
  
      // TRUE if the instance is Automatic, FALSE otherwise  
      BOOLbIsAutomatic;  
} LocalDBInstanceInfo;  
  
```  
  
 **헤더 파일:** sqlncli.h  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT LocalDBGetInstanceInfo(  
           PCWSTR wszInstanceName,  
           PLocalDBInstanceInfo pInstanceInfo,  
           DWORD dwInstanceInfoSize   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 *wszInstanceName*  
 [입력] 인스턴스 이름입니다.  
  
 *pInstanceInfo*  
 [출력] LocalDB 인스턴스에 대한 정보를 저장하는 버퍼입니다.  
  
 *dwInstanceInfoSize*  
 입력 *Instanceinfo* 버퍼의 크기를 저장 합니다.  
  
## <a name="returns"></a>반환  
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
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 인스턴스를 저장할 경로가 MAX_PATH보다 깁니다.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 인스턴스 폴더에 액세스할 수 없습니다.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 인스턴스 레지스트리에 액세스할 수 없습니다.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 인스턴스 구성이 손상되었습니다.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 예기치 않은 오류가 발생했습니다. 자세한 내용은 이벤트 로그를 참조하십시오.  
  
## <a name="details"></a>세부 정보  
 **Struct** size 인수 (*Lpinstanceinfosize*)의 도입에 대 한 근거는 API가 다른 버전의 **localdbinstanceinfostruct**를 반환할 수 있도록 하 여 전달 및 이전 버전과의 호환성을 효과적으로 설정 하는 것입니다.  
  
 **Struct** size 인수 (*Lpinstanceinfosize*)가 알려진 버전의 **localdbinstanceinfostruct**크기와 일치 하면 해당 버전의 **구조체가** 반환 됩니다. 그렇지 않으면 LOCALDB_ERROR_INVALID_PARAMETER가 반환됩니다.  
  
 **Localdbgetinstanceinfo** API 사용의 일반적인 예는 다음과 같습니다.  
  
```  
LocalDBInstanceInfo ii;  
LocalDBInstanceInfo(L"Test", &ii, sizeof(LocalDBInstanceInfo));  
  
```  
  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Express LocalDB 헤더 및 버전 정보](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
