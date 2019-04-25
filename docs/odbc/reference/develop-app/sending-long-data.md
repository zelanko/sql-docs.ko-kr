---
title: Long 데이터 전송 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc7a140d7de8548f02fde6ab309823bbe1c9c656
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465929"
---
# <a name="sending-long-data"></a>Long 데이터 전송
Dbms 정의할 *긴 데이터* 모든 문자 또는 이진 데이터 254 자 같은 특정 크기입니다. 메모리, 긴 텍스트 문서나 비트맵 항목이 나타내는 하는 경우에 긴 데이터의 전체 항목을 저장 하지 못할 수도 있습니다. 이러한 데이터는 단일 버퍼에 저장할 수 없으므로 데이터 원본으로 보냅니다 드라이버에 사용 하 여 파트 **SQLPutData** 문이 실행 되는 경우. 실행 시 데이터는 전송 하는 매개 변수 라고 *실행 시 데이터 매개 변수*합니다.  
  
> [!NOTE]  
>  응용 프로그램 실행 시 모든 종류의 데이터를 실제로 보낼 수 있습니다 **SQLPutData**이지만 부분에서 문자 및 이진 데이터를 보낼 수 있습니다. 그러나 데이터를 단일 버퍼로 수 있을 정도로 작고 경우 일반적으로 사용 하는 이유 **SQLPutData**합니다. 버퍼를 바인딩 및 드라이버 버퍼에서 데이터를 검색할 수 있도록 하려면 훨씬 쉽습니다.  
  
 실행 시 데이터를 보내도록 응용 프로그램에는 다음 작업을 수행 합니다.  
  
1.  매개 변수를 식별 하는 32 비트 값을 전달 합니다 *ParameterValuePtr* 에서 인수 **SQLBindParameter** 버퍼의 주소를 전달 하는 대신 합니다. 이 값은 드라이버에 의해 분석 되지 않습니다. 이 응용 프로그램에 항목을 의미 해야 하므로 나중에 응용 프로그램에 반환 됩니다. 예를 들어, 매개 변수 개수 또는 데이터를 포함 하는 파일의 핸들 수 있습니다.  
  
2.  길이/표시기 버퍼의 주소를 전달 합니다 *StrLen_or_IndPtr* 인수의 **SQLBindParameter**합니다.  
  
3.  SQL_DATA_AT_EXEC를 SQL_LEN_DATA_AT_EXEC 결과 저장 (*길이*) 길이/표시기 버퍼의 매크로입니다. 데이터 매개 변수를 사용 하 여 전송 되는 드라이버를 나타내는 두이 값 모두가 **SQLPutData**합니다. SQL_LEN_DATA_AT_EXEC (*길이*) 공간 사전 할당 수 있도록 긴 데이터의 바이트 수를 보낼지 알아야 하는 데이터 원본에 긴 데이터를 보낼 때 사용 됩니다. 데이터 원본에서이 값에 필요한 경우 응용 프로그램 호출 결정할 **SQLGetInfo** SQL_NEED_LONG_DATA_LEN 옵션을 사용 하 여 합니다. 모든 드라이버에서이 매크로 지원 해야 합니다. 데이터 원본 바이트 길이가 필요 하지 않으면 드라이버 무시 해도 됩니다.  
  
4.  호출 **SQLExecute** 하거나 **SQLExecDirect**합니다. 드라이버 길이/표시기 버퍼 SQL_DATA_AT_EXEC 값인지를 SQL_LEN_DATA_AT_EXEC의 결과 포함 하는 검색 (*길이*) 매크로 및 함수의 반환 값으로는 SQL_NEED_DATA 반환 합니다.  
  
5.  호출 **SQLParamData** 는 SQL_NEED_DATA에 대 한 응답에서 값을 반환 합니다. Long 데이터를 전송 해야 하는 경우 **SQLParamData** SQL_NEED_DATA를 반환 합니다. 가리키는 버퍼에는 *ValuePtrPtr* 인수를 드라이버에는 실행 시 데이터 매개 변수를 식별 하는 값을 반환 합니다. 실행 시 데이터 매개 변수를 둘 이상 있으면 응용 프로그램;에 대 한 데이터를 보내도록 매개 변수를 확인 하려면이 값을 사용 해야 합니다. 드라이버 특정 순서로 실행 시 데이터 매개 변수에 대 한 데이터를 요청할 필요 하지 않습니다.  
  
6.  호출 **SQLPutData** 드라이버에 매개 변수 데이터를 보냅니다. 긴 데이터의 경우에 흔히 있는 매개 변수 데이터를 단일 버퍼에 맞지 않으면, 응용 프로그램 호출 **SQLPutData** 반복적으로 데이터를에서 보내도록 파트; 드라이버 및 데이터 원본 데이터를 어셈블해야 하기 때문에 달려 있습니다. Null로 끝나는 문자열 데이터를 전달 하는 응용 프로그램, 드라이버 또는 데이터 원본 리어셈블리 프로세스의 일부로 null 종료 문자를 제거 해야 합니다.  
  
7.  호출 **SQLParamData** 다시 가리키는 모든 매개 변수에 대해 데이터 전송에 해당 합니다. 드라이버는 SQL_NEED_DATA 및 다음 매개 변수를; 식별 하는 값을 반환 실행 시 데이터 매개 변수를에 전송 되지 않은 데이터의 경우 응용 프로그램 단계 6 반환합니다. 모든 실행 시 데이터 매개 변수에 대 한 데이터를 보낼 경우 문이 실행 됩니다. **SQLParamData** SQL_SUCCESS, SQL_SUCCESS_WITH_INFO 및 수를 반환 하면 반환 값 또는 진단 하는 **SQLExecute** 하거나 **SQLExecDirect** 반환할 수 있습니다.  
  
 이후에 **SQLExecute** 또는 **SQLExecDirect** SQL_NEED_DATA를 반환 합니다 이며 데이터 마지막 실행 시 데이터 매개 변수에 대 한 완전히 전송 되기 전에 문에 필요한 데이터 상태에서입니다. 문에 필요한 데이터 상태에서 이지만, 응용 프로그램 에서만 호출할 수 있습니다 **SQLPutData**를 **SQLParamData**하십시오 **SQLCancel**, **SQLGetDiagField**, 또는 **SQLGetDiagRec**; 다른 모든 함수와 반환 SQLSTATE HY010 (함수 시퀀스 오류). 호출 **SQLCancel** 문의 실행을 취소 하 고 이전 상태로 돌아갑니다. 자세한 내용은 참조 하세요. [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
 실행 시 데이터를 보내는 예에 대 한 참조를 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) 함수 설명 합니다.
