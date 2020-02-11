---
title: 수준 1 API 함수 (Oracle 용 ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cb1771f88987073b1ef0bcc106f8de28549affe6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085469"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>수준 1 API 함수(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 이 수준의 함수는 핵심 인터페이스 규칙 및 트랜잭션 지원과 같은 추가 기능을 제공 합니다.  
  
|API 함수|메모|  
|------------------|-----------|  
|**SQLColumns**|지정 된 테이블의 열 목록에 해당 하는 테이블의 결과 집합을 만듭니다. 공용 동의어에 대 한 열을 요청 하는 경우 SYNONYMCOLUMNS 연결 특성을 설정 하 고 빈 문자열을 *Sztableowner* 인수로 지정 해야 합니다. 공용 동의어에 대 한 열을 반환 하는 경우 드라이버는 테이블 이름 열을 빈 문자열로 설정 합니다. 결과 집합에는 각 행의 끝에 추가 열 서 수 위치가 포함 됩니다. 이 값은 테이블에서 열의 서 수 위치입니다.|  
|**SQLDriverConnect**|기존 데이터 원본에 연결 합니다. 자세한 내용은 [연결 문자열 형식 및 특성](../../odbc/microsoft/connection-string-format-and-attributes.md)을 참조 하세요.|  
|**SQLGetConnectOption**|연결 옵션의 현재 설정을 반환 합니다. 이 함수는 부분적으로 지원 됩니다. 드라이버는 *foption* 인수에 대 한 모든 값을 지원 하지만 [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md) *foption* 인수에 대 한 일부 *vparam* 값은 지원 하지 않습니다. 자세한 내용은 [Connect Options](../../odbc/microsoft/connect-options.md)를 참조 하세요.|  
|**SQLGetData**|지정 된 결과 집합의 현재 레코드에서 단일 필드의 값을 검색 합니다.|  
|**SQLGetFunctions**|지원 되는 모든 함수에 대해 TRUE를 반환 합니다. 드라이버 관리자에 의해 구현 됩니다.|  
|**SQLGetInfo**|Oracle 용 ODBC 드라이버 및 연결 핸들과 연결 된 데이터 원본에 대 한 SQLHDBC, SQLUSMALLINT \*, SQLPOINTER, SQLPOINTER 및 sqlpointer를 비롯 한 *정보를 반환 합니다.*|  
|**SQLGetStmtOption**|문 옵션의 현재 설정을 반환 합니다. 자세한 내용은 [문 옵션](../../odbc/microsoft/statement-options.md)을 참조 하세요.|  
|**SQLGetTypeInfo**|데이터 원본에서 지 원하는 데이터 형식에 대 한 정보를 반환 합니다. 드라이버는 SQL 결과 집합의 정보를 반환 합니다.|  
|**SQLParamData**|**Sqlputdata** 와 함께 사용 되어 문 실행 시 매개 변수 데이터를 지정 합니다.|  
|**SQLPutData**|응용 프로그램에서 문 실행 시 매개 변수 또는 열에 대 한 데이터를 드라이버에 보낼 수 있도록 합니다.|  
|**SQLSetConnectOption**|연결의 여러 측면을 제어 하는 옵션에 대 한 액세스를 제공 합니다. 이 함수는 부분적으로 지원 됩니다. 드라이버는 *foption* 인수에 대 한 모든 값을 지원 하지만 [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md) *foption* 인수에 대 한 일부 *vparam* 값은 지원 하지 않습니다. 자세한 내용은 [Connect Options](../../odbc/microsoft/connect-options.md)를 참조 하세요.|  
|**SQLSetStmtOption**|문 핸들 *hstmt*와 관련 된 옵션을 설정 합니다. 자세한 내용은 [문 옵션](../../odbc/microsoft/statement-options.md)을 참조 하세요.|  
|**SQLSpecialColumns**|테이블에서 행을 고유 하 게 식별 하는 최적의 열 집합을 검색 합니다.|  
|**SQLStatistics**|단일 테이블에 대 한 통계 목록과 테이블에 연결 된 인덱스 또는 태그 이름을 검색 합니다. 드라이버는 정보를 결과 집합으로 반환 합니다.|  
|**SQLTables**|**Sqltables** 문의 매개 변수로 지정 된 테이블 이름의 목록을 반환 합니다. 매개 변수를 지정 하지 않으면 현재 데이터 소스에 저장 된 테이블 이름을 반환 합니다. 드라이버는 정보를 결과 집합으로 반환 합니다.<br /><br /> 열거형 형식 호출은 원격 뷰 또는 로컬 매개 변수가 있는 뷰에 대 한 결과 집합 항목을 받지 않습니다. 그러나 고유 테이블 이름 지정자를 사용 하 여 **Sqltables** 를 호출 하면 해당 하는 뷰의 일치 항목 (있는 경우)을 찾을 수 있습니다. 이렇게 하면 API가 새 테이블을 만들기 전에 이름 충돌을 확인할 수 있습니다.<br /><br /> 공용 동의어가 "" TABLE_OWNER 값으로 반환 됩니다.<br /><br /> SYS 또는 SYSTEM에서 소유 하는 보기는 시스템 뷰로 식별 됩니다.|
