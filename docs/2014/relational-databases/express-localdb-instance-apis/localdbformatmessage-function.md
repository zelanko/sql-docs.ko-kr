---
title: LocalDBFormatMessage 함수 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBFormatMessage
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d287a7ceff1c38c829da91a8ae2e530f664fb4ef
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63128749"
---
# <a name="localdbformatmessage-function"></a>LocalDBFormatMessage 함수
  지정한 SQL Server Express LocalDB 오류에 대해 해당 언어의 텍스트 설명을 반환합니다.  
  
 **헤더 파일:** sqlncli.h  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT LocalDBFormatMessage(  
           HRESULT hrLocalDB,  
           DWORD dwFlags,   
           DWORD dwLanguageId,   
           LPWSTR wszMessage,   
           LPDWORD lpcchMessage   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 *hrLocalDB*  
 [입력] LocalDB 오류 코드입니다.  
  
 *dwFlags*  
 [입력] 이 함수의 동작을 지정하는 플래그입니다.  
  
 사용 가능한 플래그:  
  
 LOCALDB_TRUNCATE_ERR_MESSAGE  
 입력 버퍼가 너무 짧은 경우 오류 메시지가 버퍼에 맞게 잘립니다.  
  
 *dwLanguageId*  
 [입력] 원하는 언어(LANGID) 또는 0입니다. 이 경우 Win32 FormatMessage 언어 순서가 사용됩니다.  
  
 *wszMessage*  
 [출력] LocalDB 오류 메시지를 저장할 버퍼입니다.  
  
 *lpcchMessage*  
 [입력/출력] 입력 시 문자의 *wszMessage* 버퍼 크기를 포함합니다. 출력 시 지정된 버퍼 크기가 너무 작은 경우 후행 Null을 포함하여 문자에 필요한 버퍼 크기를 포함합니다. 함수가 성공하는 경우 후행 Null을 제외하고 메시지의 문자 수를 포함합니다.  
  
## <a name="returns"></a>반환  
 S_OK  
 함수가 성공했습니다.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB가 컴퓨터에 설치되어 있지 않습니다.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 지정한 입력 매개 변수 중 한 개 이상이 잘못되었습니다.  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 요청한 메시지가 없습니다.  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 메시지가 요청한 언어로 제공되지 않습니다.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 입력된 버퍼 *wszMessage* 가 너무 짧은데 잘림을 요청하지 않았습니다.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 예기치 않은 오류가 발생했습니다. 자세한 내용은 이벤트 로그를 참조하십시오.  
  
## <a name="remarks"></a>설명  
 LocalDB API를 사용하는 코드 샘플은 [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Express LocalDB 헤더 및 버전 정보](sql-server-express-localdb-header-and-version-information.md)  
  
  
