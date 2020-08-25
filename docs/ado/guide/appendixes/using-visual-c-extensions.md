---
description: Visual C++ 확장 사용
title: Visual C++ 확장 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
author: rothja
ms.author: jroth
ms.openlocfilehash: aa5ed351f150aa913a9a454f42bd11c9fcb7ac00
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806469"
---
# <a name="visual-c-extensions"></a>Visual C++ 확장
## <a name="the-iadorecordbinding-interface"></a>IADORecordBinding 인터페이스
 ADO 용 Microsoft Visual C++ 확장은 C/c + + 변수에 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체의 필드를 연결 하거나 바인딩합니다. 바인딩된 **레코드 집합** 의 현재 행이 변경 될 때마다 **레코드 집합** 의 바인딩된 모든 필드가 C/c + + 변수에 복사 됩니다. 필요한 경우 복사 된 데이터는 C/c + + 변수의 선언 된 데이터 형식으로 변환 됩니다.

 **IADORecordBinding** 인터페이스의 **BindToRecordset** 메서드는 필드를 C/c + + 변수에 바인딩합니다. **AddNew** 메서드는 바인딩된 **레코드 집합**에 새 행을 추가 합니다. **Update** 메서드는 **레코드 집합**의 새 행에 있는 필드를 채우거 나 C/c + + 변수 값을 사용 하 여 기존 행의 필드를 업데이트 합니다.

 **IADORecordBinding** 인터페이스는 **레코드 집합** 개체에 의해 구현 됩니다. 구현을 직접 코딩 하는 것은 아닙니다.

## <a name="binding-entries"></a>바인딩 항목
 ADO 용 Visual C++ 확장 프로그램은 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체의 필드를 C/c + + 변수에 매핑합니다. 필드와 변수 간의 매핑을 정의 하는 것을 *바인딩 항목*이라고 합니다. 매크로는 숫자, 고정 길이 및 가변 길이 데이터에 대 한 바인딩 항목을 제공 합니다. 바인딩 항목 및 C/c + + 변수는 Visual C++ 확장 클래스인 **CADORecordBinding**에서 파생 된 클래스에서 선언 됩니다. **CADORecordBinding** 클래스는 바인딩 항목 매크로에 의해 내부적으로 정의 됩니다.

 ADO는 내부적으로 이러한 매크로의 매개 변수를 OLE DB **DBBINDING** 구조에 매핑하고 OLE DB **접근자** 개체를 만들어 필드와 변수 간 데이터의 이동과 변환을 관리 합니다. OLE DB는 데이터를 저장 하는 *버퍼* 의 세 부분으로 구성 된 데이터를 정의 합니다. 필드가 버퍼에 성공적으로 저장 되었는지 여부 또는 필드에 변수를 복원 하는 방법을 나타내는 *상태* 입니다. 데이터의 *길이* 입니다. 자세한 내용은 OLE DB 프로그래머 참조에서 [데이터 가져오기 및 설정 (OLE DB)](/previous-versions/windows/desktop/ms713700(v=vs.85))을 참조 하세요.

## <a name="header-file"></a>헤더 파일
 ADO 용 Visual C++ 확장을 사용 하려면 응용 프로그램에 다음 파일을 포함 합니다.

```cpp
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>레코드 집합 필드 바인딩

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>C/c + + 변수에 레코드 집합 필드를 바인딩하려면

1.  **CADORecordBinding** 클래스에서 파생 된 클래스를 만듭니다.

2.  파생 클래스에서 바인딩 항목과 해당 C/c + + 변수를 지정 합니다. **BEGIN_ADO_BINDING** 와 **END_ADO_BINDING** 매크로 사이에 바인딩 항목을 묶습니다. 매크로를 쉼표나 세미콜론으로 종료 하지 마십시오. 각 매크로에서 적절 한 구분 기호를 자동으로 지정 합니다.

     C/c + + 변수에 매핑할 각 필드에 대해 하나의 바인딩 항목을 지정 합니다. **ADO_FIXED_LENGTH_ENTRY**, **ADO_NUMERIC_ENTRY**또는 **ADO_VARIABLE_LENGTH_ENTRY** 매크로 모음에서 적절 한 멤버를 사용 합니다.

3.  응용 프로그램에서 **CADORecordBinding**에서 파생 된 클래스의 인스턴스를 만듭니다. **레코드 집합**에서 **IADORecordBinding** 인터페이스를 가져옵니다. 그런 다음 **BindToRecordset** 메서드를 호출 하 여 **레코드 집합** 필드를 C/c + + 변수에 바인딩합니다.

 자세한 내용은 [Visual C++ 확장 예제](./visual-c-extensions-example.md)를 참조 하세요.

## <a name="interface-methods"></a>인터페이스 메서드
 **IADORecordBinding** 인터페이스에는 **BindToRecordset**, **AddNew**및 **Update**의 세 가지 메서드가 있습니다. 각 메서드에 대 한 유일한 인수는 **CADORecordBinding**에서 파생 된 클래스의 인스턴스에 대 한 포인터입니다. 따라서 **AddNew** 및 **UPDATE** 메서드는 ADO 메서드 namesakes의 매개 변수를 지정할 수 없습니다.

## <a name="syntax"></a>구문
 **BindToRecordset** 메서드는 C/c + + 변수와 **레코드 집합** 필드를 연결 합니다.

```cpp
BindToRecordset(CADORecordBinding *binding)
```

 **AddNew** 메서드는 해당 마다 ADO [AddNew](../../reference/ado-api/addnew-method-ado.md) 메서드를 호출 하 여 **레코드 집합**에 새 행을 추가 합니다.

```cpp
AddNew(CADORecordBinding *binding)
```

 **Update** 메서드는 ADO [업데이트](../../reference/ado-api/update-method.md) 메서드인 마다을 호출 하 여 **레코드 집합**을 업데이트 합니다.

```cpp
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>바인딩 항목 매크로
 바인딩 항목 매크로는 **레코드 집합** 필드와 변수를 연결 하는 것을 정의 합니다. 시작 및 종료 매크로는 바인딩 항목 집합을 구분 합니다.

 **Addate** 또는 **addate**과 같은 고정 길이 데이터에 대 한 매크로 패밀리가 제공 됩니다. **Adtinyint**, **Adtinyint**또는 **addououn**등의 숫자 데이터 **Adchar**, **adVarChar** 또는 **adVarBinary**와 같은 가변 길이 데이터 **AdVarNumeric**를 제외한 모든 숫자 형식은 고정 길이 형식 이기도 합니다. 각 패밀리에는 서로 다른 매개 변수 집합이 있으므로 관심 없는 바인딩 정보를 제외할 수 있습니다.

 자세한 내용은 OLE DB 프로그래머 참조의 [부록 a: 데이터 형식](/previous-versions/windows/desktop/ms723969(v=vs.85))을 참조 하세요.

### <a name="begin-binding-entries"></a>바인딩 항목 시작
 **BEGIN_ADO_BINDING**(*클래스*)

### <a name="fixed-length-data"></a>고정 길이 데이터
 **ADO_FIXED_LENGTH_ENTRY**(*서 수, 데이터 형식, 버퍼, 상태, 수정*)

 **ADO_FIXED_LENGTH_ENTRY2**(*서 수, 데이터 형식, 버퍼, 수정*)

### <a name="numeric-data"></a>숫자 데이터
 **ADO_NUMERIC_ENTRY**(*서 수, 데이터 형식, 버퍼, 전체 자릿수, 소수 자릿수, 상태, 수정*)

 **ADO_NUMERIC_ENTRY2**(*서 수, 데이터 형식, 버퍼, 전체 자릿수, 소수 자릿수, 수정*)

### <a name="variable-length-data"></a>가변 길이 데이터
 **ADO_VARIABLE_LENGTH_ENTRY**(*서 수, 데이터 형식, 버퍼, 크기, 상태, 길이, 수정*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*서 수, 데이터 형식, 버퍼, 크기, 상태, 수정*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*서 수, 데이터 형식, 버퍼, 크기, 길이, 수정*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*서 수, 데이터 형식, 버퍼, 크기, 수정*)

### <a name="end-binding-entries"></a>바인딩 항목 종료
 **END_ADO_BINDING**()

|매개 변수|설명|
|---------------|-----------------|
|*클래스*|바인딩 항목 및 C/c + + 변수가 정의 되는 클래스입니다.|
|*순서로*|C/c + + 변수에 해당 하는 **레코드 집합** 필드 중 하나에서 계산 하는 서 수입니다.|
|*DataType*|C/c + + 변수의 해당 ADO 데이터 형식입니다 (유효한 데이터 형식 목록은 [DataTypeEnum](../../reference/ado-api/datatypeenum.md) 참조). 필요한 경우 **레코드 집합** 필드의 값이이 데이터 형식으로 변환 됩니다.|
|*Buffer*|**레코드 집합** 필드가 저장 되는 c/c + + 변수의 이름입니다.|
|*크기*|*버퍼*의 최대 크기 (바이트)입니다. *버퍼가* 가변 길이 문자열을 포함 하는 경우 종료 0에 대해 공간을 허용 합니다.|
|*상태*|*버퍼* 의 내용이 올바른지 여부와 필드를 *데이터 형식* 으로 변환 하는 작업이 성공 했는지 여부를 나타내는 변수의 이름입니다.<br /><br /> 이 변수에 대 한 가장 중요 한 두 가지 값은 변환이 성공 했음을 의미 하는 **Adfldok**입니다. 및 **Adfldnull**은 필드의 값이 단순히 비어 있지 않고 VT_NULL 형식의 VARIANT 임을 의미 합니다.<br /><br /> *상태* 에 사용할 수 있는 값은 다음 테이블인 "상태 값"에 나열 되어 있습니다.|
|*수정*|부울 플래그입니다. TRUE 이면 ADO에서 해당 **레코드 집합** 필드를 *버퍼*에 포함 된 값으로 업데이트할 수 있음을 나타냅니다.<br /><br /> 부울 *modify* 매개 변수를 TRUE로 설정 하 여 ADO에서 바인딩된 필드를 업데이트할 수 있게 하 고, 필드를 검사 하지만 변경 하지 않으려면 FALSE로 설정 합니다.|
|*정밀도*|숫자 변수로 나타낼 수 있는 자릿수입니다.|
|*크기 조정*|숫자 변수의 소수 자릿수입니다.|
|*길이*|*버퍼*에 있는 데이터의 실제 길이를 포함 하는 4 바이트 변수의 이름입니다.|

## <a name="status-values"></a>상태 값
 *상태* 변수의 값은 필드가 변수에 성공적으로 복사 되었는지 여부를 나타냅니다.

 데이터를 설정할 때 *상태* 를 **Adfldnull** 로 설정 하 여 **레코드 집합** 필드를 null로 설정 해야 함을 나타낼 수 있습니다.

|상수|값|설명|
|--------------|-----------|-----------------|
|**adFldOK**|0|Null이 아닌 필드 값이 반환 되었습니다.|
|**adFldBadAccessor**|1|바인딩이 잘못 되었습니다.|
|**adFldCantConvertValue**|2|부호 불일치 또는 데이터 오버플로 이외의 이유로 인해 값을 변환할 수 없습니다.|
|**adFldNull**|3|필드를 가져오는 경우 null 값이 반환 되었음을 나타냅니다.<br /><br /> 필드를 설정 하는 경우 필드에서 **null** 을 인코딩할 수 없는 경우 (예: 문자 배열 또는 정수) 필드를 **null** 로 설정 해야 함을 나타냅니다.|
|**adFldTruncated**|4|가변 길이 데이터 또는 숫자가 잘렸습니다.|
|**adFldSignMismatch**|5|값은 signed 이며 변수 데이터 형식은 부호가 없습니다.|
|**adFldDataOverFlow**|6|값이 변수 데이터 형식에 저장 될 수 있는 값 보다 큽니다.|
|**adFldCantCreate**|7|알 수 없는 열 유형 및 필드가 이미 열려 있습니다.|
|**adFldUnavailable 수 없음**|8|필드 값을 확인할 수 없습니다. 예를 들어 기본값 없이 새로 할당 되지 않은 필드를 지정 합니다.|
|**Adfld이상 거부 됨**|9|업데이트할 때 데이터를 쓸 수 있는 권한이 없습니다.|
|**adFldIntegrityViolation**|10|업데이트할 때 필드 값이 열 무결성을 위반 합니다.|
|**adFldSchemaViolation**|11|업데이트할 때 필드 값이 열 스키마를 위반 합니다.|
|**adFldBadStatus**|12|업데이트할 때 상태 매개 변수가 잘못 되었습니다.|
|**adFldDefault**|13|업데이트 시 기본값이 사용 되었습니다.|

## <a name="see-also"></a>참고 항목
 [Visual C++ 확장 예제](./visual-c-extensions-example.md) [Visual C++ extensions 헤더](./visual-c-extensions-header.md)