---
title: "매개 변수 배열을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a7c6a6ee4f066925d2a7ec46a2186134d75cb7e4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-arrays-of-parameters"></a>매개 변수 배열을 사용 하 여
매개 변수를 호출 하 여 응용 프로그램의 배열을 사용 하 **SQLSetStmtAttr** 와 *특성* SQL_ATTR_PARAMSET_SIZE 매개 변수 집합의 수를 지정할 수의 인수입니다. 호출 **SQLSetStmtAttr** 와 *특성* SQL_ATTR_PARAMS_PROCESSED_PTR 드라이버 처리 하는 매개 변수 집합의 수를 반환할 수 있는 변수의 주소를 지정할 수의 인수 포함 하 여 오류를 설정합니다. 호출 **SQLSetStmtAttr** 와 *특성* 매개 변수 값의 각 행에 대 한 상태 정보를 반환 하는 배열을 가리키는 SQL_ATTR_PARAM_STATUS_PTR의 인수입니다. 드라이버는 이러한 주소 문에 대 한 유지 관리 하는 구조에 저장 합니다.  
  
> [!NOTE]  
>  Odbc 2. *x*, **SQLParamOptions** 매개 변수에 대해 여러 값을 지정 하기 위해 호출 되었습니다. Odbc 3. *x*에 대 한 호출 **SQLParamOptions** 에 대 한 호출으로 대체 되었습니다 **SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE 및 SQL_ATTR_PARAMS_PROCESSED_ARRAY 특성을 설정 하려면 .  
  
 해당 문을 실행 하기 전에 응용 프로그램 바인딩된 각 배열의 각 요소 값을 설정 합니다. 드라이버 매개 변수 값을 검색 한; 데이터 원본에 보내야 하는 저장 된 정보를 사용 하 여 문이 실행 되는 경우 가능 하면 드라이버가 이러한 값 배열로 보냅니다. 매개 변수 배열 사용 하는 데이터 원본에 대 한 단일 호출으로 배열에 있는 모든 매개 변수를 사용 하 여 SQL 문을 실행 하 여 구현할지 있지만이 기능이 광범위 하 게 사용할 수 없는 경우 Dbms에서 오늘 그러나 드라이버 각각 단일 매개 변수 집합이 있는 SQL 문을 여러 번 실행 하 여 것 시뮬레이션할 수 있습니다.  
  
 응용 프로그램에 매개 변수 배열을 사용 하기 전에 응용 프로그램에서 사용 하는 드라이버에서 지원 하는지 확인 해야 합니다. 이때 다음과 같은 두 가지 방법을 사용할 수 있습니다.  
  
-   매개 변수 배열을 지 원하는 드라이버에만 사용 합니다. 응용 프로그램이 이러한 드라이버의 이름을 하드 코딩할 수 또는 사용자만이 드라이버를 사용 하도록 할 수 있습니다. 사용자 지정 응용 프로그램 및 세로 응용 프로그램 보통 제한 된 드라이버 집합을 사용합니다.  
  
-   실행 시 매개 변수 배열의 지원을 확인 합니다. 드라이버는 SQL_ATTR_PARAMSET_SIZE 문 특성을 1 보다 큰 값으로 설정 하는 경우 매개 변수 배열을 지원 합니다. 일반 응용 프로그램 및 수직 응용 프로그램을 일반적으로 매개 변수 배열에 대 한 지원 런타임에 검사 합니다.  
  
 행 개수와 매개 변수가 있는 실행에서 결과 집합의 가용성을 호출 하 여 확인할 수 있습니다 **SQLGetInfo** SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션입니다. 에 대 한 **삽입**, **업데이트**, 및 **삭제** 개별 행 개수 (각 매개 변수 집합에 대해 각각 하나씩)이 있는지 문, SQL_PARAM_ARRAY_ROW_COUNTS 옵션 표시 사용 가능한 (SQL_PARC_BATCH) 또는 행 개수 여부 (SQL_PARC_NO_BATCH) 하나에 롤업 됩니다. 에 대 한 **선택** 결과 집합은 각 매개 변수 (SQL_PAS_BATCH) 집합에 사용할 수 있는지 여부 또는 하나의 결과 집합 인지 사용할 수 있는 (SQL_PAS_NO_BATCH) 문, SQL_PARAM_ARRAY_SELECTS 옵션을 나타냅니다. 드라이버는 결과 집합 생성-실행할 문을 매개 변수 배열을 사용을 허용 하지 않는 경우 SQL_PARAM_ARRAY_SELECTS SQL_PAS_NO_SELECT를 반환 합니다. 이러한 문에서 매개 변수 사용은 데이터 원본에 따른 특정 되며 ODBC SQL 문법을 따르지 것 때문에 특히, 매개 변수 배열을 다른 형식의 문의와 사용할 수 있는지 여부를 데이터 원본에 따른 특정을입니다.  
  
 매개 변수는 행을 무시 하 SQL_ATTR_PARAM_OPERATION_PTR 문 특성에서 가리키는 배열을 사용할 수 있습니다. 배열의 요소 SQL_PARAM_IGNORE로 설정 되어 요소에 해당 하는 매개 변수 집합에서 제외 됩니다는 **SQLExecute** 또는 **SQLExecDirect** 호출 합니다. SQL_ATTR_PARAM_OPERATION_PTR 특성에서 가리키는 배열 할당 되 고 응용 프로그램은 입력 되 고 드라이버에서 읽은 합니다. 인출 된 행으로 입력된 매개 변수를 사용 하는 매개 변수 작업 배열에서 행 상태 배열이의 값을 사용할 수 있습니다.  
  
## <a name="error-processing"></a>오류 처리  
 문을 실행 하는 동안 오류가 발생 하는 경우 실행 함수에서 오류를 반환 하 고 오류를 포함 하는 행의 수에 행 번호 변수를 설정 합니다. 모든 행 오류 집합 실행 되거나 오류 집합 실행 됩니다 (않음 다음 날짜까지) 하기 전에 모든 행이 있는지 여부를 제외 하 고 있는지 여부를 데이터 원본에 따른 특정을입니다. 매개 변수 집합을 처리 하기 때문에 드라이버가 SQL_ATTR_PARAMS_PROCESSED_PTR 매개 변수 특성의 현재 처리 중인 행 수로 지정 된 버퍼를 설정 합니다. 오류 집합 실행 되는 점을 제외 하 고로 설정 하는 모든 드라이버 모든 행이 처리 된 후 SQL_ATTR_PARAMSET_SIZE를이 버퍼를 설정 합니다.  
  
 SQL_ATTR_PARAM_STATUS_PTR 문 특성 설정 된 경우 **SQLExecute** 또는 **SQLExecDirect** 반환 된 *매개 변수 상태 배열을* 상태를 제공 하는 각 매개 변수 집합입니다. 매개 변수 상태 배열은 응용 프로그램에 의해 할당 되 고 드라이버에 의해 채워집니다. 해당 요소는 SQL 문이 매개 변수 행에 대해 성공적으로 실행 되었는지 여부 또는 매개 변수 집합을 처리 하는 동안 오류가 발생 했는지 여부를 나타냅니다. 오류가 발생 한 경우 드라이버 SQL_PARAM_ERROR에 매개 변수 상태 배열을의 해당 값을 설정 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다. 응용 프로그램 상태 배열을 어떤 행이 처리를 확인 하려면 확인할 수 있습니다. 행 번호를 사용 하 여 응용 프로그램 수 종종 오류를 수정 하 고 처리를 다시 시작 합니다.  
  
 매개 변수 상태 배열을 사용 되는 방법에 대 한 호출에서 반환 된 SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션에 의해 결정 됩니다 **SQLGetInfo**합니다. 에 대 한 **삽입**, **업데이트**, 및 **삭제** SQL_PARC_BATCH SQL_PARAM_ARRAY_에 대해 반환 되 면 상태 정보를 사용 하 여 문, 매개 변수 상태 배열을 채워집니다 ROW_COUNTS, 하지만 SQL_PARC_NO_BATCH 반환 되 면 not 합니다. 에 대 한 **선택** 문, 매개 변수 상태 배열을에 이름이 입력 되어 SQL_PAS_BATCH SQL_PARAM_ARRAY_SELECT에 대 한 반환 되 면 하지만 SQL_PAS_NO_BATCH 또는 SQL_PAS_NO_SELECT 반환 되는 경우에 없습니다.  
  
## <a name="data-at-execution-parameters"></a>실행 시 데이터 매개 변수  
 SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 결과 길이/표시기 배열에 있는 값 중 하나일 경우 (*길이*) 매크로 해당 값에 대 한 데이터와 함께 보내집니다 **SQLPutData** 일반적인 방식입니다. 이 프로세스의 다음 양상 띄지 되지 않기 때문에 특수 주석을 해야 합니다.  
  
-   드라이버에서 sql_need_data가 반환 될 때 필요한 데이터 행에 행 번호 변수의 주소를 설정 합니다. 마찬가지로 단일 값, 응용 프로그램이 드라이버에서 단일 매개 변수 집합 내에서 매개 변수 값을 요청 하는 데는 순서에 대 한 가정을 만들 수 없습니다. SQL_ATTR_PARAMS_PROCESSED_PTR 매개 변수 특성으로 지정 된 버퍼에 오류가 발생 한, 변수로 지정 된 행 상태 배열에 있는 행에 대 한 상태 행의 수로 설정 되어 실행 시 데이터 매개 변수를 실행 하는 오류가 발생 하는 경우 SQL_ATTR_PARAM_STATUS_PTR 문 특성이 SQL_PARAM_ERROR, 및에 대 한 호출으로 설정 된 **SQLExecute**, **SQLExecDirect**, **SQLParamData**, 또는 ** SQLPutData** SQL_ERROR를 반환 합니다. 경우에이 버퍼의 내용을 정의 되지 않습니다 **SQLExecute**, **SQLExecDirect**, 또는 **SQLParamData** SQL_STILL_EXECUTING을 반환 합니다.  
  
-   드라이버는 값을 해석 하지 않으므로 때문에 *ParameterValuePtr* 의 인수 **SQLBindParameter** 실행 시 데이터 매개 변수를 응용 프로그램 하 여 배열에 대 한 포인터를 제공 하는 경우에 대 한 ** SQLParamData** 추출 및 응용 프로그램에이 배열의 요소를 반환 하지 않습니다. 대신, 응용 프로그램 스칼라 값이 제공 하는 반환 합니다. 반환한 값 즉 **SQLParamData** 은 매개 변수를 지정 하는 데 충분 하지 응용 프로그램 데이터를 보내는 응용 프로그램도 현재 행 번호를 고려해 야 합니다.  
  
     실행 시 데이터 매개 변수가 매개 변수 배열의 요소 중 일부에 응용 프로그램 해야 통과 경우 배열 주소 *ParameterValuePtr* 모든 매개 변수에 대해 요소가 들어 있는입니다. 실행 시 데이터 매개 변수가 아닌 매개 변수에 대 한이 배열은 일반적으로 해석 됩니다. 실행 시 데이터 매개 변수 값에 대 한는 **SQLParamData** 를 제공 합니다. 일반적으로 사용할 수 있는이 경우에는 드라이버를 요청 하는 데이터를 확인, 응용 프로그램은 항상 배열의 주소입니다.

