---
title: 매개 변수 배열 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ff4a76c38f04c7b9b12842ef800bc8a26a27ed9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312518"
---
# <a name="using-arrays-of-parameters"></a>매개 변수 배열 사용
응용 프로그램이 호출 매개 변수의 배열을 사용 하 **SQLSetStmtAttr** 사용 하 여는 *특성* 인수의 SQL_ATTR_PARAMSET_SIZE 매개 변수 집합의 수를 지정 합니다. 호출한 **SQLSetStmtAttr** 사용 하 여는 *특성* 드라이버 수를 처리 하는 매개 변수 집합의 수를 반환 하는 변수의 주소를 지정 하는 SQL_ATTR_PARAMS_PROCESSED_PTR 인수 포함 하 여 오류를 설정합니다. 호출한 **SQLSetStmtAttr** 사용 하 여는 *특성* 매개 변수 값의 각 행에 대 한 상태 정보를 반환 하는 배열을를 가리키도록 SQL_ATTR_PARAM_STATUS_PTR의 인수입니다. 드라이버는 이러한 주소 문에 대 한 유지 관리 구조에 저장 합니다.  
  
> [!NOTE]  
>  Odbc 2. *x*하십시오 **SQLParamOptions** 매개 변수의 여러 값을 지정 하기 위해 호출 되었습니다. Odbc 3. *x*에 대 한 호출 **SQLParamOptions** 에 대 한 호출으로 대체 되었습니다 **SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE 및 SQL_ATTR_PARAMS_PROCESSED_ARRAY 속성을 설정 하려면 .  
  
 문을 실행 하기 전에 응용 프로그램이 바인딩된 각 배열의 각 요소 값을 설정 합니다. 드라이버 매개 변수 값을 검색 하는 데이터 원본에 보낼 수에 저장 한 정보를 사용 하 여 문이 실행 된 경우 가능한 경우 드라이버는 배열로 이러한 값을 전송 해야 합니다. 매개 변수 배열 사용 하는 데이터 원본에 대 한 단일 호출을 사용 하 여 배열의 모든 매개 변수를 사용 하 여 SQL 문을 실행 하 여 최적으로 구현 됩니다, 있지만이 기능은 광범위 하 게 사용할 수 없는 경우 Dbms의 오늘 그러나 드라이버 단일 매개 변수 집합을 사용 하 여 각 SQL 문을 여러 번 실행 하 여 시뮬레이트할 수 있습니다.  
  
 응용 프로그램 매개 변수 배열에 사용 하기 전에 응용 프로그램에서 사용 하는 드라이버에서 지원 되는지 이어야 합니다. 이때 다음과 같은 두 가지 방법을 사용할 수 있습니다.  
  
-   배열 매개 변수를 지원 하기 위해 알려진 드라이버만 사용 합니다. 응용 프로그램이 이러한 드라이버의 이름을 하드 코딩할 수 또는 사용자만이 드라이버를 사용 하도록 할 수 있습니다. 사용자 지정 응용 프로그램 및 수직 시장 응용 프로그램 제한 된 드라이버 집합을 일반적으로 사용 합니다.  
  
-   런타임에 매개 변수 배열에 대 한 지원 확인 합니다. 드라이버는 SQL_ATTR_PARAMSET_SIZE 문 특성을 1 보다 큰 값으로 설정할 수 있으면 매개 변수 배열을 지원 합니다. 일반 응용 프로그램 및 수직 응용 프로그램을 일반적으로 매개 변수 배열에 대 한 지원 런타임에 검사 합니다.  
  
 호출 하 여 행 개수 및 매개 변수가 있는 실행의 결과 집합의 가용성을 확인할 수 있습니다 **SQLGetInfo** SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션을 사용 하 여 합니다. 에 대 한 **삽입**하십시오 **업데이트**, 및 **삭제** 문을 SQL_PARAM_ARRAY_ROW_COUNTS 옵션은 개별 행 개수 (각 매개 변수 집합에 대해 하나) 되는지 여부를 나타냅니다 사용할 수 있습니다 (SQL_PARC_BATCH) 또는 행 개수 여부 (SQL_PARC_NO_BATCH) 하나에 롤업 됩니다. 에 대 한 **선택** 하나만 결과 집합의 사용 가능한 (SQL_PAS_NO_BATCH) 인지 또는 결과 집합을 각 매개 변수 (SQL_PAS_BATCH) 집합에 사용할 수 있는 인지 문을 SQL_PARAM_ARRAY_SELECTS 옵션을 나타냅니다. 드라이버는 결과 집합 생성 문 매개 변수 배열을 사용 하 여 실행을 허용 하지 않으면 SQL_PARAM_ARRAY_SELECTS SQL_PAS_NO_SELECT를 반환 합니다. 매개 변수 배열을 사용할 수 다른 유형의 문 사용 하 여 이러한 문의 매개 변수에 사용 데이터 소스 관련 되 고 ODBC SQL 문법에 따르지는 때문에 특히 여부를 데이터 소스 관련 것입니다.  
  
 SQL_ATTR_PARAM_OPERATION_PTR 문 특성에서 가리키는 배열 매개 변수는 행을 무시 하 사용할 수 있습니다. 배열 요소의 SQL_PARAM_IGNORE로 해당 요소에 해당 하는 매개 변수 집합에서 제외 됩니다 합니다 **SQLExecute** 하거나 **SQLExecDirect** 호출 합니다. SQL_ATTR_PARAM_OPERATION_PTR 특성에서 가리키는 배열 할당 되 및 응용 프로그램에서 입력 되 고 드라이버에서 읽기. 인출된 된 행을 입력된 매개 변수로 사용 하는 경우 행 상태 배열 값 매개 변수 작업 배열에서 사용할 수 있습니다.  
  
## <a name="error-processing"></a>오류 처리  
 문을 실행 하는 동안 오류가 발생 하는 경우 실행 함수 오류 반환 하 고 오류를 포함 하는 행 수가 행 숫자 변수를 설정 합니다. 모든 행 오류 집합 실행 되거나 오류 집합 실행 됩니다 (그러나 이후부터 아님) 하기 전에 모든 행이 있는지 여부를 제외 하 고 있는지 여부를 데이터 소스 관련 것입니다. 매개 변수 집합을 처리 하기 때문에 드라이버는 현재 처리 중인 행의 수 문 특성 sql_attr_params_processed_ptr은 지정한 버퍼를 설정 합니다. 오류 집합 실행 됩니다 점을 제외 하 고로 설정 하는 모든 드라이버 모든 행이 처리 된 후 SQL_ATTR_PARAMSET_SIZE 하려면이 버퍼를 설정 합니다.  
  
 SQL_ATTR_PARAM_STATUS_PTR 문 특성에 설정한 경우 **SQLExecute** 하거나 **SQLExecDirect** 반환 된 *매개 변수 상태 배열을* 상태를 제공 하는 각 매개 변수 집합입니다. 매개 변수 상태 배열은 응용 프로그램에 의해 할당 되 고 드라이버에서 입력 합니다. 해당 요소는 SQL 문이 된 매개 변수 행에 대해 성공적으로 실행 되었는지 여부 또는 매개 변수 집합을 처리 하는 동안 오류가 발생 했는지 여부를 나타냅니다. 오류가 발생 하는 경우 드라이버 SQL_PARAM_ERROR 매개 변수 상태 배열에서 해당 값을 설정 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다. 응용 프로그램에서는 상태 배열을 행이 처리 결정을 확인할 수 있습니다. 행 번호를 사용 하 여, 응용 프로그램 수 종종 오류를 수정한 처리를 다시 시작 합니다.  
  
 에 대 한 호출에서 반환 된 SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션에 따라 결정 됩니다 매개 변수 상태 배열을 사용 하는 방법을 **SQLGetInfo**합니다. 에 대 한 **삽입**하십시오 **업데이트**, 및 **삭제** SQL_PARC_BATCH SQL_PARAM_ARRAY_에 대해 반환 되 면 상태 정보를 사용 하 여 문을 매개 변수 상태 배열을 채워집니다 ROW_COUNTS, 하지만 SQL_PARC_NO_BATCH이 반환 하는 경우에 아닙니다. 에 대 한 **선택** 문 매개 변수 상태 배열을 채워집니다 SQL_PAS_BATCH SQL_PARAM_ARRAY_SELECT에 대 한 반환 되 면 하지만 SQL_PAS_NO_BATCH 또는 SQL_PAS_NO_SELECT 반환 되는 경우에 없습니다.  
  
## <a name="data-at-execution-parameters"></a>실행 시 데이터 매개 변수  
 SQL_LEN_DATA_AT_EXEC 결과 또는 SQL_DATA_AT_EXEC를 경우 길이/표시기 배열에 값 (*길이*) 매크로 해당 값에 대 한 데이터와 함께 보내집니다 **SQLPutData** 일반적인 방식입니다. 이 프로세스의 다음 측면을 띄지 하지 않기 때문에 특별 한 주석 주의:  
  
-   드라이버 sql_need_data가 반환 될 때 필요한 데이터 행에 행 번호 변수의 주소를 설정 합니다. 단일 값 처럼 응용 프로그램 드라이버에서 매개 변수는 단일 집합 내에서 매개 변수 값을 요청 하는 데는 순서에 대 한 가정을 만들 수 없습니다. 문 특성 sql_attr_params_processed_ptr은 지정 된 버퍼는이 오류가 발생 하 여 지정 된 행 상태 배열에 있는 행에 대 한 상태 행의 수 설정 실행 시 데이터 매개 변수의 실행에서 오류가 발생 하는 경우 SQL_ATTR_PARAM_STATUS_PTR 문 특성은 SQL_PARAM_ERROR, 및에 대 한 호출으로 **SQLExecute**, **SQLExecDirect**하십시오 **SQLParamData**, 또는  **SQLPutData** SQL_ERROR를 반환 합니다. 경우에이 버퍼의 내용을 정의 되지 않습니다 **SQLExecute**를 **SQLExecDirect**, 또는 **SQLParamData** SQL_STILL_EXECUTING을 반환 합니다.  
  
-   드라이버는 값을 해석 하지 않으므로 하므로 합니다 *ParameterValuePtr* 인수의 **SQLBindParameter** 실행 시 데이터 매개 변수의 경우 응용 프로그램을 배열에 대 한 포인터를 제공 하는 경우  **SQLParamData** 추출 되지 않으며 응용 프로그램에이 배열의 요소를 반환 합니다. 대신, 응용 프로그램 스칼라 값이 제공 하는 반환 합니다. 반환한 값 즉 **SQLParamData** 데이터를 보내도록 해야 응용 프로그램 매개 변수를 지정 하는 것이 부족은 응용 프로그램도는 현재 행 번호를 고려해 야 합니다.  
  
     경우 실행 시 데이터 매개 변수가 매개 변수 배열의 요소 중 일부에 응용 프로그램 전달 해야 배열 주소의 *ParameterValuePtr* 모든 매개 변수에 대 한 요소가 들어 있는입니다. 실행 시 데이터 매개 변수가 매개 변수의이 배열은 일반적으로 해석 됩니다. 실행 시 데이터 매개 변수 값에 대 한는 **SQLParamData** 제공 일반적으로 사용할 수 있는 드라이버가이 경우에 요청 하는 데이터를 확인, 응용 프로그램은 항상 배열의 주소입니다.
