---
title: LocalDBGetVersions 함수 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBGetVersions
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 033a9c6b-0d7f-4f8a-ab60-33cd6fee0d33
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e8b02f89903475462265ffc154553c176951c259
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027674"
---
# <a name="localdbgetversions-function"></a>LocalDBGetVersions 함수
  컴퓨터에서 사용할 수 있는 모든 SQL Server Express LocalDB 버전을 반환합니다.  
  
 **헤더 파일:** sqlncli.h  
  
## <a name="syntax"></a>구문  
  
```  
#define MAX_LOCALDB_VERSION_LENGTH 43typedef WCHAR TLocalDBVersion[MAX_LOCALDB_VERSION_LENGTH + 1];typedef TLocalDBVersion* PTLocalDBVersion;HRESULT LocalDBGetVersions(           PTLocalDBVersion pVersion,           LPDWORD lpdwNumberOfVersions);  
```  
  
## <a name="parameters"></a>매개 변수  
 *pVersionNames*  
 출력 사용자의 워크스테이션에서 사용할 수 있는 LocalDB 버전의 이름을 포함 합니다.  
  
 *lpdwNumberOfVersions*  
 [입력/출력] 입력 시 *pVersionNames* 버퍼의 버전에 대한 슬롯 수를 저장합니다.   
출력 시 기존 LocalDB 버전의 수를 저장합니다.  
  
## <a name="returns"></a>반환  
 S_OK  
 함수가 성공했습니다.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB가 컴퓨터에 설치되어 있지 않습니다.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 지정한 입력 매개 변수 중 한 개 이상이 잘못되었습니다.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 입력 버퍼가 너무 짧은데 잘림이 요청되지 않았습니다.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 예기치 않은 오류가 발생했습니다. 자세한 내용은 이벤트 로그를 참조하십시오.  
  
## <a name="remarks"></a>설명  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Express LocalDB 헤더 및 버전 정보](sql-server-express-localdb-header-and-version-information.md)  
  
  
