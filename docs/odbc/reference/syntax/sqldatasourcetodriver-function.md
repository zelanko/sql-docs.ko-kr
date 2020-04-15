---
title: SQLDataSourceToDriver 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSourceToDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSourceToDriver
helpviewer_keywords:
- SQLDataSourceToDriver function [ODBC]
ms.assetid: 0d87fcac-30a0-4303-ad8f-a5b53f4b428d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92df58b76a9a11d0d4ab9821756bff014ecae29a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301193"
---
# <a name="sqldatasourcetodriver-function"></a>SQLDataSourceToDriver 함수
**SQLDataSourceToDriver는** ODBC 드라이버에 대한 번역을 지원합니다. 이 함수는 ODBC 지원 응용 프로그램에서 호출되지 않습니다. 응용 프로그램은 **SQLSetConnectAttr을**통해 번역을 요청합니다. **SQLSetConnectAttr에** 지정된 *연결 핸들과* 연결된 드라이버는 지정된 DLL을 호출하여 데이터 원본에서 드라이버로 흐르는 모든 데이터의 변환을 수행합니다. ODBC 초기화 파일에 기본 변환 DLL을 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
BOOL SQLDataSourceToDriver(  
     UDWORD     fOption,  
     SWORD      fSqlType,  
     PTR        rgbValueIn,  
     SDWORD     cbValueIn,  
     PTR        rgbValueOut,  
     SDWORD     cbValueOutMax,  
     SDWORD *   pcbValueOut,  
     UCHAR *    szErrorMsg,  
     SWORD      cbErrorMsgMax,  
     SWORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>인수  
 *f옵션*  
 [입력] 옵션 값입니다.  
  
 *fSqlType*  
 [입력] SQL 데이터 형식입니다. 이 인수는 드라이버에게 *rgbValueIn을* 응용 프로그램에서 허용되는 형식으로 변환하는 방법을 알려줍니다. 유효한 SQL 데이터 형식 목록은 부록 D: 데이터 [형식의 SQL 데이터 유형](../../../odbc/reference/appendixes/sql-data-types.md) 섹션을 참조하십시오.  
  
 *rgbValueIn*  
 [입력] 번역할 값입니다.  
  
 *cbValueIn*  
 [입력] *rgbValueIn의*길이 .  
  
 *rgbValueOut*  
 [출력] 번역의 결과입니다.  
  
> [!NOTE]  
>  번역 DLL은 이 값을 null-종료하지 않습니다.  
  
 *cb밸류아웃맥스*  
 [입력] *rgbValueOut의*길이 .  
  
 *pcb밸류아웃*  
 [출력] *rgbValueOut에서*반환할 수 있는 총 바이트 수(null-termination 바이트 제외)입니다.  
  
 문자 또는 이진 데이터의 경우 *cbValueOutMax보다*크거나 같으면 *rgbValueOut의* 데이터가 *cbValueOutMax* 바이트로 잘립니다.  
  
 다른 모든 데이터 형식의 경우 *cbValueOutMax* 의 값이 무시되고 번역 DLL은 *rgbValueOut의* 크기가 *fSqlType으로*지정된 SQL 데이터 형식의 기본 C 데이터 형식의 크기라고 가정합니다.  
  
 *pcbValueOut* 인수는 null 포인터일 수 있습니다.  
  
 *szErrorMsg*  
 [출력] 오류 메시지에 대한 저장소에 대한 포인터입니다. 번역에 실패하지 않는 한 빈 문자열입니다.  
  
 *cbErrorMsgMax*  
 [입력] *szErrorMsg의*길이 .  
  
 *pcbErrorMsg*  
 [출력] *szErrorMsg에서*반환할 수 있는 총 바이트 수(null-termination 바이트 제외)에 대한 포인터입니다. *cbErrorMsg보다*크거나 같으면 *szErrorMsg의* 데이터는 null 종료 문자를 뺀 *cbErrorMsgMax로* 잘립니다. *pcbErrorMsg* 인수는 null 포인터일 수 있습니다.  
  
## <a name="returns"></a>반환  
 TRUE 번역에 성공한 경우 TRUE, 번역에 실패한 경우 FALSE입니다.  
  
## <a name="comments"></a>주석  
 드라이버는 **SQLDataSourceToDriver를** 호출하여 데이터 원본에서 드라이버로 전달하는 alldata(결과 집합 데이터, 테이블 이름, 행 수, 오류 메시지 등)를 변환합니다. 번역 DLL은 데이터의 유형과 번역 DLL의 목적에 따라 일부 데이터를 번역하지 않을 수 있습니다. 예를 들어 한 코드 페이지에서 다른 코드 페이지로 문자 데이터를 변환하는 DLL은 모든 숫자 및 이진 데이터를 무시합니다.  
  
 *fOption의* 값은 **sqlSetConnectAttr을** SQL_ATTR_TRANSLATE_OPTION 특성으로 호출하여 지정된 *vParam* 값으로 설정됩니다. 지정된 번역 DLL에 대한 특정 의미가 있는 32비트 값입니다. 예를 들어 특정 문자 집합 변환을 지정할 수 있습니다.  
  
 *rgbValueIn* 및 *rgbValueOut에*대해 동일한 버퍼가 지정되면 버퍼의 데이터 변환이 수행됩니다.  
  
 *cbValueIn,* *cbValueOutMax*및 *pcbValueOut은* SDWORD 형식이지만 **SQLDataSourceToDriver가** 반드시 거대한 포인터를 지원하지는 않습니다.  
  
 **SQLDataSourceToDriver가** FALSE를 반환하는 경우 번역 중에 데이터 잘림이 발생했을 수 있습니다. *pcbValueOut(출력* 버퍼에서 반환할 수 있는 바이트 수)가 *cbValueOutMax(출력* 버퍼의 길이)보다 큰 경우 잘림이 발생했습니다. 드라이버는 잘림이 허용되는지 여부를 결정해야 합니다. 잘림이 발생하지 않으면 **SQLDataSourceToDriver가** 다른 오류로 인해 FALSE를 반환했습니다. 두 경우 모두 특정 오류 메시지가 *szErrorMsg*로 반환됩니다.  
  
 데이터 변환에 대한 자세한 내용은 [번역 DLL을](../../../odbc/reference/develop-app/translation-dlls.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|데이터 원본으로 전송되는 데이터 변환|[SQLDriverToData소스](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|연결 특성의 설정 반환|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
