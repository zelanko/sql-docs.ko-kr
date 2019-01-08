---
title: LocalDBGetVersionInfo 함수 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBGetVersionInfo
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4350badedcaf2a4e2b977b57cf9e6cfde6c1b275
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52803015"
---
# <a name="localdbgetversioninfo-function"></a>LocalDBGetVersionInfo 함수
  버전이 존재하는지 여부, 전체 LocalDB 버전 번호(빌드 및 릴리스 번호 포함)와 같이 지정한 SQL Server Express LocalDB 버전에 대한 정보를 반환합니다.  
  
 형식으로 반환 되는 정보를 `struct` 라는 **LocalDBVersionInfo**, 다음 정의는.  
  
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
 [입력] 크기를 유지 합니다 *VersionInfo* 버퍼입니다.  
  
## <a name="returns"></a>반환 값  
 S_OK  
 함수가 성공했습니다.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB가 컴퓨터에 설치되어 있지 않습니다.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 지정한 입력 매개 변수 중 한 개 이상이 잘못되었습니다.  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../express-localdb-error-messages/localdb-error-unknown-version.md)  
 지정된 LocalDB 버전이 없습니다.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 예기치 않은 오류가 발생했습니다. 자세한 내용은 이벤트 로그를 참조하십시오.  
  
## <a name="details"></a>설명  
 미치는 근거 합니다 `struct` 크기 인수 (*lpVersionInfoSize*)의 서로 다른 버전을 반환 하는 API를 사용 하도록 설정 하는 것을 **LocalDBVersionInfostruct**, 효과적으로 및 이전 버전과 호환성을 사용 하도록 설정 합니다.  
  
 경우는 `struct` 크기 인수 (*lpVersionInfoSize*)가 알려진된 버전의 크기와 일치 합니다 **LocalDBVersionInfostruct**, 해당 버전의는 `struct` 반환 됩니다. 그렇지 않으면 LOCALDB_ERROR_INVALID_PARAMETER가 반환됩니다.  
  
 일반적인 예로 **LocalDBGetVersionInfo** API 사용법은 다음과 같습니다.  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>Remarks  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Express LocalDB 헤더 및 버전 정보](sql-server-express-localdb-header-and-version-information.md)  
  
  
