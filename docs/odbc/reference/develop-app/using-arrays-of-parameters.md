---
title: 매개 변수 배열 사용 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b584dc3d635e9fa8ce3228e4e89b0f24451fe165
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306804"
---
# <a name="using-arrays-of-parameters"></a>매개 변수 배열 사용
매개 변수의 배열을 사용 하려면 응용 프로그램 **호출 SQLSetStmtAttr** 매개 변수 집합의 수를 지정 하려면 SQL_ATTR_PARAMSET_SIZE *특성* 인수와 함께. SQL_ATTR_PARAMS_PROCESSED_PTR *특성* 인수를 사용하여 **SQLSetStmtAttr을** 호출하여 드라이버가 오류 집합을 포함하여 처리된 매개 변수 집합 의 수를 반환할 수 있는 변수의 주소를 지정합니다. 매개 변수 값의 각 행에 대 한 상태 정보를 반환 하는 배열을 가리키는 SQL_ATTR_PARAM_STATUS_PTR *특성* 인수를 사용 하 여 **SQLSetStmtAttr를** 호출 합니다. 드라이버는 이러한 주소를 명령문에 대해 유지 관리하는 구조에 저장합니다.  
  
> [!NOTE]  
>  ODBC 2. *x*, **SQLParamOptions** 매개 변수에 대 한 여러 값을 지정 하기 위해 호출 되었습니다. ODBC 3. *x*, **SQLParamOptions에** 대한 호출은 SQL_ATTR_PARAMSET_SIZE 및 SQL_ATTR_PARAMS_PROCESSED_ARRAY 특성을 설정하기 위해 **SQLSetStmtAttr에** 대한 호출로 대체되었습니다.  
  
 문을 실행 하기 전에 응용 프로그램은 각 바인딩된 배열의 각 요소의 값을 설정 합니다. 문이 실행되면 드라이버는 저장된 정보를 사용하여 매개 변수 값을 검색하고 데이터 원본으로 보냅니다. 가능하면 드라이버는 이러한 값을 배열로 보내야 합니다. 데이터 원본에 대한 단일 호출로 배열의 모든 매개 변수와 함께 SQL 문을 실행하여 매개 변수 배열의 사용을 가장 잘 구현하지만 이 기능은 현재 DBMS에서 널리 사용할 수 없습니다. 그러나 드라이버는 단일 매개 변수 집합을 가진 SQL 문을 여러 번 실행하여 시뮬레이션할 수 있습니다.  
  
 응용 프로그램에서 매개 변수 배열을 사용하기 전에 응용 프로그램에서 사용하는 드라이버에서 지원되는지 확인해야 합니다. 여기에는 두 가지 방법이 있습니다.  
  
-   매개 변수 배열을 지원하는 것으로 알려진 드라이버만 사용합니다. 응용 프로그램은 이러한 드라이버의 이름을 하드 코딩하거나 사용자에게 이러한 드라이버만 사용하도록 지시할 수 있습니다. 사용자 지정 응용 프로그램 및 수직 응용 프로그램은 일반적으로 제한된 드라이버 집합을 사용합니다.  
  
-   런타임에 매개 변수 배열의 지원을 확인합니다. SQL_ATTR_PARAMSET_SIZE 문 특성을 1보다 큰 값으로 설정할 수 있는 경우 드라이버는 매개 변수 배열을 지원합니다. 일반 응용 프로그램 및 수직 응용 프로그램은 일반적으로 런타임에 매개 변수 배열의 지원을 확인합니다.  
  
 매개 변수화된 실행의 행 개수 및 결과 집합의 가용성은 SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션으로 **SQLGetInfo를** 호출하여 결정할 수 있습니다. **INSERT**, **UPDATE**및 **DELETE** 문의 경우 SQL_PARAM_ARRAY_ROW_COUNTS 옵션은 개별 행 개수(각 매개 변수 집합에 대해 하나씩)를 사용할 수 있는지(SQL_PARC_BATCH) 또는 행 수가 SQL_PARC_NO_BATCH(SQL_PARC_NO_BATCH)로 롤업되는지 여부를 나타냅니다. **SELECT** 문의 경우 SQL_PARAM_ARRAY_SELECTS 옵션은 각 매개 변수 집합(SQL_PAS_BATCH)에 대해 결과 집합을 사용할 수 있는지 또는 하나의 결과 집합만 사용할 수 있는지 여부를 SQL_PAS_NO_BATCH 나타냅니다. 드라이버가 매개 변수 배열로 결과 집합 생성 문을 실행할 수 SQL_PARAM_ARRAY_SELECTS SQL_PAS_NO_SELECT 반환합니다. 특히 이러한 명령문에서 매개 변수를 사용하는 것은 데이터 원본에 따라다르며 ODBC SQL 문법을 따르지 않기 때문에 매개 변수 배열을 다른 유형의 문과 함께 사용할 수 있는지 여부는 데이터 원본에 따라다릅니다.  
  
 SQL_ATTR_PARAM_OPERATION_PTR 문 특성으로 가리키는 배열은 매개 변수 행을 무시하는 데 사용할 수 있습니다. 배열의 요소가 SQL_PARAM_IGNORE 설정된 경우 해당 요소에 해당하는 매개 변수 집합은 **SQLExecute** 또는 **SQLExecDirect** 호출에서 제외됩니다. SQL_ATTR_PARAM_OPERATION_PTR 특성이 가리키는 배열은 응용 프로그램에서 할당되고 채워지고 드라이버에서 읽습니다. 가져온 행이 입력 매개 변수로 사용되는 경우 행 상태 배열의 값을 매개 변수 작업 배열에 사용할 수 있습니다.  
  
## <a name="error-processing"></a>오류 처리  
 문을 실행하는 동안 오류가 발생하면 실행 함수는 오류를 반환하고 행 번호 변수를 오류를 포함하는 행 수로 설정합니다. 오류 집합을 제외한 모든 행이 실행되는지 또는 오류 집합 이전의 모든 행이 실행되는지 여부(이후)의 데이터 원본에 따라 다릅니다. 매개 변수 집합을 처리하기 때문에 드라이버는 SQL_ATTR_PARAMS_PROCESSED_PTR 문 특성에 의해 지정된 버퍼를 현재 처리 중인 행 의 수로 설정합니다. 오류 집합을 제외한 모든 집합이 실행되면 드라이버는 모든 행이 처리된 후 SQL_ATTR_PARAMSET_SIZE 이 버퍼를 설정합니다.  
  
 SQL_ATTR_PARAM_STATUS_PTR 문 특성이 설정된 경우 **SQLExecute** 또는 **SQLExecDirect는** 각 매개 변수 집합의 상태를 제공하는 *매개 변수 상태 배열을* 반환합니다. 매개 변수 상태 배열은 응용 프로그램에 의해 할당되고 드라이버에 의해 채워질 수 있습니다. 해당 요소는 매개 변수 행에 대해 SQL 문이 성공적으로 실행되었는지 또는 매개 변수 집합을 처리하는 동안 오류가 발생했는지 여부를 나타냅니다. 오류가 발생하면 드라이버는 매개 변수 상태 배열의 해당 값을 SQL_PARAM_ERROR 설정하고 SQL_SUCCESS_WITH_INFO 반환합니다. 응용 프로그램은 상태 배열을 확인하여 처리된 행을 확인할 수 있습니다. 행 번호를 사용하여 응용 프로그램은 종종 오류를 수정하고 처리를 다시 시작할 수 있습니다.  
  
 매개 변수 상태 배열이 사용되는 방법은 SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션 **SQLGetInfo**에 대한 호출에 의해 반환되는 옵션에 의해 결정됩니다. **INSERT**, **UPDATE**및 **DELETE** 문의 경우 SQL_PARAM_ARRAY_ROW_COUNTS SQL_PARC_BATCH 반환되는 경우 매개 변수 상태 배열이 상태 정보로 채워지지만 SQL_PARC_NO_BATCH 반환되지는 않습니다. **SELECT** 문의 경우 SQL_PARAM_ARRAY_SELECT SQL_PAS_BATCH 반환되는 경우 매개 변수 상태 배열이 채워지지만 SQL_PAS_NO_BATCH 또는 SQL_PAS_NO_SELECT 반환되지는 않습니다.  
  
## <a name="data-at-execution-parameters"></a>실행 시 데이터 매개 변수  
 길이/표시기 배열의 값 중 SQL_DATA_AT_EXEC 또는*SQL_LEN_DATA_AT_EXEC(길이)* 매크로의 결과인 경우 해당 값에 대한 데이터는 일반적인 방법으로 **SQLPutData와** 함께 전송됩니다. 이 프로세스의 다음 측면은 쉽게 명확하지 않기 때문에 특별한 설명을 합니다.  
  
-   드라이버가 SQL_NEED_DATA 반환하면 행 번호 변수의 주소를 데이터가 필요한 행으로 설정해야 합니다. 단일 값 의 경우와 마찬가지로 응용 프로그램은 드라이버가 단일 매개 변수 집합 내에서 매개 변수 값을 요청하는 순서에 대해 어떠한 가정도 할 수 없습니다. 실행 시 데이터 매개 변수의 실행에서 오류가 발생하는 경우 SQL_ATTR_PARAMS_PROCESSED_PTR 문 특성에 의해 지정된 버퍼는 오류가 발생한 행의 수로 설정되고, SQL_ATTR_PARAM_STATUS_PTR 문 특성에 의해 지정된 행 상태 배열의 행 상태가 SQL_PARAM_ERROR 설정되고 **SQLExecute**, **SQLExecDirect**, **SQLParamData**또는 **SQLPutData에** 대한 호출은 SQL_ERROR 반환합니다. 이 버퍼의 내용은 **SQLExecute,** **SQLExecDirect**또는 **SQLParamData** 반환 SQL_STILL_EXECUTING 경우 정의되지 않습니다.  
  
-   드라이버는 데이터 실행 매개 **변수에** 대 한 *SQLBindParameter의 ParameterValuePtr* 인수에서 값을 해석 하지 않습니다 때문에 응용 프로그램 배열에 대 한 포인터를 제공 하는 경우 **SQLParamData** 추출 하 고 응용 프로그램에이 배열의 요소를 반환 하지 않습니다. 대신 응용 프로그램에서 제공한 스칼라 값을 반환합니다. 즉, **SQLParamData에서** 반환하는 값은 응용 프로그램이 데이터를 전송해야 하는 매개 변수를 지정하기에 충분하지 않습니다. 응용 프로그램은 또한 현재 행 번호를 고려해야 합니다.  
  
     매개 변수 배열의 일부 요소만 실행 시 데이터 매개 변수인 경우 응용 프로그램은 모든 매개 변수에 대한 요소를 포함하는 *ParameterValuePtr에서* 배열의 주소를 전달해야 합니다. 이 배열은 실행 시 데이터 매개 변수가 아닌 매개 변수에 대해 일반적으로 해석됩니다. 실행 시 데이터 매개 변수의 경우 **SQLParamData가** 응용 프로그램에 제공하는 값은 일반적으로 드라이버가 이 경우 요청하는 데이터를 식별하는 데 사용할 수 있는 배열의 주소입니다.
