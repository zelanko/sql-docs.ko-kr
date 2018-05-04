---
title: LocalDBGetVersionInfo 함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- LocalDBGetVersionInfo
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
caps.latest.revision: 10
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 979ad0ecdfa10825bc9d131683dc88ab41779ff5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="localdbgetversioninfo-function"></a>LocalDBGetVersionInfo 함수
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  버전이 존재하는지 여부, 전체 LocalDB 버전 번호(빌드 및 릴리스 번호 포함)와 같이 지정한 SQL Server Express LocalDB 버전에 대한 정보를 반환합니다.  
  
 형태로 반환 하는 정보는 **구조체** 라는 **LocalDBVersionInfo**, 있으며 그 다음 정의 합니다.  
  
```  
typedef struct _LocalDBVersionInfo  
{  
      // Contains the size of the LocalDBVersionInfo struct  
      DWORD  cbLocalDBVersionInfoSize;  
  
      // Holds the version name  
      TLocalDBVersionwszVersion;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
} LocalDBVersionInfo;  
  
```  
  
 **헤더 파일:** sqlncli.h  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT LocalDBGetVersionInfo(  
           PCWSTR wszVersionName,           PLocalDBVersionInfo pVersionInfo,           DWORD dwVersionInfoSize);  
```  
  
## <a name="parameters"></a>매개 변수  
 *wszVersionName*  
 [입력] LocalDB 버전 이름입니다.  
  
 *pVersionInfo*  
 [출력] LocalDB 버전에 대한 정보를 저장하는 버퍼입니다.  
  
 *dwVersionInfoSize*  
 [입력] 크기를 유지는 *VersionInfo* 버퍼입니다.  
  
## <a name="returns"></a>반환 값  
 S_OK  
 함수가 성공했습니다.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB가 컴퓨터에 설치되어 있지 않습니다.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 지정한 입력 매개 변수 중 한 개 이상이 잘못되었습니다.  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-version.md)  
 지정된 LocalDB 버전이 없습니다.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 예기치 않은 오류가 발생했습니다. 자세한 내용은 이벤트 로그를 참조하십시오.  
  
## <a name="details"></a>세부 정보  
 도입 도입한 이유는 **구조체** 크기 인수 (*lpVersionInfoSize*)의 서로 다른 버전을 반환 하는 API를 사용 하도록 설정 하는 것은 **LocalDBVersionInfostruct**, 효과적으로 및 이전 버전과 호환성을 사용 하도록 설정 합니다.  
  
 경우는 **구조체** 크기 인수 (*lpVersionInfoSize*)가 알려진된 버전의 크기와 일치 하는 **LocalDBVersionInfostruct**, 해당 버전의는  **구조체** 반환 됩니다. 그렇지 않으면 LOCALDB_ERROR_INVALID_PARAMETER가 반환됩니다.  
  
 일반적인 예 **LocalDBGetVersionInfo** API 사용법은 다음과 같습니다.  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L”11.0”, &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>주의  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Express LocalDB 헤더 및 버전 정보](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
