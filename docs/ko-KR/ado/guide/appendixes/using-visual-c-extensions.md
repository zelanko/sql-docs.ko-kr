---
title: Visual c + + 확장을 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cefa64e3677fa1d6c2660d288c59b4ffe79d4e9b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="visual-c-extensions"></a>Visual c + + 확장
## <a name="the-iadorecordbinding-interface"></a>IADORecordBinding 인터페이스
 Microsoft Visual c + + 확장의 ADO 연결 또는 바인딩 필드에 대해는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 C/c + + 변수입니다. 때마다 바인딩된의 현재 행 **레코드 집합** 변경에 대 한 모든 바인딩된 필드는 **레코드 집합** C/c + + 변수에 복사 됩니다. 필요에 따라 복사한 데이터는 C/c + + 변수의 선언 된 데이터 형식으로 변환 됩니다.

 **BindToRecordset** 의 메서드는 **IADORecordBinding** 인터페이스 C/c + + 변수를 필드에 바인딩합니다. **AddNew** 메서드 범위에 새 행 추가 **레코드 집합**합니다. **업데이트** 의 새 행의 필드를 채우려고 하는 메서드는 **레코드 집합**, C/c + + 변수 값을 가진 기존 행의 필드를 업데이트 하거나 합니다.

 **IADORecordBinding** 인터페이스에서 구현 됩니다는 **레코드 집합** 개체입니다. 수행 하지 구현 직접 코딩 합니다.

## <a name="binding-entries"></a>바인딩 항목
 ADO에 대 한 Visual c + + 확장의 필드를 매핑하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 C/c + + 변수입니다. 필드와 변수 간의 매핑 정의 이라고는 *항목 바인딩*합니다. 매크로 숫자, 고정 길이 및 가변 길이 데이터에 대 한 바인딩 항목을 제공 합니다. Visual c + + 확장명 클래스에서 파생 된 클래스에서 바인딩 항목 및 C/c + + 변수 선언 **CADORecordBinding**합니다. **CADORecordBinding** 클래스 바인딩 항목 매크로 통해 내부적으로 정의 됩니다.

 ADO를 OLE DB에 이러한 매크로의 매개 변수를 내부적으로 매핑합니다 **DBBINDING** 구조체이 고 OLE DB 만듭니다 **접근자** 이동 및 필드 및 변수도 간의 데이터 변환 관리 하는 개체입니다. 구성 되도록 데이터를 정의 하는 OLE DB의 세 부분: A *버퍼* 데이터가 저장 됩니다; 여기서는 *상태* 저장 버퍼를 하거나 변수를 복원 하는 하는 방법을 나타내는 필드입니다. 및 *길이* 데이터입니다. (참조 [보기 및 설정 데이터 (OLE DB)](http://msdn.microsoft.com/en-us/4369708b-c9fb-4d48-a321-bf949b41a369)자세한 정보에 대 한 OLE DB 프로그래머 참조 합니다.)

## <a name="header-file"></a>헤더 파일
 ADO에 대 한 Visual c + + 확장을 사용 하려면 응용 프로그램에서 다음 파일을 포함 합니다.

```
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>레코드 집합 필드 바인딩

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>C/c + + 변수를 레코드 집합 필드를 바인딩하려면

1.  파생 된 클래스를 만들기는 **CADORecordBinding** 클래스입니다.

2.  파생된 클래스에서 바인딩 항목 및 해당 C/c + + 변수를 지정 합니다. 대괄호 사이의 바인딩 항목 **BEGIN_ADO_BINDING** 및 **END_ADO_BINDING** 매크로입니다. 쉼표 또는 세미콜론으로 매크로 종료 하지 마세요. 적절 한 구분 기호는 각 매크로 의해 자동으로 지정 됩니다.

     C/c + + 변수 매핑될 수 있도록 각 필드에 대 한 바인딩 항목을 지정 합니다. 적절 한 멤버에서 사용 하 여는 **ADO_FIXED_LENGTH_ENTRY**, **ADO_NUMERIC_ENTRY**, 또는 **ADO_VARIABLE_LENGTH_ENTRY** 매크로의 제품군입니다.

3.  응용 프로그램에서 파생 된 클래스의 인스턴스를 만들고 **CADORecordBinding**합니다. 가져오기는 **IADORecordBinding** 에서 인터페이스는 **레코드 집합**합니다. 다음 호출에서 **BindToRecordset** 바인딩할 메서드는 **레코드 집합** 필드 C/c + + 변수를 합니다.

 자세한 내용은 참조는 [Visual c + + 확장 예제](../../../ado/guide/appendixes/visual-c-extensions-example.md)합니다.

## <a name="interface-methods"></a>인터페이스 메서드
 **IADORecordBinding** 인터페이스에는 세 가지 방법: **BindToRecordset**, **AddNew**, 및 **업데이트**합니다. 각 메서드의 유일한 인수는 포인터에서 파생 된 클래스의 인스턴스로 **CADORecordBinding**합니다. 따라서는 **AddNew** 및 **업데이트** 메서드 자신의 ADO 메서드 namesakes의 매개 변수를 지정할 수 없습니다.

## <a name="syntax"></a>구문
 **BindToRecordset** 메서드 associates는 **레코드 집합** C/c + + 변수를 사용 하는 필드가 있습니다.

```
BindToRecordset(CADORecordBinding *binding)
```

 **AddNew** 메서드 호출의 마다 ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 메서드는 새 행을 추가 하는 **레코드 집합**합니다.

```
AddNew(CADORecordBinding *binding)
```

 **업데이트** 메서드 호출의 마다 ADO [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 업데이트 하는 **레코드 집합**합니다.

```
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>바인딩 항목 매크로
 연결을 정의 하는 바인딩 항목 매크로 **레코드 집합** 필드와 변수입니다. 시작 및 끝 매크로 집합 바인딩 항목을 구분 합니다.

 매크로의 제품군 고정 길이 데이터의 경우와 같이 제공 **adDate** 또는 **adBoolean**; 숫자 데이터와 같은 **adTinyInt**, **adInteger**, 또는 **adDouble**; 및 가변 길이 데이터와 같은 **adChar**, **집합이 있으므로 필요** 또는 **adVarBinary**합니다. 모든 숫자 형식 제외 하 고 **adVarNumeric**, 고정 길이 형식 됩니다. 각 패밀리는 서로 다른 매개 변수 집합에 있으므로 관련 없는 바인딩 정보를 제외할 수 있습니다.

 자세한 내용은 참조 [부록 a: 데이터 형식](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6), OLE DB 프로그래머 참조 합니다.

### <a name="begin-binding-entries"></a>바인딩 항목 시작
 **BEGIN_ADO_BINDING**(*Class*)

### <a name="fixed-length-data"></a>고정 길이 데이터
 **ADO_FIXED_LENGTH_ENTRY**(*Ordinal, DataType, Buffer, Status, Modify*)

 **ADO_FIXED_LENGTH_ENTRY2**(*Ordinal, DataType, Buffer, Modify*)

### <a name="numeric-data"></a>숫자 데이터
 **ADO_NUMERIC_ENTRY**(*Ordinal, DataType, Buffer, Precision, Scale, Status, Modify*)

 **ADO_NUMERIC_ENTRY2**(*서 수, 데이터 형식, 버퍼, 정밀도, 배율, 수정*)

### <a name="variable-length-data"></a>가변 길이 데이터
 **ADO_VARIABLE_LENGTH_ENTRY**(*Ordinal, DataType, Buffer, Size, Status, Length, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*Ordinal, DataType, Buffer, Size, Status, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*Ordinal, DataType, Buffer, Size, Length, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*Ordinal, DataType, Buffer, Size, Modify*)

### <a name="end-binding-entries"></a>바인딩 항목 끝
 **END_ADO_BINDING**()

|매개 변수|Description|
|---------------|-----------------|
|*클래스*|바인딩 항목 및 C/c + + 변수는 정의 된 클래스입니다.|
|*Ordinal*|하나를 계산 하는 서 수는 **레코드 집합** C/c + + 변수에 해당 하는 필드입니다.|
|*DataType*|C/c + + 변수의 해당 ADO 데이터 형식 (참조 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 유효한 데이터 형식 목록에 대 한). 값은 **레코드 집합** 필드가 필요한 경우이 데이터 형식으로 변환 됩니다.|
|*Buffer*|C/c + + 변수 이름 여기서는 **레코드 집합** 필드 저장 됩니다.|
|*크기*|최대 크기의 바이트 *버퍼*합니다. 경우 *버퍼* 에 다양 한 길이의 문자열을 포함 종결 0에 대 한 공간을 허용 합니다.|
|*상태*|나타내는 변수의 이름입니다 여부의 내용을 *버퍼* 올바른지 여부와 필드를 변환 하는 과정 *DataType* 성공적으로 합니다.<br /><br /> 이 변수에 대 한 가장 중요 한 두 값이 **adFldOK**, 즉, 변환 작업이 성공적 및 **adFldNull**, VT_NULL 유형의 VARIANT 것 필드의 값 즉 및 뿐만 아니라 빈 합니다.<br /><br /> 가능한 값에 대 한 *상태* "상태 값" 합니다. 다음 표에 나열 된|
|*수정*|부울 플래그입니다. TRUE 이면 ADO 해당 업데이트 하도록 허용 된 **레코드 집합** 필드에 포함 된 값을 가진 *버퍼*합니다.<br /><br /> 부울 설정 *수정* 바인딩된 필드를 업데이트 하는 ADO를 사용 하도록 설정 하려면 TRUE이 고 FALSE 이면 필드를 검사 하지만 변경 되지 수 매개 변수입니다.|
|*정밀도*|숫자 변수로 나타낼 수 있는 자릿수의 수입니다.|
|*소수 자릿수*|소수 자릿수는 숫자 변수 수입니다.|
|*길이*|에 있는 데이터의 실제 길이 포함 하는 4 바이트 변수의 이름을 *버퍼*합니다.|

## <a name="status-values"></a>상태 값
 값은 *상태* 변수 필드 성공적으로 변수 복사 되는지 여부를 나타냅니다.

 데이터를 설정할 때 *상태* 로 설정할 수 있습니다 **adFldNull** 나타내려면는 **레코드 집합** 필드를 설정 해야 null로 합니다.

|상수|Value|Description|
|--------------|-----------|-----------------|
|**adFldOK**|0|Null이 아닌 필드 값이 반환 되었습니다.|
|**adFldBadAccessor**|1.|바인딩 올바르지 않습니다.|
|**adFldCantConvertValue**|2|부호 불일치 또는 데이터 오버플로가 아닌 다른 이유로 값을 변환할 수 없습니다.|
|**adFldNull**|3|필드를 가져올 때 null 값을 반환 되었음을 나타냅니다.<br /><br /> 필드를 설정할 때 표시로 필드를 설정 해야 **NULL** 필드 인코딩할 수 없는 경우 **NULL** 자체 (예를 들어 문자 배열 또는 정수).|
|**adFldTruncated**|4|가변 길이 데이터 또는 숫자로 이루어진 잘렸습니다.|
|**adFldSignMismatch**|5|값은 서명 되어 및 변수 데이터 형식은 부호가 없습니다.|
|**adFldDataOverFlow**|6|값은 데이터 형식에 저장할 수 있는 보다 큽니다.|
|**adFldCantCreate**|7|알 수 없는 열 유형 및 필드 이미 열려 있습니다.|
|**adFldUnavailable**|8|필드 값을 확인할 수 없습니다-기본값을 갖지 할당 되지 않은 새 필드에서 예를 들어 있습니다.|
|**adFldPermissionDenied**|9|업데이트, 데이터를 쓸 수 있는 권한이 없습니다.|
|**adFldIntegrityViolation**|10|를 업데이트할 때 필드 값은 열 무결성을 위반 합니다.|
|**adFldSchemaViolation**|11|를 업데이트할 때 필드 값은 열 스키마를 위반 합니다.|
|**adFldBadStatus**|12|잘못 된 상태 매개 변수를 업데이트 하는 경우.|
|**adFldDefault**|13|를 업데이트할 때 기본값이 사용 되었습니다.|

## <a name="see-also"></a>관련 항목:
 [Visual c + + 확장 예제](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual c + + 확장 헤더](../../../ado/guide/appendixes/visual-c-extensions-header.md)
