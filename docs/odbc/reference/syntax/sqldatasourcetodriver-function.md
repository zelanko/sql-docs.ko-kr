---
title: "SQLDataSourceToDriver 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6b6b37e632f4e610ec19cf355e94999135d72781
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqldatasourcetodriver-function"></a>SQLDataSourceToDriver 함수
**SQLDataSourceToDriver** supportstranslations ODBC 드라이버에 대 한 합니다. 이 함수는 ODBC 사용 응용 프로그램; 의해 호출 되지 않습니다. 응용 프로그램 요청 통해 번역 **SQLSetConnectAttr**합니다. 관련 된 드라이버의 *ConnectionHandle* 에 지정 된 **SQLSetConnectAttr** 드라이버에 데이터 원본의 모든 데이터의 번역을 수행 하려면 지정된 된 DLL을 호출 합니다. ODBC 초기화 파일의 기본 변환 DLL을 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 옵션 값입니다.  
  
 *fSqlType*  
 [입력] SQL 데이터 형식입니다. 이 인수는 드라이버를 변환 하는 방법을 알립니다 *rgbValueIn* 응용 프로그램에 의해 허용 되는 양식으로 합니다. 목록이 올바른 SQL 데이터 형식에 대 한 참조는 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식에는 섹션입니다.  
  
 *rgbValueIn*  
 [입력] 변환할 값입니다.  
  
 *cbValueIn*  
 [입력] 길이 *rgbValueIn*합니다.  
  
 *rgbValueOut*  
 [출력] 변환의 결과입니다.  
  
> [!NOTE]  
>  변환 DLL 종료 하지 않습니다 null-이 값.  
  
 *cbValueOutMax*  
 [입력] 길이 *rgbValueOut*합니다.  
  
 *pcbValueOut*  
 [출력] 바이트 (null 종료 바이트 제외)의 총 수를 반환 하려면 사용 가능한 *rgbValueOut*합니다.  
  
 문자 또는 이진 데이터를 보다 크거나 같은 경우 이것이 *cbValueOutMax*, 데이터에 *rgbValueOut* 잘립니다 *cbValueOutMax* 바이트입니다.  
  
 다른 모든 데이터 형식, 값에 대 한 *cbValueOutMax* 는 무시 됩니다 변환 DLL 있다고 가정 하 고 크기 *rgbValueOut* 로지정된SQL데이터형식의기본C데이터형식크기*fSqlType*합니다.  
  
 *pcbValueOut* 인수는 null 포인터 일 수 있습니다.  
  
 *szErrorMsg*  
 [출력] 오류 메시지에 대 한 저장소에 대 한 포인터입니다. 변환 실패 하지 않으면 빈 문자열입니다.  
  
 *cbErrorMsgMax*  
 [입력] 길이 *szErrorMsg*합니다.  
  
 *pcbErrorMsg*  
 [출력] 바이트 (null 종료 바이트 제외)의 총 수에 대 한 포인터를 반환 하려면 사용 가능한 *szErrorMsg*합니다. 보다 크거나 같은 경우 이것이 *cbErrorMsg*, 데이터에 *szErrorMsg* 잘립니다 *cbErrorMsgMax* null 종결 문자가 뺀 값입니다. *pcbErrorMsg* 인수는 null 포인터 일 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 변환이 성공 했으면 FALSE 변환에 실패 한 경우 TRUE입니다.  
  
## <a name="comments"></a>설명  
 드라이버 호출 **SQLDataSourceToDriver** 드라이버에 원본 데이터에서 전달 alldata (결과 집합 데이터, 테이블 이름, 행 개수, 오류 메시지 및 등)을 변환 합니다. 변환 DLL 데이터의 유형 및 번역; DLL의 용도 따라 일부 데이터를 번역 되지 않을 수 없습니다. 예를 들어 다른 코드 페이지에서 문자 데이터를 변환 하는 DLL 모든 숫자 및 이진 데이터를 무시 합니다.  
  
 값 *fOption* 의 값으로 설정 되어 *vParam* 호출 하 여 지정 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 특성을 사용 합니다. 지정 된 변환 DLL에 대 한 특정 의미 있는 32 비트 값입니다. 예를 들어, 특정 문자 집합 변환 지정할 수 없습니다.  
  
 동일한 버퍼에 대해 지정 된 경우 *rgbValueIn* 및 *rgbValueOut*, 버퍼에 데이터의 위치에서 수행 됩니다.  
  
 하지만 *cbValueIn*, *cbValueOutMax*, 및 *pcbValueOut* SDWORD, 형식의 **SQLDataSourceToDriver** 반드시 않습니다 거 대 한 포인터를 지원 합니다.  
  
 경우 **SQLDataSourceToDriver** 데이터 잘림 변환 하는 동안 발생 했을 수 FALSE를 반환 합니다. 경우 *pcbValueOut* (출력 버퍼에서 반환할 수 있는 바이트 수) 보다 크면 *cbValueOutMax* (출력 버퍼의 길이)에 잘림이 발생 합니다. 드라이버는 잘림을 허용 했는지 여부를 결정 해야 합니다. 잘림이 발생 하지 않은 경우는 **SQLDataSourceToDriver** 다른 오류로 인해 FALSE를 반환 합니다. 두 경우 모두 특정 오류 메시지에 반환 됩니다 *szErrorMsg*합니다.  
  
 에 데이터를 변환 하는 방법에 대 한 자세한 내용은 참조 [번역 Dll](../../../odbc/reference/develop-app/translation-dlls.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|데이터 원본에 전송 되는 데이터를 변환 합니다.|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|연결 특성의 설정은 반환|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
