---
title: Long 데이터를 보내는 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a15a3fdd69a1578392d34adac08b297269df7cf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913968"
---
# <a name="sending-long-data"></a>Long 데이터를 전송합니다.
Dbms 정의 *긴 데이터* 모든 문자 데이터 또는 254 자 같은 특정 크기에 대 한 이진 데이터입니다. 긴 텍스트 문서 또는 비트맵 항목이 나타내는 하는 경우와 같은 메모리에 긴 데이터의 전체 항목을 저장 하려면 하지 못할 수도 있습니다. 이러한 데이터는 단일 버퍼에 저장할 수 없습니다, 때문에 데이터 원본에 전송으로 파트를 지정 된 드라이버 **SQLPutData** 문이 실행 되는 경우. 매개 변수를 실행 시 데이터 보내집니다 라고 *실행 시 데이터 매개 변수*합니다.  
  
> [!NOTE]  
>  응용 프로그램 수와 실행 시간에 모든 종류의 데이터를 보낼 실제로 **SQLPutData**문자 및 이진 데이터 부분에 보낼 수 있지만, 합니다. 그러나 데이터를 단일 버퍼로 수 있을 정도로 작고 경우 없기 일반적으로 사용할 이유가 없습니다 **SQLPutData**합니다. 훨씬 버퍼를 바인딩하고 버퍼에서 데이터를 검색 하는 드라이버를 사용 하는 것이 쉽습니다.  
  
 실행 시 데이터를 보내도록 응용 프로그램에서는 다음 작업을 수행 합니다.  
  
1.  매개 변수를 식별 하는 32 비트 값을 전달는 *ParameterValuePtr* 인수 **SQLBindParameter** 버퍼의 주소를 전달 하는 대신 합니다. 이 값은 드라이버에 의해 분석 되지 않습니다. 응용 프로그램에 것을 의미 해야 하므로 응용 프로그램을 나중에 반환 됩니다. 예를 들어, 매개 변수 번호 또는 데이터를 포함 하는 파일 핸들 수 있습니다.  
  
2.  전달에 길이/표시기 버퍼의 주소는 *StrLen_or_IndPtr* 의 인수 **SQLBindParameter**합니다.  
  
3.  SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 결과 저장 (*길이*) 길이/표시기 버퍼에는 매크로입니다. 이 두 값을 매개 변수 데이터가 전송 되는 드라이버에 알립니다 **SQLPutData**합니다. SQL_LEN_DATA_AT_EXEC (*길이*) 긴 데이터의 바이트 수 받게 될 공간을 미리 할당할 수 있도록 알아야 하는 데이터 원본에 대 한 long 데이터를 보낼 때 사용 됩니다. 데이터 원본에서이 값을 필요한 경우 응용 프로그램 호출을 확인 하려면 **SQLGetInfo** SQL_NEED_LONG_DATA_LEN 옵션을 사용 합니다. 모든 드라이버;이 매크로 지원 해야 합니다. 데이터 원본 바이트 길이 필요 하지 않으면 드라이버 무시 해도 됩니다.  
  
4.  호출 **SQLExecute** 또는 **SQLExecDirect**합니다. 드라이버 길이/표시기 버퍼 SQL_DATA_AT_EXEC 값 이나는 SQL_LEN_DATA_AT_EXEC의 결과 포함 하는 검색 (*길이*) 매크로 및 함수의 반환 값으로는 SQL_NEED_DATA 반환 합니다.  
  
5.  호출 **SQLParamData** 는 SQL_NEED_DATA에 대 한 응답에서 값을 반환 합니다. Long 데이터를 전송 해야 할 경우 **SQLParamData** SQL_NEED_DATA를 반환 합니다. 가 가리키는 버퍼에는 *ValuePtrPtr* 인수, 드라이버는 실행 시 데이터 매개 변수를 식별 하는 값을 반환 합니다. 둘 이상의 실행 시 데이터 매개 변수 이면 응용 프로그램;에 대 한 데이터를 보내는 되는 매개 변수를 확인 하려면이 값을 사용 해야 합니다. 드라이버가 특정 순서로 실행 시 데이터 매개 변수에 대 한 데이터를 요청 하는 필요 하지 않습니다.  
  
6.  호출 **SQLPutData** 드라이버에 매개 변수 데이터를 보냅니다. 응용 프로그램이 호출할 수 있으므로 긴 데이터의 경우 매개 변수 데이터를 단일 버퍼에 맞지 않으면, **SQLPutData** 반복 해 서 부분;의 데이터를 전송 하는 데이터를 다시 드라이버와 데이터 소스는 합니다. Null로 끝나는 문자열 데이터를 전달 하는 응용 프로그램, 드라이버 또는 데이터 원본 리어셈블리 프로세스의 일부로 null 종결 문자를 제거 해야 합니다.  
  
7.  호출 **SQLParamData** 다시 나타내려면 데이터 매개 변수를 모두 전송 않은 것입니다. 드라이버를에 전송 되지 않은 데이터는 실행 시 데이터 매개 변수가 있는 경우 SQL_NEED_DATA 및; 다음 매개 변수를 식별 하는 값 반환 응용 프로그램 6 단계를 반환합니다. 모든 실행 시 데이터 매개 변수에 대 한 데이터를 전송한 문이 실행 됩니다. **SQLParamData** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 및 수를 반환 하면 모든 반환 값 또는 진단 하는 **SQLExecute** 또는 **SQLExecDirect** 반환할 수 있습니다.  
  
 후 **SQLExecute** 또는 **SQLExecDirect** sql_need_data가 반환 되며 데이터가 마지막 실행 시 데이터 매개 변수에 대 한 완전히 플러시된 전에 문이에서 필요한 데이터 상태입니다. 응용 프로그램만 호출할 수는 문이 필요한 데이터 상태에서 이지만, **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, 또는 **SQLGetDiagRec**; 다른 모든 함수가 반환 SQLSTATE HY010 (함수 시퀀스 오류). 호출 **SQLCancel** 문 실행을 취소 하 고 이전 상태로 돌아갑니다. 자세한 내용은 참조 [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
 실행 시 데이터를 보내는 예 참조는 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) 함수 설명 합니다.
