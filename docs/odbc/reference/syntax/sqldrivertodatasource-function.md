---
title: SQLDriverToDataSource 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverToDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverToDataSource
helpviewer_keywords:
- SQLDriverToDataSource function [ODBC]
ms.assetid: 0de28eb5-8aa9-43e4-a87f-7dbcafe800dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f5450bbabb43b1f5cbc8c0fd7cb1a83da3a8bc7
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53203692"
---
# <a name="sqldrivertodatasource-function"></a>SQLDriverToDataSource 함수
**SQLDriverToDataSource** ODBC 드라이버에 대 한 번역을 지원 합니다. 이 함수는 ODBC 사용 응용 프로그램에서 호출 되지 않습니다. 응용 프로그램 요청을 통해 번역 **SQLSetConnectAttr**합니다. 연결 된 드라이버는 *ConnectionHandle* 에 지정 된 **SQLSetConnectAttr** 드라이버에서 데이터 원본에 전달 하는 모든 데이터 변환을 수행 하려면 지정 된 DLL을 호출 합니다. ODBC 초기화 파일의 기본 번역 DLL을 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL SQLDriverToDataSource(  
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
 [입력] ODBC SQL 데이터 형식입니다. 이 인수 드라이버를 변환 하는 방법을 지시 *rgbValueIn* 데이터 소스에서 허용 되는 형태로 합니다. 올바른 SQL 데이터 형식의 목록을 참조 하세요 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md)합니다.  
  
 *rgbValueIn*  
 [입력] 변환할 값입니다.  
  
 *cbValueIn*  
 [입력] 길이가 *rgbValueIn*합니다.  
  
 *rgbValueOut*  
 [출력] 변환의 결과입니다.  
  
> [!NOTE]  
>  변환 DLL 종료 하지 않습니다 null-이 값.  
  
 *cbValueOutMax*  
 [입력] 길이가 *rgbValueOut*합니다.  
  
 *pcbValueOut*  
 [출력] 총 바이트 (null 종료 바이트 제외)에서 반환할 사용 가능한 *rgbValueOut*합니다.  
  
 문자 또는 이진 데이터를 보다 크거나 같은 경우에 대 한 *cbValueOutMax*, 데이터가 *rgbValueOut* 잘립니다 *cbValueOutMax* 바이트입니다.  
  
 다른 모든 데이터 형식의 경우 값에 대 한 *cbValueOutMax* 무시 됩니다 가정 변환 DLL 및 크기인 *rgbValueOut* 를사용하여지정된SQL데이터형식의기본C데이터형식의크기*fSqlType*합니다.  
  
 합니다 *pcbValueOut* 인수로 null 포인터를 사용할 수 있습니다.  
  
 *szErrorMsg*  
 [출력] 오류 메시지에 대 한 저장소에 대 한 포인터입니다. 이것이 변환 실패 하지 않으면 빈 문자열입니다.  
  
 *cbErrorMsgMax*  
 [입력] 길이가 *szErrorMsg*합니다.  
  
 *pcbErrorMsg*  
 [출력] 총 바이트 (null 종료 바이트 제외)에 대 한 포인터를 반환 하려면 사용 가능한 *szErrorMsg*합니다. 보다 크거나 같은 경우 *cbErrorMsg*에 있는 데이터 *szErrorMsg* 잘립니다 *cbErrorMsgMax* null 종결 문자가 뺀 값입니다. 합니다 *pcbErrorMsg* 인수로 null 포인터를 사용할 수 있습니다.  
  
## <a name="returns"></a>반환 값  
 변환 성공 했으면 FALSE 변환에 실패 한 경우 TRUE입니다.  
  
## <a name="comments"></a>주석  
 드라이버 **SQLDriverToDataSource** (SQL 문, 매개 변수 및 등)의 모든 데이터를 변환 하는 드라이버에서 데이터 원본에 전달 합니다. 변환 DLL 데이터의 형식 및 변환 DLL의 용도 따라 일부 데이터를를 변환 하지 않을 수 있습니다. 예를 들어, 다른 코드 페이지의 문자 데이터를 변환 하는 DLL에는 모든 숫자 및 이진 데이터는 무시 합니다.  
  
 값 *fOption* 의 값으로 설정 됩니다 *갖고* 호출 하 여 지정 된 **SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 특성을 사용 합니다. 지정 된 번역이 DLL에 대 한 특별 한 의미가 있는 32 비트 값입니다. 예를 들어, 특정 문자 집합 번역 지정 합니다.  
  
 동일한 버퍼에 지정 되어 있으면 *rgbValueIn* 하 고 *rgbValueOut*, 버퍼의 데이터 변환 되어에서 수행 됩니다.  
  
 하지만 *cbValueIn*를 *cbValueOutMax*, 및 *pcbValueOut* SDWORD, 형식의 **SQLDriverToDataSource** 반드시 거 대 한 포인터를 지원 합니다.  
  
 하는 경우 **SQLDriverToDataSource** 데이터 잘림 변환 하는 동안 발생 했을 수 FALSE를 반환 합니다. 경우 *pcbValueOut* (출력 버퍼에서 반환할 사용 가능한 바이트의 수) 보다 크면 *cbValueOutMax* (출력 버퍼의 길이), 잘림이 발생 합니다. 드라이버는 잘림을 허용 된 있는지 여부를 결정 해야 합니다. 잘림이 발생 하지 않은 경우는 **SQLDriverToDataSource** 다른 오류로 인해 FALSE를 반환 합니다. 두 경우 모두 특정 오류 메시지에 반환 됩니다 *szErrorMsg*합니다.  
  
 데이터를 변환 하는 방법에 대 한 자세한 내용은 참조 하세요. [변환 Dll](../../../odbc/reference/develop-app/translation-dlls.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|데이터 소스에서 반환 된 데이터를 변환 합니다.|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|연결 특성의 설정을 반환합니다.|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
