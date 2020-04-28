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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b584dc3d635e9fa8ce3228e4e89b0f24451fe165
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306804"
---
# <a name="using-arrays-of-parameters"></a>매개 변수 배열 사용
매개 변수 배열을 사용 하기 위해 응용 프로그램은 SQL_ATTR_PARAMSET_SIZE의 *특성* 인수를 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 매개 변수 집합의 수를 지정 합니다. SQL_ATTR_PARAMS_PROCESSED_PTR의 *특성* 인수를 사용 하 여 **SQLSetStmtAttr** 를 호출 하 여 드라이버가 오류 집합을 포함 하 여 처리 된 매개 변수 집합의 수를 반환할 수 있는 변수의 주소를 지정 합니다. SQL_ATTR_PARAM_STATUS_PTR의 *특성* 인수를 사용 하는 **SQLSetStmtAttr** 를 호출 하 여 매개 변수 값의 각 행에 대 한 상태 정보를 반환 하는 배열을 가리킵니다. 이 드라이버는 문에 대해 유지 관리 되는 구조에 이러한 주소를 저장 합니다.  
  
> [!NOTE]  
>  ODBC 2. *x*, **sqlparamoptions** 를 호출 하 여 매개 변수에 대해 여러 값을 지정 했습니다. ODBC 3. *x*SQL_ATTR_PARAMSET_SIZE 및 SQL_ATTR_PARAMS_PROCESSED_ARRAY 특성을 설정 하기 위해 **SQLSetStmtAttr** 에 대 한 호출로 **sqlparamoptions** 호출을 대체 했습니다.  
  
 문을 실행 하기 전에 응용 프로그램은 각 바인딩된 배열의 각 요소에 대 한 값을 설정 합니다. 문이 실행 되 면 드라이버는 저장 된 정보를 사용 하 여 매개 변수 값을 검색 하 고 데이터 원본으로 보냅니다. 가능 하면 드라이버는 이러한 값을 배열로 전송 해야 합니다. 매개 변수 배열을 사용 하는 것은 데이터 원본에 대 한 단일 호출을 사용 하 여 배열의 모든 매개 변수를 사용 하 여 SQL 문을 실행 하는 것이 가장 좋습니다 .이 기능은 현재 Dbms에서 광범위 하 게 사용할 수 없습니다. 그러나 드라이버는 단일 매개 변수 집합을 사용 하 여 SQL 문을 여러 번 실행 하 여 시뮬레이션할 수 있습니다.  
  
 응용 프로그램에서 매개 변수 배열을 사용 하기 전에 응용 프로그램에서 사용 하는 드라이버에서 매개 변수를 지원 하는지 알아야 합니다. 여기에는 두 가지 방법이 있습니다.  
  
-   매개 변수 배열을 지 원하는 것으로 알려진 드라이버만 사용 합니다. 응용 프로그램은 이러한 드라이버의 이름을 하드 코딩 하거나 사용자에 게 이러한 드라이버만 사용 하도록 지시할 수 있습니다. 사용자 지정 응용 프로그램 및 수직 응용 프로그램은 일반적으로 제한 된 드라이버 집합을 사용 합니다.  
  
-   런타임에 매개 변수 배열이 지원 되는지 확인 합니다. SQL_ATTR_PARAMSET_SIZE statement 특성을 1 보다 큰 값으로 설정할 수 있는 경우 드라이버는 매개 변수 배열을 지원 합니다. 일반 응용 프로그램 및 수직 응용 프로그램은 일반적으로 런타임에 매개 변수 배열에 대 한 지원을 확인 합니다.  
  
 매개 변수가 있는 실행에서 행 개수와 결과 집합의 가용성은 SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션으로 **SQLGetInfo** 를 호출 하 여 확인할 수 있습니다. **INSERT**, **UPDATE**및 **DELETE** 문의 경우 SQL_PARAM_ARRAY_ROW_COUNTS 옵션은 개별 행 개수 (각 매개 변수 집합에 대해 하나씩)를 사용할 수 있는지 (SQL_PARC_BATCH) 또는 행 개수가 1로 롤업 되는지 (SQL_PARC_NO_BATCH)를 나타냅니다. **SELECT** 문의 경우 SQL_PARAM_ARRAY_SELECTS 옵션은 각 매개 변수 집합에 대해 결과 집합을 사용할 수 있는지 (SQL_PAS_BATCH) 또는 하나의 결과 집합을 사용할 수 있는지 여부 (SQL_PAS_NO_BATCH)를 나타냅니다. 드라이버에서 매개 변수 배열을 사용 하 여 결과 집합 생성 문을 실행 하는 것을 허용 하지 않는 경우 SQL_PARAM_ARRAY_SELECTS는 SQL_PAS_NO_SELECT 반환 합니다. 매개 변수 배열을 다른 형식의 문과 함께 사용할 수 있는지 여부는 데이터 원본에 따라 다릅니다. 특히 이러한 문에서 매개 변수를 사용 하는 것은 데이터 원본에 따라 다르므로 ODBC SQL 문법을 따르지 않기 때문입니다.  
  
 SQL_ATTR_PARAM_OPERATION_PTR statement 특성에서 가리키는 배열을 사용 하 여 매개 변수 행을 무시할 수 있습니다. 배열의 요소가 SQL_PARAM_IGNORE로 설정 된 경우 해당 요소에 해당 하는 매개 변수 집합이 **Sqlexecute** 또는 **sqlexecdirect** 호출에서 제외 됩니다. SQL_ATTR_PARAM_OPERATION_PTR 특성이 가리키는 배열은 응용 프로그램에 의해 할당 되 고 채워지고 드라이버가 읽습니다. 인출 된 행을 입력 매개 변수로 사용 하는 경우 매개 변수 작업 배열에서 행 상태 배열의 값을 사용할 수 있습니다.  
  
## <a name="error-processing"></a>오류 처리  
 문을 실행 하는 동안 오류가 발생 하는 경우 실행 함수는 오류를 반환 하 고 행 번호 변수를 오류가 포함 된 행의 수로 설정 합니다. 오류 집합을 제외한 모든 행이 실행 되는지 여부 또는 오류 집합 앞에 있는 모든 행이 실행 되는지 여부에 관계 없이 데이터 원본에 해당 합니다. 매개 변수 집합을 처리 하기 때문에 드라이버는 SQL_ATTR_PARAMS_PROCESSED_PTR statement 특성으로 지정 된 버퍼를 현재 처리 중인 행의 수로 설정 합니다. 오류 집합을 제외한 모든 집합이 실행 되는 경우 드라이버는 모든 행이 처리 된 후이 버퍼를 SQL_ATTR_PARAMSET_SIZE 설정 합니다.  
  
 SQL_ATTR_PARAM_STATUS_PTR statement 특성이 설정 된 경우 **Sqlexecute** 또는 **sqlexecdirect** 는 각 매개 변수 집합의 상태를 제공 하는 *매개 변수 상태 배열을* 반환 합니다. 매개 변수 상태 배열은 응용 프로그램에 의해 할당 되 고 드라이버에서 채워집니다. 해당 요소는 매개 변수 행에 대해 SQL 문이 성공적으로 실행 되었는지 또는 매개 변수 집합을 처리 하는 동안 오류가 발생 했는지 여부를 나타냅니다. 오류가 발생 한 경우 드라이버는 매개 변수 상태 배열의 해당 값을 SQL_PARAM_ERROR 설정 하 고 SQL_SUCCESS_WITH_INFO를 반환 합니다. 응용 프로그램은 상태 배열을 확인 하 여 처리 된 행을 확인할 수 있습니다. 응용 프로그램은 행 번호를 사용 하 여 오류를 수정 하 고 처리를 다시 시작할 수 있습니다.  
  
 매개 변수 상태 배열을 사용 하는 방법은 **SQLGetInfo**호출에서 반환 되는 SQL_PARAM_ARRAY_ROW_COUNTS 및 SQL_PARAM_ARRAY_SELECTS 옵션에 의해 결정 됩니다. **INSERT**, **UPDATE**및 **DELETE** 문의 경우 SQL_PARC_BATCH이 SQL_PARAM_ARRAY_ROW_COUNTS에 대해 반환 되지만 SQL_PARC_NO_BATCH 반환 될 경우에는 상태 정보가 매개 변수 상태 배열에 채워집니다. **SELECT** 문의 경우에는 SQL_PARAM_ARRAY_SELECT에 대해 SQL_PAS_BATCH 반환 되지만 SQL_PAS_NO_BATCH 또는 SQL_PAS_NO_SELECT 반환 될 경우에는 매개 변수 상태 배열이 채워집니다.  
  
## <a name="data-at-execution-parameters"></a>실행 시 데이터 매개 변수  
 길이/지표 배열의 값이 SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC (*length*) 매크로의 결과인 경우 이러한 값에 대 한 데이터는 일반적인 방식으로 **sqlputdata** 를 사용 하 여 전송 됩니다. 이 프로세스의 다음과 같은 측면은 쉽게 알 수 없기 때문에 특별 한 주석입니다.  
  
-   드라이버가 SQL_NEED_DATA 반환 하는 경우 행 번호 변수의 주소를 데이터를 필요로 하는 행으로 설정 해야 합니다. 단일 값과 마찬가지로 응용 프로그램은 드라이버에서 단일 매개 변수 집합 내의 매개 변수 값을 요청 하는 순서에 대 한 가정을 만들 수 없습니다. 실행 시 데이터 매개 변수를 실행 하는 동안 오류가 발생 하는 경우 SQL_ATTR_PARAMS_PROCESSED_PTR statement 특성으로 지정 된 버퍼는 오류가 발생 한 행의 수로 설정 되 고, SQL_ATTR_PARAM_STATUS_PTR statement 특성에 의해 지정 된 행 상태 배열에서 행의 상태는 SQL_PARAM_ERROR로 설정 되 고, **Sqlexecute**, **sqlexecdirect**, **Sqlparamdata**또는 **sqlputdata** 에 대 한 호출은 SQL_ERROR을 반환 합니다. **Sqlexecute**, **Sqlexecdirect**또는 **sqlparamdata** 가 SQL_STILL_EXECUTING 반환 하는 경우이 버퍼의 내용은 정의 되지 않습니다.  
  
-   드라이버는 실행 시 데이터 매개 변수에 대해 **SQLBindParameter** 의 *Parametervalueptr* 인수 값을 해석 하지 않으므로 응용 프로그램이 배열에 대 한 포인터를 제공 하는 경우 **sqlparamdata** 는이 배열의 요소를 추출 하 여 응용 프로그램에 반환 하지 않습니다. 대신 응용 프로그램이 제공한 스칼라 값을 반환 합니다. 즉, **Sqlparamdata** 에서 반환 된 값이 응용 프로그램에서 데이터를 전송 하는 데 필요한 매개 변수를 지정 하는 데 충분 하지 않습니다. 또한 응용 프로그램은 현재 행 번호를 고려해 야 합니다.  
  
     매개 변수 배열의 요소만 실행 시 데이터 매개 변수인 경우 응용 프로그램은 모든 매개 변수에 대 한 요소를 포함 하는 *Parametervalueptr* 의 배열 주소를 전달 해야 합니다. 이 배열은 실행 시 데이터 매개 변수가 아닌 매개 변수에 대해 정상적으로 해석 됩니다. 실행 시 데이터 매개 변수의 경우 **Sqlparamdata** 가 응용 프로그램에 제공 하는 값 (일반적으로이 경우 드라이버에서 요청 하는 데이터를 식별 하는 데 사용 될 수 있음)은 항상 배열의 주소입니다.
