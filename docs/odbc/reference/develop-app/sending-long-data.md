---
title: 긴 데이터 전송 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aeeeb716aa2f9a72338f3aeb586dffce86f84069
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304184"
---
# <a name="sending-long-data"></a>Long 데이터 전송
DBMS는 *긴 데이터를* 254문자와 같은 특정 크기이상의 문자 또는 이진 데이터로 정의합니다. 항목이 긴 텍스트 문서 또는 비트맵을 나타내는 경우와 같이 긴 데이터의 전체 항목을 메모리에 저장하지 못할 수 있습니다. 이러한 데이터는 단일 버퍼에 저장할 수 없으므로 데이터 원본은 명령문이 실행될 때 **SQLPutData를** 사용하여 부분적으로 드라이버로 전송합니다. 실행 시 데이터가 전송되는 매개 변수를 *실행 시 데이터 매개 변수라고 합니다.*  
  
> [!NOTE]  
>  응용 프로그램은 **실제로 SQLPutData를**사용하여 실행 시 모든 유형의 데이터를 보낼 수 있지만 문자 및 이진 데이터만 부분적으로 보낼 수 있습니다. 그러나 데이터가 단일 버퍼에 들어갈 만큼 작으면 일반적으로 **SQLPutData**를 사용할 이유가 없습니다. 버퍼를 바인딩하고 드라이버가 버퍼에서 데이터를 검색하도록 하는 것이 훨씬 쉽습니다.  
  
 실행 시 데이터를 전송하기 위해 응용 프로그램은 다음 작업을 수행합니다.  
  
1.  버퍼의 주소를 전달하는 대신 **SQLBindParameter의** *ParameterValuePtr* 인수에서 매개 변수를 식별하는 32비트 값을 전달합니다. 이 값은 드라이버에서 분석하지 않습니다. 나중에 응용 프로그램에 반환되므로 응용 프로그램에 무언가를 의미해야합니다. 예를 들어 매개 변수의 수 또는 데이터를 포함하는 파일의 핸들일 수 있습니다.  
  
2.  **SQLBindParameter**의 *StrLen_or_IndPtr* 인수에서 길이/표시기 버퍼의 주소를 전달합니다.  
  
3.  SQL_DATA_AT_EXEC 또는*SQL_LEN_DATA_AT_EXEC(길이)* 매크로의 결과를 길이/표시기 버퍼에 저장합니다. 이 두 값은 드라이버에게 매개 변수에 대한 데이터가 **SQLPutData**로 전송된다는 것을 나타냅니다. *SQL_LEN_DATA_AT_EXEC(길이)는*긴 데이터를 데이터 원본으로 보낼 때 사용되며, 이 데이터는 공간을 할당할 수 있도록 전송되는 긴 데이터의 바이트 수를 알아야 합니다. 데이터 원본에 이 값이 필요한지 확인하려면 응용 프로그램에서 SQL_NEED_LONG_DATA_LEN 옵션을 사용하여 **SQLGetInfo를** 호출합니다. 모든 드라이버는 이 매크로를 지원해야 합니다. 데이터 원본에 바이트 길이가 필요하지 않은 경우 드라이버는 이를 무시할 수 있습니다.  
  
4.  **SQLExecute** 또는 **SQLExecDirect를**호출합니다. 드라이버는 길이/표시기 버퍼에 SQL_DATA_AT_EXEC 값 또는*SQL_LEN_DATA_AT_EXEC(길이)* 매크로의 결과가 포함되어 있음을 발견하고 SQL_NEED_DATA 함수의 반환 값으로 반환합니다.  
  
5.  SQL_NEED_DATA 반환 값에 대한 응답으로 **SQLParamData를** 호출합니다. 긴 데이터를 전송해야 하는 경우 **SQLParamData는** SQL_NEED_DATA 반환합니다. *ValuePtrPtr* 인수가 가리키는 버퍼에서 드라이버는 실행 시 데이터 매개 변수를 식별하는 값을 반환합니다. 실행 시 데이터 매개 변수가 두 개 이상 있는 경우 응용 프로그램은 이 값을 사용하여 데이터를 보낼 매개 변수를 결정해야 합니다. 드라이버는 특정 순서로 실행 시 데이터 매개 변수에 대한 데이터를 요청할 필요가 없습니다.  
  
6.  **SQLPutData를** 호출하여 매개 변수 데이터를 드라이버로 보냅니다. 매개 변수 데이터가 단일 버퍼에 맞지 않는 경우( 긴 데이터의 경우처럼 응용 프로그램은 **SQLPutData를** 반복적으로 호출하여 부분적으로 데이터를 전송합니다.) 데이터를 다시 어셈블하는 것은 드라이버와 데이터 원본에 달려 있습니다. 응용 프로그램이 null 종료 문자열 데이터를 전달하는 경우 드라이버 또는 데이터 원본은 재구성 프로세스의 일부로 null 종료 문자를 제거해야 합니다.  
  
7.  매개 변수에 대 한 모든 데이터를 보낸 다는 것을 나타내기 위해 **SQLParamData를** 다시 호출 합니다. 데이터가 전송되지 않은 데이터 실행 매개 변수가 있는 경우 드라이버는 SQL_NEED_DATA 다음 매개 변수를 식별하는 값을 반환합니다. 응용 프로그램이 6단계로 돌아갑니다. 실행 시 모든 데이터 매개 변수에 대한 데이터가 전송된 경우 명령문이 실행됩니다. **SQLParamData** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환 하 고 모든 반환 값 또는 **SQLExecDirect** 반환할 수 있는 진단을 반환할 수 있습니다. **SQLExecute**  
  
 **SQLExecute** 또는 **SQLExecDirect가** SQL_NEED_DATA 반환하고 마지막 실행 시 데이터 매개 변수에 대한 데이터가 완전히 전송되기 전에 명령문은 데이터 필요 상태에 있습니다. 명령문이 필요한 데이터 상태에 있는 동안 응용 프로그램은 **SQLPutData,** **SQLParamData,** **SQLCancel,** **SQLGetDiagField**또는 **SQLGetDiagRec만**호출할 수 있습니다. 다른 모든 함수는 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. **SQLCancel호출하면** 명령문의 실행이 취소되고 이전 상태로 반환됩니다. 자세한 내용은 [부록 B: ODBC 상태 전환 테이블을](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)참조하십시오.  
  
 실행 시 데이터를 보내는 예제는 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) 함수 설명을 참조하십시오.
