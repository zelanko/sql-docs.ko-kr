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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aeeeb716aa2f9a72338f3aeb586dffce86f84069
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304184"
---
# <a name="sending-long-data"></a>Long 데이터 전송
Dbms는 *긴 데이터* 를 254 문자와 같이 특정 크기의 문자 또는 이진 데이터로 정의 합니다. 항목이 긴 텍스트 문서 또는 비트맵을 나타내는 경우 처럼 긴 데이터의 전체 항목을 메모리에 저장 하지 못할 수 있습니다. 이러한 데이터는 단일 버퍼에 저장할 수 없기 때문에 문이 실행 될 때 데이터 원본에서 **Sqlputdata** 를 사용 하 여 해당 데이터를 드라이버에 드라이버로 보냅니다. 실행 시 데이터를 전송 하는 매개 변수를 *실행 시 데이터 매개 변수*라고 합니다.  
  
> [!NOTE]  
>  응용 프로그램은 실행 시 **Sqlputdata**를 사용 하 여 모든 형식의 데이터를 실제로 전송할 수 있지만 문자 및 이진 데이터만 파트에 보낼 수 있습니다. 그러나 데이터가 단일 버퍼에 맞게 충분히 작은 경우 일반적으로 **Sqlputdata**를 사용할 이유가 없습니다. 버퍼를 바인딩하는 것이 훨씬 쉬우며 드라이버에서 버퍼의 데이터를 검색할 수 있습니다.  
  
 실행 시 데이터를 보내기 위해 응용 프로그램은 다음 작업을 수행 합니다.  
  
1.  버퍼의 주소를 전달 하는 대신 **SQLBindParameter** 의 *Parametervalueptr* 인수에서 매개 변수를 식별 하는 32 비트 값을 전달 합니다. 이 값은 드라이버에서 분석 되지 않습니다. 나중에 응용 프로그램에 반환 되므로 응용 프로그램에 대 한 내용을 의미 해야 합니다. 예를 들어 매개 변수 수 또는 데이터를 포함 하는 파일의 핸들 일 수 있습니다.  
  
2.  **SQLBindParameter**의 *StrLen_or_IndPtr* 인수에서 길이/표시기 버퍼의 주소를 전달 합니다.  
  
3.  길이/표시기 버퍼에 SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC (*길이*) 매크로의 결과를 저장 합니다. 이 두 값은 매개 변수에 대 한 데이터가 **Sqlputdata**를 사용 하 여 전송 됨을 드라이버에 표시 합니다. SQL_LEN_DATA_AT_EXEC (*길이*)는 공간을 미리 할당할 수 있도록 전송할 long 데이터의 바이트 수를 확인 해야 하는 데이터 원본으로 긴 데이터를 보낼 때 사용 됩니다. 데이터 원본에이 값이 필요한 지 여부를 확인 하기 위해 응용 프로그램은 SQL_NEED_LONG_DATA_LEN 옵션으로 **SQLGetInfo** 를 호출 합니다. 모든 드라이버는이 매크로를 지원 해야 합니다. 데이터 원본에 바이트 길이가 필요 하지 않은 경우 드라이버는이를 무시할 수 있습니다.  
  
4.  **Sqlexecute** 또는 **sqlexecdirect**를 호출 합니다. 이 드라이버는 길이/표시기 버퍼에 SQL_LEN_DATA_AT_EXEC (*length*) 매크로의 값 SQL_DATA_AT_EXEC 또는 값이 포함 되어 있음을 검색 하 고 SQL_NEED_DATA를 함수의 반환 값으로 반환 합니다.  
  
5.  SQL_NEED_DATA 반환 값에 대 한 응답으로 **Sqlparamdata** 를 호출 합니다. Long 데이터를 전송 해야 하는 경우 **Sqlparamdata** 는 SQL_NEED_DATA을 반환 합니다. 이상 *값에 의해* 가리키는 버퍼에서 드라이버는 실행 시 데이터 매개 변수를 식별 하는 값을 반환 합니다. 실행 시 데이터 매개 변수가 두 개 이상인 경우에는 응용 프로그램에서이 값을 사용 하 여 데이터를 보낼 매개 변수를 결정 해야 합니다. 드라이버는 특정 순서로 실행 시 데이터 매개 변수에 대 한 데이터를 요청 하는 데 필요 하지 않습니다.  
  
6.  **Sqlputdata** 를 호출 하 여 매개 변수 데이터를 드라이버로 보냅니다. 긴 데이터를 사용 하는 경우 처럼 매개 변수 데이터가 단일 버퍼에 맞지 않는 경우 응용 프로그램은 **Sqlputdata** 를 반복적으로 호출 하 여 데이터를 파트로 보냅니다. 데이터를 다시 어셈블할 수 있는 드라이버 및 데이터 원본이 있습니다. 응용 프로그램이 null로 끝나는 문자열 데이터를 전달 하는 경우에는 드라이버 또는 데이터 원본이 리어셈블리 프로세스의 일부로 null 종료 문자를 제거 해야 합니다.  
  
7.  **Sqlparamdata** 를 다시 호출 하 여 매개 변수에 대 한 모든 데이터를 보냈는지 여부를 표시 합니다. 데이터가 전송 되지 않은 실행 시 데이터 매개 변수가 있는 경우 드라이버는 SQL_NEED_DATA을 반환 하 고 다음 매개 변수를 식별 하는 값을 반환 합니다. 응용 프로그램이 6 단계로 돌아옵니다. 모든 실행 시 데이터 매개 변수에 대해 데이터를 보낸 경우 문이 실행 됩니다. **Sqlparamdata** 는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하며, **Sqlexecute** 또는 **sqlparamdata** 에서 반환할 수 있는 반환 값 또는 진단을 반환할 수 있습니다.  
  
 **Sqlexecute** 또는 **sqlexecdirect** 는 SQL_NEED_DATA을 반환 하 고 마지막 실행 시 데이터 매개 변수에 대 한 데이터를 완전히 보내기 전에 데이터를 요구 하는 상태에 있습니다. 문이 데이터의 필요 상태에 있는 동안 응용 프로그램은 **Sqlputdata**, **sqlputdata**, **Sqlcancel**, **SQLGetDiagField**또는 **SQLGetDiagRec**만 호출할 수 있습니다. 다른 모든 함수는 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다. **Sqlcancel** 을 호출 하면 문의 실행이 취소 되 고 이전 상태로 돌아갑니다. 자세한 내용은 [부록 B: ODBC 상태 전환 표](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)를 참조 하세요.  
  
 실행 시 데이터를 전송 하는 예제는 [Sqlputdata](../../../odbc/reference/syntax/sqlputdata-function.md) 함수 설명을 참조 하세요.
