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
ms.openlocfilehash: cce316685bccb2724eb89965e4e466fe58fb807e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027734"
---
# <a name="localdbgetversioninfo-function"></a>LocalDBGetVersionInfo 함수
  버전이 존재하는지 여부, 전체 LocalDB 버전 번호(빌드 및 릴리스 번호 포함)와 같이 지정한 SQL Server Express LocalDB 버전에 대한 정보를 반환합니다.  
  
 정보는 다음 정의를 포함 하는 명명 된 LocalDBVersionInfo 형식으로 반환 됩니다 `struct` . **LocalDBVersionInfo**  
  
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
 입력 *VersionInfo* 버퍼의 크기를 유지 합니다.  
  
## <a name="returns"></a>반환  
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
  
## <a name="details"></a>세부 정보  
 `struct`크기 인수 (*lpVersionInfoSize*)를 도입 하는 이유는 API에서 다른 버전의 **LocalDBVersionInfostruct**를 반환할 수 있도록 하 여 전달 및 이전 버전과의 호환성을 효과적으로 설정 하는 것입니다.  
  
 `struct`Size 인수 (*lpVersionInfoSize*)가 알려진 버전의 **LocalDBVersionInfostruct**크기와 일치 하면 해당 버전의 `struct` 이 반환 됩니다. 그렇지 않으면 LOCALDB_ERROR_INVALID_PARAMETER가 반환됩니다.  
  
 **LocalDBGetVersionInfo** API 사용의 일반적인 예는 다음과 같습니다.  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>설명  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Express LocalDB 헤더 및 버전 정보](sql-server-express-localdb-header-and-version-information.md)  
  
  
