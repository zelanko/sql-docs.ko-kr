---
title: 시각적 개체를 사용 하 여 C++ 확장 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f89b08d968b5f601c37f89b15196d6ef03db434
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702908"
---
# <a name="visual-c-extensions"></a>Visual C++ 확장
## <a name="the-iadorecordbinding-interface"></a>IADORecordBinding 인터페이스
 Microsoft Visual C++ 의 ADO 연결 또는 바인딩 필드에 대 한 확장을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 c /C++ 변수입니다. 때마다 바인딩된의 현재 행 **레코드 집합** 바인딩된 모든 필드를 변경 합니다 **레코드 집합** C에 복사 됩니다 /C++ 변수입니다. 필요한 경우 C의 선언 된 데이터 형식으로 복사 된 데이터를 변환는 /C++ 변수입니다.

 **BindToRecordset** 메서드는 **IADORecordBinding** 인터페이스 C 바인딩할 필드 /C++ 변수입니다. 합니다 **AddNew** 바인딩된에 새 행을 추가 하는 메서드 **Recordset**합니다. **업데이트** 메서드는 새 행의 필드를 채우려고 합니다 **레코드 집합**, C의 값을 사용 하 여 기존 행의 필드를 업데이트 하거나 /C++ 변수입니다.

 합니다 **IADORecordBinding** 가 인터페이스를 구현 합니다 **레코드 집합** 개체입니다. 코딩 하지 구현을 직접.

## <a name="binding-entries"></a>바인딩 항목
 시각적 개체 C++ ADO에 대 한 확장의 필드를 매핑하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 c /C++ 변수입니다. 필드 및 변수 간의 매핑 정의 라고는 *항목을 바인딩*합니다. 매크로 숫자, 고정 길이 및 가변 길이 데이터에 대 한 바인딩 항목을 제공합니다. 바인딩 항목과 C /C++ 시각적 개체에서 파생 된 클래스에서 선언 된 변수는 C++ 확장 클래스 **CADORecordBinding**합니다. 합니다 **CADORecordBinding** 클래스 바인딩 항목 매크로 통해 내부적으로 정의 됩니다.

 ADO OLE DB에 내부적으로 이러한 매크로의 매개 변수를 매핑합니다 **DBBINDING** OLE DB를 만들고 구조체 **접근자** 이동 및 변환 필드 및 변수 간에 데이터를 관리 하는 개체입니다. 구성 데이터를 정의 하는 OLE DB의 세 부분으로 구성 합니다. A *버퍼* 데이터가 저장 됩니다; 여기서는 *상태* 여부를 필드에에서 저장 되었습니다. 버퍼 또는 변수의; 필드를 복원 해야 하는 방법을 나타내는 및 *길이* 데이터. (참조 [가져오기 및 설정 데이터 (OLE DB)](https://msdn.microsoft.com/4369708b-c9fb-4d48-a321-bf949b41a369)자세한 정보에 대 한 OLE DB 프로그래머 참조.)

## <a name="header-file"></a>헤더 파일
 시각적 개체를 사용 하기 위해 응용 프로그램에 다음 파일을 포함할 C++ ADO에 대 한 확장:

```cpp
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>레코드 집합 필드 바인딩

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>레코드 집합 필드를 C 바인딩할 /C++ 변수

1.  파생 된 클래스를 만듭니다는 **CADORecordBinding** 클래스입니다.

2.  바인딩 항목 및 해당 C 지정 /C++ 파생된 클래스에서 변수입니다. 사이의 바인딩 항목을 대괄호 **BEGIN_ADO_BINDING** 하 고 **END_ADO_BINDING** 매크로입니다. 쉼표 또는 세미콜론을 사용 하 여 매크로 종료 하지 마세요. 적절 한 구분 기호는 각 매크로 의해 자동으로 지정 됩니다.

     C에 매핑할 각 필드에 대 한 바인딩 항목을 하나씩 지정 /C++ 변수입니다. 적절 한 멤버를 사용 하 여는 **ADO_FIXED_LENGTH_ENTRY**를 **ADO_NUMERIC_ENTRY**, 또는 **ADO_VARIABLE_LENGTH_ENTRY** 매크로 제품군입니다.

3.  응용 프로그램에서 파생 된 클래스의 인스턴스를 만듭니다 **CADORecordBinding**합니다. 가져오기의 **IADORecordBinding** 에서 인터페이스를 **레코드 집합**합니다. 다음 호출을 **BindToRecordset** 바인딩할 메서드는 **레코드 집합** c 필드 /C++ 변수.

 자세한 내용은 참조 하세요. 합니다 [시각적 C++ 확장 예제](../../../ado/guide/appendixes/visual-c-extensions-example.md)합니다.

## <a name="interface-methods"></a>인터페이스 메서드
 합니다 **IADORecordBinding** 인터페이스에 세 가지 방법이 있습니다. **BindToRecordset**하십시오 **AddNew**, 및 **업데이트**합니다. 각 방법의 유일한 인수는에서 파생 된 클래스의 인스턴스에 대 한 포인터 **CADORecordBinding**합니다. 따라서 합니다 **AddNew** 하 고 **업데이트** 메서드는 ADO 메서드 namesakes의 매개 변수를 지정할 수 없습니다.

## <a name="syntax"></a>구문
 **BindToRecordset** 메서드에 연결 합니다 **레코드 집합** C 사용 하 여 필드 /C++ 변수입니다.

```cpp
BindToRecordset(CADORecordBinding *binding)
```

 **AddNew** 메서드 호출의 마다 ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 메서드를 새 행을 추가 하는 **레코드 집합**합니다.

```cpp
AddNew(CADORecordBinding *binding)
```

 **업데이트** 메서드 호출의 마다 ADO [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 업데이트 하는 **레코드 집합**합니다.

```cpp
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>바인딩 항목 매크로
 연결을 정의 하는 바인딩 항목 매크로 **레코드 집합** 필드와 변수입니다. 시작 및 종료 매크로 바인딩 항목의 집합을 구분 합니다.

 매크로의 제품군과 같은 고정 길이 데이터에 대 한 제공 됩니다 **adDate** 하거나 **adBoolean**; 숫자 데이터와 같은 **adTinyInt**, **adInteger**, 또는 **adDouble**; 및 가변 길이 데이터와 같은 **adChar**를 **집합이 있으므로 필요** 또는 **adVarBinary**합니다. 모든 숫자 형식, 제외한 **adVarNumeric**, 고정 길이 형식 이기도 합니다. 각 제품군 서로 다른 매개 변수 집합에 있으므로 관련 없는 바인딩 정보를 제외할 수 있습니다.

 자세한 내용은 참조 하세요. [부록 a: 데이터 형식](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6), OLE DB 프로그래머 참조입니다.

### <a name="begin-binding-entries"></a>바인딩 항목 시작
 **BEGIN_ADO_BINDING**(*Class*)

### <a name="fixed-length-data"></a>고정 길이 데이터
 **ADO_FIXED_LENGTH_ENTRY**(*Ordinal, DataType, Buffer, Status, Modify*)

 **ADO_FIXED_LENGTH_ENTRY2**(*Ordinal, DataType, Buffer, Modify*)

### <a name="numeric-data"></a>숫자 데이터
 **ADO_NUMERIC_ENTRY**(*Ordinal, DataType, Buffer, Precision, Scale, Status, Modify*)

 **ADO_NUMERIC_ENTRY2**(*서, DataType, 버퍼, 정밀도, 배율, 수정*)

### <a name="variable-length-data"></a>가변 길이 데이터
 **ADO_VARIABLE_LENGTH_ENTRY**(*Ordinal, DataType, Buffer, Size, Status, Length, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*Ordinal, DataType, Buffer, Size, Status, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*Ordinal, DataType, Buffer, Size, Length, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*Ordinal, DataType, Buffer, Size, Modify*)

### <a name="end-binding-entries"></a>바인딩 항목 끝
 **END_ADO_BINDING**()

|매개 변수|Description|
|---------------|-----------------|
|*클래스*|클래스는 바인딩 항목과 C /C++ 변수 정의 됩니다.|
|*Ordinal*|하나에서 계산 되는 서 수를 **레코드 집합** 필드에 해당 하 여 C /C++ 변수.|
|*DataType*|C의 해당 하는 ADO 데이터 형식 /C++ 변수 (참조 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 유효한 데이터 형식 목록에 대 한). 값을 **레코드 집합** 필드 필요한 경우이 데이터 형식으로 변환 됩니다.|
|*Buffer*|C의 이름 /C++ 변수 위치는 **레코드 집합** 필드가 저장 됩니다.|
|*크기*|최대 크기 (바이트)입니다 *버퍼*합니다. 하는 경우 *버퍼* 에 가변 길이 문자열을 포함 종료 0에 대 한 공간을 허용 합니다.|
|*상태*|나타내는 변수의 이름입니다 여부를 내용의 *버퍼* 올바른지 여부에 관계 없이 필드를 변환 하는 *DataType* 성공 했습니다.<br /><br /> 이 변수에 대 한 가장 중요 한 두 값이 **adFldOK**, 즉, 변환 작업이 성공적 및 **adFldNull**, VT_NULL 형식의 VARIANT 필드의 값을 의미 하는 것 뿐만 아니라 및 비어 있습니다.<br /><br /> 가능한 값 *상태* "상태 값입니다." 다음 표에 나열 되어 있습니다|
|*수정*|부울 플래그입니다. TRUE 이면 ADO 해당 업데이트를 허용 됨을 나타냅니다 **Recordset** 포함 된 값을 사용 하 여 필드 *버퍼*합니다.<br /><br /> 설정할 부울 *수정* 바인딩된 필드를 업데이트 하는 ADO를 사용 하도록 설정 하려면 TRUE이 고 필드를 검사 하지만 변경 하지 않으려면 FALSE 매개 변수입니다.|
|*전체 자릿수*|숫자 변수를 나타낼 수 있는 자릿수의 수입니다.|
|*소수 자릿수*|숫자 변수에 대 한 소수 자릿수의 수입니다.|
|*길이*|에 있는 데이터의 실제 길이 포함 하는 4 바이트 변수의 이름을 *버퍼*합니다.|

## <a name="status-values"></a>상태 값
 값을 *상태* 변수 필드 변수에 성공적으로 복사 하는지 여부를 나타냅니다.

 데이터를 설정 하는 경우 *상태* 로 설정할 수 있습니다 **adFldNull** 나타내려면 합니다 **레코드 집합** 필드를 설정 해야 null로 합니다.

|상수|값|Description|
|--------------|-----------|-----------------|
|**adFldOK**|0|Null이 아닌 필드 값을 반환 했습니다.|
|**adFldBadAccessor**|1|바인딩이 잘못 되었습니다.|
|**adFldCantConvertValue**|2|부호 불일치 또는 데이터 오버플로가 아닌 다른 이유로 값을 변환할 수 없습니다.|
|**adFldNull**|3|필드를 가져올 때 null 값을 반환 되었음을 나타냅니다.<br /><br /> 필드에 설정할 필드를 설정할 때 나타냅니다 **NULL** 필드를 인코딩할 수 없는 경우 **NULL** 자체 (예: 문자 배열 또는 정수).|
|**adFldTruncated**|4|가변 길이 데이터 또는 숫자 잘렸습니다.|
|**adFldSignMismatch**|5|값은 로그인 및 변수 데이터 형식은 부호가 없습니다.|
|**adFldDataOverFlow**|6|값이 변수 데이터 형식에 저장할 수 있습니다 보다 큽니다.|
|**adFldCantCreate**|7|알 수 없는 열 형식 및 필드가 이미 열려 있습니다.|
|**adFldUnavailable**|8|필드 값에 결정-예를 들어, 기본값이 사용 하 여 새 할당 되지 않은 필드를 사용할 수 없습니다.|
|**adFldPermissionDenied**|9|업데이트, 데이터를 쓸 수 있는 권한이 없습니다.|
|**adFldIntegrityViolation**|10|를 업데이트할 때 필드 값을 열 무결성을 위반 합니다.|
|**adFldSchemaViolation**|11|를 업데이트할 때 필드 값을 열 스키마를 위반 합니다.|
|**adFldBadStatus**|12|잘못 된 상태 매개 변수를 업데이트할 때.|
|**adFldDefault**|13|를 업데이트할 때 기본값이 사용 되었습니다.|

## <a name="see-also"></a>관련 항목
 [Visual C++ 확장 예제](../../../ado/guide/appendixes/visual-c-extensions-example.md) [시각적 C++ 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)
