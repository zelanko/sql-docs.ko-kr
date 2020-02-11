---
title: SQLDataSourceToDriver 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba5019b15fdbb8bce06f04d5109813b88c40647d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104846"
---
# <a name="sqldatasourcetodriver-function"></a>SQLDataSourceToDriver 함수
**SQLDataSourceToDriver** SUPPORTSTRANSLATIONS for ODBC drivers. 이 함수는 ODBC 사용 응용 프로그램에서 호출 되지 않습니다. 응용 프로그램은 **SQLSetConnectAttr**를 통해 변환을 요청 합니다. **SQLSetConnectAttr** 에 지정 된 *ConnectionHandle* 와 연결 된 드라이버는 지정 된 DLL을 호출 하 여 데이터 원본에서 드라이버로 흐르는 모든 데이터의 번역을 수행 합니다. 기본 변환 DLL은 ODBC 초기화 파일에 지정할 수 있습니다.  
  
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
 *fOption*  
 입력 옵션 값입니다.  
  
 *fSqlType*  
 입력 SQL 데이터 형식입니다. 이 인수는 *rgbValueIn* 를 응용 프로그램에서 사용할 수 있는 형식으로 변환 하는 방법을 드라이버에 알립니다. 유효한 SQL 데이터 형식 목록은 부록 D: 데이터 형식에서 [Sql 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 섹션을 참조 하세요.  
  
 *rgbValueIn*  
 입력 변환할 값입니다.  
  
 *cbValueIn*  
 입력 *RgbValueIn*의 길이입니다.  
  
 *rgbValueOut*  
 출력 변환의 결과입니다.  
  
> [!NOTE]  
>  변환 DLL이이 값을 null로 종료 하지 않습니다.  
  
 *cbValueOutMax*  
 입력 *RgbValueOut*의 길이입니다.  
  
 *pcbValueOut*  
 출력 *RgbValueOut*에서 반환할 수 있는 총 바이트 수 (null 종결 바이트 제외)입니다.  
  
 문자 또는 이진 데이터의 경우,이가 *cbvalueoutmax*보다 크거나 같으면 *RgbValueOut* 의 데이터가 *cbvalueoutmax* 바이트로 잘립니다.  
  
 다른 모든 데이터 형식의 경우, *Cbvalueoutmax* 값은 무시 되 고 변환 DLL은 *RgbValueOut* 의 크기가 *fSqlType*로 지정 된 SQL 데이터 형식의 기본 C 데이터 형식 크기인 것으로 가정 합니다.  
  
 *Pcbvalueout* 인수는 null 포인터 일 수 있습니다.  
  
 *szErrorMsg*  
 출력 오류 메시지의 저장소에 대 한 포인터입니다. 변환이 실패 하지 않는 한 빈 문자열입니다.  
  
 *cbErrorMsgMax*  
 입력 *Szerrormsg*의 길이입니다.  
  
 *pcbErrorMsg*  
 출력 *Szerrormsg*에서 반환 하는 데 사용할 수 있는 총 바이트 수 (null 종결 바이트 제외)에 대 한 포인터입니다. 이가 *cberrormsg*보다 크거나 같으면 *szerrormsg* 의 데이터가 *cberrormsgmax* 에서 null 종료 문자를 뺀 값으로 잘립니다. *Pcberrormsg* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환  
 변환이 성공 했으면 TRUE이 고, 변환에 실패 하면 FALSE입니다.  
  
## <a name="comments"></a>주석  
 이 드라이버는 **SQLDataSourceToDriver** 를 호출 하 여 데이터 원본에서 드라이버로 전달 하는 alldata (결과 집합 데이터, 테이블 이름, 행 개수, 오류 메시지 등)를 변환 합니다. 변환 DLL은 데이터의 형식 및 변환 DLL의 용도에 따라 일부 데이터를 변환 하지 않을 수 있습니다. 예를 들어 한 코드 페이지에서 다른 코드로 문자 데이터를 변환 하는 DLL은 모든 숫자 데이터와 이진 데이터를 무시 합니다.  
  
 *Foption* 값은 SQL_ATTR_TRANSLATE_OPTION 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하 여 지정 된 *vparam* 의 값으로 설정 됩니다. 지정 된 변환 DLL의 특정 의미를 갖는 32 비트 값입니다. 예를 들어 특정 문자 집합 변환을 지정할 수 있습니다.  
  
 *RgbValueIn* 및 *rgbValueOut*에 대해 동일한 버퍼가 지정 된 경우 버퍼의 데이터 변환이 수행 됩니다.  
  
 *Cbvaluein*, *cbvalueoutmax*및 *PCBVALUEOUT* 은 sdword 유형 이지만 **SQLDataSourceToDriver** 는 큰 포인터를 지원 하지 않을 수 있습니다.  
  
 **SQLDataSourceToDriver** 가 FALSE를 반환 하는 경우 변환 중에 데이터가 잘릴 수 있습니다. *Pcbvalueout* (출력 버퍼에서 반환할 수 있는 바이트 수)가 *Cbvalueoutmax* (출력 버퍼의 길이) 보다 큰 경우 잘림이 발생 합니다. 드라이버는 잘림이 허용 되는지 여부를 확인 해야 합니다. 잘림이 발생 하지 않은 경우 다른 오류로 인해 **SQLDataSourceToDriver** 에서 FALSE를 반환 했습니다. 두 경우 모두 *Szerrormsg*에 특정 오류 메시지가 반환 됩니다.  
  
 데이터 변환에 대 한 자세한 내용은 [변환 dll](../../../odbc/reference/develop-app/translation-dlls.md)을 참조 하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|데이터 원본으로 전송 되는 데이터 변환|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|연결 특성의 설정 반환|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
