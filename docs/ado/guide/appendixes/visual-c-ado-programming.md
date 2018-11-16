---
title: Visual c + + ADO 프로그래밍 | Microsoft Docs
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
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 713d471d350877a207b49a9649db0b7262273f52
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350377"
---
# <a name="visual-c-ado-programming"></a>Visual C++ ADO 프로그래밍
ADO API 참조는 ADO API (응용 프로그래밍 인터페이스)을 Microsoft Visual Basic과 유사한 구문을 사용 하 여의 기능을 설명 합니다. 독자는 모든 사용자, ADO 프로그래머에 게 Visual Basic, Visual c + +와 같은 다양 한 언어를 사용 하는 (하거나 사용 하지 않고 합니다 **#import** 지시문), 및 Visual J++ (사용 하 여 ADO/WFC 클래스 패키지).  

> [!NOTE]
> 2004 년에 Microsoft에 지원을 Visual J++에 대 한 종료 되었습니다.

 이 다양성 수용 하기 위해 합니다 [Visual c + + 구문 인덱스에 대 한 ADO](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) 기능, 매개 변수, 예외 동작 및 API에서 일반적인 설명에 대 한 링크를 사용 하 여 Visual c + + 언어 관련 구문을 제공 참조입니다.  
  
 ADO는 COM (구성 요소 개체 모델) 인터페이스를 사용 하 여 구현 됩니다. 그러나 다른 항목 보다 특정 프로그래밍 언어로 COM을 사용 하는 프로그래머를 위한 쉽습니다. 예를 들어, COM을 사용 하 여 거의 모든 세부 정보는 암시적으로 처리 Visual Basic 프로그래머를 위한 Visual c + + 프로그래머에 게 해당 정보 자체에 참석 해야 하는 반면.  
  
 다음 섹션에서는 ADO를 사용 하는 C 및 c + + 프로그래머에 대 한 세부 정보를 요약 및 **#import** 지시문입니다. COM에 특정 데이터 형식에 중점을 둡니다 (**Variant**를 **BSTR**, 및 **SafeArray**), 및 오류 처리 (_com_error).  
  
## <a name="using-the-import-compiler-directive"></a>#Import 컴파일러 지시문을 사용 하 여  
 합니다 **#import** Visual c + + 컴파일러 지시문 ADO 메서드 및 속성을 사용 하 여 작업을 간소화 합니다. 지시문 (Msado15.dll) ADO.dll 등 형식 라이브러리를 포함 하는 파일의 이름을 사용 하 고 typedef 선언, 인터페이스 및 열거 상수에 대 한 스마트 포인터를 포함 하는 헤더 파일을 생성 합니다. 각 인터페이스 캡슐화 되었거나 클래스에서 래핑되어 있습니다.  
  
 클래스 (즉, 메서드 또는 속성이 호출) 내에서 각 작업에는 해당 작업을 직접 (즉, "원시" 형식으로 작업)를 호출 하는 선언 및 원시 작업을 호출 하 고 작업 succ를 실행 하지 못한 경우 COM 오류를 throw 하는 선언 essfully 합니다. 작업 속성 인 경우 일반적으로 Visual Basic과 같은 구문이 있는 작업에 대 한 대체 구문을 만드는 컴파일러 지시문을 합니다.  
  
 속성의 값을 검색 하는 작업 이름이 양식의 **가져오기 * * * 속성*합니다. 속성의 값을 설정 하는 작업 이름이 양식의 **배치 * * * 속성*합니다. ADO 개체에 대 한 포인터를 사용 하 여 속성의 값을 설정 하는 작업 이름이 양식의 **PutRef * * * 속성*합니다.  
  
 이러한 형식으로 호출 하 여 속성을 설정 또는 얻을 수 있습니다.  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>속성 지시문을 사용 하 여  
 **__declspec**  컴파일러 지시문이는 대체 구문 할 속성으로 사용 되는 함수를 선언 하는 Microsoft 전용 C 언어 확장입니다. 결과적으로 설정 하거나 Visual Basic에서와 비슷한 방식으로 속성의 값을 얻을 수 있습니다. 예를 들어, 설정 하 고 이러한 방식으로 속성을 가져올 수 있습니다.  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 코드에 없는 알림:  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 컴파일러는 적절 한 생성 **Get * * *-* 를 **배치**-, 또는 **PutRef * * * 속성* 호출 되는 대체 구문을 선언 및 속성 인지에 따라 읽거나 작성 합니다.  
  
 **__declspec**  컴파일러 지시문만 선언할 수 있습니다 **가져올**, **배치**, 또는 **가져오기** 및 **배치** 함수에 대 한 대체 구문. 읽기 전용 작업 하나만 **가져올** 선언; 하나만 쓰기 전용 작업을 **배치** 선언; 작업은 둘 다 읽고 쓰는 둘 다 **가져오기** 및 **배치** 선언 합니다.  
  
 이 지시문;를 사용 하 여 가능한 두 선언만 그러나 각 속성 구문이 있을: **가져오기 * * * 속성*, **배치 * * * 속성*, 및 **PutRef * * * 속성*합니다. 이 경우 두 형식에만 속성의 대체 구문을 사용 해야 합니다.  
  
 예를 들어 합니다 **명령** 개체 **ActiveConnection** 속성에 대 한 대체 구문을 사용 하 여 선언 된 **가져오기 * * * ActiveConnection* 및 **PutRef * * * ActiveConnection*합니다. **PutRef**-구문은 적합 하기 때문에 실제로 일반적으로 개방적이 고 배치 **연결** 개체 (즉, 한 **연결** 개체 포인터)이 속성입니다. 다른 한편으로 **레코드 집합** 개체에 **가져오기**-를 **Put**-, 및 **PutRef * * * ActiveConnection* 작업 하지만 다른 대안이 구문입니다.  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>컬렉션, GetItem 메서드 및 항목 속성  
 ADO 여러 컬렉션을 포함 하 여 정의 **필드**, **매개 변수**합니다 **속성**, 및 **오류**합니다. Visual c + +에서는 합니다 **GetItem (***인덱스***)** 메서드 컬렉션의 멤버를 반환 합니다. *인덱스* 은 **Variant**, 값은 컬렉션에서 멤버의 숫자 인덱스 또는 멤버의 이름을 포함 하는 문자열입니다.  
  
 **__declspec**  컴파일러 지시문을 선언 합니다 **항목** 각 컬렉션에는 대체 구문으로 속성의 기본적인 **GetItem()** 메서드. 대체 구문 대괄호를 사용 하 고 배열 참조와 비슷합니다. 일반적으로 두 가지 형태는 다음과 같습니다.  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 예를 들어, 필드에 값을 할당을 **레코드 집합** 라는 개체 ***rs***에서 파생 된 합니다 **작성자** 목차를 **pubs** 데이터베이스입니다. 사용 된 **Item()** 세 번째 액세스할 속성을 **필드** 의 **레코드 집합** 개체 **필드** 컬렉션 (컬렉션에서 인덱스가 만들어집니다 0입니다. 세 번째 필드는 가정 ***au_fname***). 호출을 **value ()** 메서드는 **필드** 문자열 값을 할당 하는 개체입니다.  
  
 이 표현 될 수 있습니다 Visual Basic의 다음 네 가지 방법 (마지막으로 두 가지 양식은 Visual Basic에 고유한; 다른 언어에 해당 하는 없는):  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 위의 처음 두 형식이 Visual c + +에서와 동등한 다음과 같습니다.  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 -또는-(에 대 한 대체 구문을 합니다 **값** 속성 표시 됨)  
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 에서 컬렉션을 반복 하는 예 "ADO 참조"의 "ADO 컬렉션" 섹션을 참조 합니다.  
  
## <a name="com-specific-data-types"></a>COM 별 데이터 형식  
 일반적으로 모든 Visual Basic 데이터 ADO API 참조에서 찾기 형식은 Visual c + +와 동일 합니다. 와 같은 표준 데이터 형식을 사용 다음과 **unsigned char** Visual basic **바이트**에 **짧은** 에 대 한 **정수**, 및  **긴** 에 대 한 **긴**합니다. 구문 Indexesto 찾는 위치 기능을 보러 정확 하 게 지정 된 메서드 또는 속성의 피연산자가 필요 합니다.  
  
 이 규칙에 대 한 예외는 COM에 특정 데이터 형식: **Variant**하십시오 **BSTR**, 및 **SafeArray**합니다.  
  
### <a name="variant"></a>Variant  
 A **Variant** 값 멤버 및 데이터 형식 멤버를 포함 하는 구조화 된 데이터 형식입니다. A **Variant** 다양 한 범위의 다른 변형, BSTR, 부울, IDispatch 또는 IUnknown 포인터, 통화, 날짜 및 등을 비롯 한 다른 데이터 형식에 포함 될 수 있습니다. COM은 메서드를 쉽게 다른 데이터 형식 변환도 제공 합니다.  
  
 합니다 **_variant_t** 캡슐화 하 고 관리 하는 클래스는 **Variant** 데이터 형식입니다.  
  
 ADO API 참조 라는 메서드 또는 속성 피연산자 값을 사용 하는 경우 일반적으로 의미에서 값의 전달 된 **_variant_t**합니다.  
  
 이 규칙은 명시적으로 true 합니다 **매개 변수** ADO API 참조 항목의 섹션 라는 피연산자는 **Variant**합니다. 설명서 명시 피연산자와 같은 표준 데이터 형식을 사용 하는 경우는 예외입니다 **긴** 하거나 **바이트**, 또는 열거형입니다. 다른 예외는 피연산자를 사용 하는 경우는 **문자열**합니다.  
  
### <a name="bstr"></a>BSTR  
 A **BSTR** (**B**이 있습니다 **STR**ing) 문자열 및 문자열의 길이 포함 하는 구조화 된 데이터 형식입니다. 할당, 조작 및 가능한 메서드를 제공 하는 COM을 **BSTR**합니다.  
  
 합니다 **_bstr_t** 캡슐화 하 고 관리 하는 클래스는 **BSTR** 데이터 형식입니다.  
  
 ADO API 참조는 메서드 또는 속성을 표시 하는 경우는 **문자열** 값, 즉 값의 형태로를 **_bstr_t**.  
  
### <a name="casting-variantt-and-bstrt-classes"></a>캐스팅 _variant_t 및 _bstr_t 클래스  
 명시적으로 코드에 필요한 경우가 **_variant_t** 또는 **_bstr_t** 인수에 작업입니다. 경우는 **_variant_t** 또는 **_bstr_t** 클래스에 생성자 인수 데이터 형식과 일치 하는, 컴파일러는 적절 한 생성 **_variant_t** 또는 **_bstr_t**합니다.  
  
 그러나 인수 모호한 경우 즉, 인수의 데이터 형식이 일치 둘 이상의 생성자에 인수가 올바른 생성자를 호출 하려면 적절 한 데이터 형식으로 캐스팅 해야 합니다.  
  
 예를 들어 선언 된 **Recordset::Open** 메서드는:  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 합니다 `ActiveConnection` 인수에 대 한 참조에는 **_variant_t**, 개방적이 고에 대 한 포인터 또는 연결 문자열을 코딩할 수 있는 **연결** 개체입니다.  
  
 올바른 **_variant_t** 와 같은 문자열을 전달 하는 경우 암시적으로 생성 될 "`DSN=pubs;uid=MyUserName;pwd=MyPassword;`", 또는와 같은 포인터 "`(IDispatch *) pConn`"입니다.  
  
> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 하거나 **Integrated Security = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.  
  
 명시적으로 코딩할 수 있습니다 또는 한 **_variant_t** 와 같은 포인터를 포함 하 "`_variant_t((IDispatch *) pConn, true)`". 캐스트를 `(IDispatch *)`, IUnknown 인터페이스 포인터를 사용 하는 다른 생성자를 사용 하 여 모호성을 해결 합니다.  
  
 ADO IDispatch 인터페이스는 실제로 거의 언급 하지만 것 중요 합니다. 때마다 변수로 ADO 개체에 대 한 포인터를 전달 되어야 합니다는 **Variant**, 해당 포인터는 IDispatch 인터페이스에 대 한 포인터로 캐스팅 해야 합니다.  
  
 선택적 기본 값을 사용 하 여 생성자의 두 번째 부울 인수를 명시적으로 코딩 하는 마지막 경우 `true`합니다. 이 인수를 사용 하면 합니다 **Variant** 호출할 생성자를 해당 **AddRef**() 메서드를 자동으로 호출 하는 ADO에 대 한 보정을 **_variant_t::Release**() 메서드 ADO 메서드 또는 속성을 호출 하는 경우 완료 됩니다.  
  
### <a name="safearray"></a>SafeArray  
 A **SafeArray** 다른 데이터 형식의 배열을 포함 하는 구조화 된 데이터 형식입니다. A **SafeArray** 이라고 *안전 하 게* 각 배열 차원의 하 한 범위에 대 한 정보를 포함 하며 해당 범위 내에서 배열 요소에 대 한 액세스를 제한 하기 때문에 있습니다.  
  
 경우 ADO API 참조 라는 메서드 또는 속성은 배열을 반환 합니다, 즉, 메서드 또는 속성을 사용 하거나 반환 된 **SafeArray**, 네이티브 C/c + + 배열이 아닌 합니다.  
  
 예를 들어, 두 번째 매개 변수를 **연결** 개체 **OpenSchema** 메서드를 사용 하려면 배열을 **Variant** 값입니다. 이러한 **Variant** 값의 요소로 전달 되어야 합니다는 **SafeArray**, 및 **SafeArray** 다른 값으로 설정 해야 합니다 **Variant** . 다른 **Variant** 의 두 번째 인수로 전달 되는 **OpenSchema**합니다.  
  
 대로 예의 첫 번째 인수를 **찾을** 메서드를 **Variant** 값인 1 차원 **SafeArray**각 선택적 첫 번째와 두 번째 인수는 **AddNew** 는 1 차원 **SafeArray**;의 반환 값과는 **GetRows** 메서드를 **Variant** 입니다 값은 2 차원 **SafeArray**합니다.  
  
## <a name="missing-and-default-parameters"></a>누락 및 기본 매개 변수  
 Visual Basic에서는 메서드에 매개 변수가 없습니다. 예를 들어 합니다 **레코드 집합** 개체 **오픈** 메서드에 5 개의 매개 변수가 있지만 중간 매개 변수를 건너뛰고 후행 매개 변수를 생략할 수 있습니다. 기본값 **BSTR** 하거나 **Variant** 누락 피연산자의 데이터 형식에 따라 대체 됩니다.  
  
 C/c + +에서는 모든 피연산자를 지정 해야 합니다. 데이터 형식이 문자열인 누락 된 매개 변수를 지정 하려는 경우, 지정 된 **_bstr_t** null 문자열을 포함 하 합니다. 데이터 형식은 해당 누락 된 매개 변수를 지정 하려는 경우는 **Variant**, 지정는 **_variant_t** DISP_E_PARAMNOTFOUND 및 VT_ERROR 유형의 값을 사용 하 여 합니다. 또는 해당을 지정할 **_variant_t** 상수를 **vtMissing**에서 제공 하는 합니다 **#import** 지시문입니다.  
  
 세 가지 메서드는 예외를 사용 하는 일반적인 **vtMissing**합니다. 이들은 합니다 **Execute** 의 메서드는 **연결** 및 **명령** 개체 및 **NextRecordset** 메서드의 합니다 **레코드 집합** 개체입니다. 다음은 해당 서명이입니다.  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 매개 변수를 *RecordsAffected* 하 고 *매개 변수*에 대 한 포인터를 **Variant**합니다. *매개 변수* 의 주소를 지정 하는 입력 매개 변수를 **Variant** 하나만 포함 된 매개 변수 또는 매개 변수는 실행 중인 명령을 수정 하는 배열입니다. *RecordsAffected* 의 주소를 지정 하는 출력 매개 변수를 **Variant**여기서 메서드에 의해 영향을 받는 행 수가 반환 됩니다.  
  
 에 **명령** 개체 **Execute** 메서드를 설정 하 여 지정 된 매개 변수가 없습니다 나타냅니다 *매개 변수* 를 `&vtMissing` (권장 되는) 또는 null 포인터 (즉, **NULL** 또는 영 (0)). 하는 경우 *매개 변수* 설정 되어 null 포인터를 메서드 내부적으로 대체 하는 것과 같습니다 **vtMissing**, 다음 작업을 완료 합니다.  
  
 모든 메서드에 영향을 받은 레코드 수를 설정 하 여 하지 반환 되어야 함을 나타낼 *RecordsAffected* null 포인터에 대 한 합니다. 이 경우 null 포인터 많은 누락 된 매개 변수가 아닙니다 확인 하기 위해 메서드가 영향을 받은 레코드 수를 무시 해야 합니다.  
  
 따라서 이러한 세 가지 방법에 대 한와 같은 코딩 하는 것이 유효 합니다.  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>오류 처리  
 Com에서 대부분의 작업 함수를 성공적으로 완료 되었는지 여부를 나타내는 HRESULT 반환 코드를 반환 합니다. 합니다 **#import** 지시문 각 "원시" 메서드 또는 속성 래퍼 코드를 생성 하 고 반환된 된 HRESULT를 확인 합니다. HRESULT 오류를 나타냅니다 래퍼 코드는 인수로 서 COM 오류를 HRESULT 반환 코드를 사용 하 여 호출 _com_issue_errorex()에서 throw 합니다. COM 오류 개체를 낼 수 있습니다는 **시도**-**catch** 블록입니다. (효율성의 위해서 catch에 대 한 참조를 **_com_error** 개체입니다.)  
  
 ADO 오류입니다: ADO 작업이 실패에서 하 여 발생 합니다. 기본 공급자에서 반환한 오류를 표시 **오류** 개체를 **연결** 개체 **오류** 컬렉션입니다.  
  
 합니다 **#import** 지시문 처리 루틴 메서드와 ADO.dll에 선언 된 속성에 대 한 오류만을 만듭니다. 그러나이 동일한 오류 처리 메커니즘 매크로 또는 인라인 함수를 검사 하 여 고유한 오류를 작성 하 여 활용을 걸릴 수 있습니다. 항목을 참조 하세요 [Visual c + + 확장](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md), 또는 예제를 보려면 다음 섹션의 코드입니다.  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual c + + 해당 하는 Visual Basic 규칙  
 다음은 ADO 설명서에서 해당 하는 Visual c + +에서를 비롯 하 여 Visual Basic의 경우에 코딩 된 여러 규칙을 요약 합니다.  
  
### <a name="declaring-an-ado-object"></a>ADO 개체를 선언합니다.  
 Visual basic에서 ADO 개체 변수 (이 경우에 **레코드 집합** 개체) 다음과 같이 선언 됩니다.  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 절은 "`ADODB.Recordset`"의 ProgID는 합니다 **레코드 집합** 레지스트리에 정의 된 개체입니다. 새 인스턴스를 **레코드** 개체는 다음과 같이 선언 됩니다.  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 -또는-  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 Visual c + +에서는 합니다 **#import** 지시문 모든 ADO 개체에 대 한 스마트 포인터 형식 선언을 생성 합니다. 예를 들어 가리키는 변수를 **_Recordset** 형식의 개체가 **_RecordsetPtr**를 다음과 같이 선언 되 고:  
  
```cpp
_RecordsetPtr  rs;  
```
  
 새 인스턴스를 가리키는 변수를 **_Recordset** 개체는 다음과 같이 선언 됩니다.  
  
```cpp
_RecordsetPtr  rs("ADODB.Recordset");  
```
  
 -또는-  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```
  
 -또는-  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```
  
 후 합니다 **CreateInstance** 메서드가 호출 되 면 변수를 다음과 같이 사용할 수 있습니다.  
  
```cpp
rs->Open(...);  
```
  
 한 경우, 다음에 유의 "`.`" 변수는 클래스의 인스턴스인 것 처럼 연산자를 사용 (`rs.CreateInstance`), 및 다른 경우에는 "`->`" 연산자는 변수를 인터페이스에 대 한 포인터 처럼 사용 됩니다 (`rs->Open`).  
  
 하나의 변수 때문에 두 가지 방법으로 사용할 수 있습니다는 "`->`" 인터페이스에 대 한 포인터 처럼 동작 하는 클래스의 인스턴스를 허용 하도록 연산자가 오버 로드 합니다. 인스턴스 변수 private 클래스 멤버에 대 한 포인터를 포함 합니다 **_Recordset** ; 인터페이스는 "`->`" 연산자의 멤버에 액세스 하는 포인터와 반환된 된 포인터를 반환 합니다는 **_Recordset**  개체입니다.  
  
### <a name="coding-a-missing-parameter--string"></a>누락 된 매개 변수 코딩-문자열  
 누락 된 코드 해야 할 때 **문자열** 피연산자 Visual basic의 경우 단순히 피연산자가 생략 합니다. Visual c + +에서는 피연산자를 지정 해야 합니다. 코드를 **_bstr_t** 빈 문자열 값으로 포함 합니다.  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter--variant"></a>누락 된 매개 변수 코딩-Variant  
 누락 된 코드 해야 할 때 **Variant** 피연산자 Visual basic의 경우 단순히 피연산자가 생략 합니다. Visual c + +의 모든 피연산자를 지정 해야 합니다. 누락 된 코드 **Variant** 매개 변수를 **_variant_t** 특수 값, DISP_E_PARAMNOTFOUND, 및 형식, VT_ERROR로 설정 합니다. 또는 지정할 **vtMissing**에서 제공 하는 해당 하는 미리 정의 된 상수를 **#import** 지시문입니다.  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 또는 사용  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>Variant 선언  
 Visual basic의 경우는 **Variant** 로 선언 합니다 **Dim** 문은 다음과 같이:  
  
```vb
Dim VariableName As Variant  
```
  
 Visual c + +에서 형식으로 변수를 선언 **_variant_t**합니다. 구성도 몇 **_variant_t** 선언 아래에 표시 됩니다.  
  
> [!NOTE]
>  이러한 선언에는 단순히을 대략적으로 자신의 프로그램에서 코드는 제공 합니다. 자세한 내용은 아래 예제 및 Visual C++ 설명서를 참조 하세요.  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>Variant의 배열을 사용 하 여  
 Visual basic에서 배열 **변형** 사용 하 여 코딩할 수 있습니다 합니다 **Dim** 문 또는 수를 사용할 수 있습니다 합니다 **배열** 함수를 다음 예제 코드 에서처럼:  
  
```vb
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```
  
 다음 Visual c + + 예제는 **SafeArray** 사용을 **_variant_t**합니다.  
  
#### <a name="notes"></a>참고  
 다음 정보는 코드 예제에서 주석 처리 된 섹션에 해당합니다.  
  
1.  다시 한 번 TESTHR() 인라인 함수는 기존 오류 처리 메커니즘을 활용 하기 위해 정의 됩니다.  
  
2.  사용할 수 있도록 1 차원 배열에만 필요한 **SafeArrayCreateVector**, 범용 대신 **SAFEARRAYBOUND** 선언 하 고 **SafeArrayCreate** 함수입니다. 다음은 해당 코드를 사용 하 여 새로운 같습니다 **SafeArrayCreate**:  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  열거형된 상수인으로 식별 되는 스키마 **adSchemaColumns**, 4 개 제약 조건 열과 연결 된: TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME 및 COLUMN_NAME 합니다. 따라서 배열을 **Variant** 네 개의 요소를 사용 하 여 값이 생성 됩니다. 그런 다음 TABLE_NAME 세 번째 열에 해당 하는 제약 조건 값이 지정 됩니다.  
  
     **레코드 집합** 반환 되는 여러 열을의 하위 집합은 제약 조건 열으로 구성 됩니다. 반환 된 각 행에 대 한 제약 조건 열의 값의 해당 제약 조건 값과 같아야 합니다.  
  
4.  익숙한 **Safearray** 수는 달라진 **SafeArrayDestroy**()를 종료 하기 전에 호출 되지 않습니다. 사실, 호출 **SafeArrayDestroy**()이 경우 하면 런타임 예외가 발생 합니다. 이유는 소멸자 `vtCriteria` 호출 **VariantClear**() 경우는 **_variant_t** 있는 범위를 벗어날를 **SafeArray**합니다. 호출 **SafeArrayDestroy**, 수동으로 지우지 않고 합니다 **_variant_t**, 잘못 된 선택을 취소 하려고 소멸자로 인해 **SafeArray** 포인터입니다.  
  
     하는 경우 **SafeArrayDestroy** 된 호출 코드는 다음과 같습니다.  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     그러나 것 수 있도록 하려면 훨씬 더 간단 합니다 **_variant_t** 관리를 **SafeArray**합니다.  
  
```cpp
// Visual_CPP_ADO_Prog_1.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Note 1  
inline void TESTHR( HRESULT _hr ) {   
   if FAILED(_hr)   
      _com_issue_error(_hr);   
}  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      _ConnectionPtr pCn("ADODB.Connection");  
      _variant_t vtTableName("authors"), vtCriteria;  
      long ix[1];  
      SAFEARRAY *pSa = NULL;  
  
      pCn->Provider = "sqloledb";  
      pCn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
      // Note 2, Note 3  
      pSa = SafeArrayCreateVector(VT_VARIANT, 1, 4);  
      if (!pSa)   
         _com_issue_error(E_OUTOFMEMORY);  
  
      // Specify TABLE_NAME in the third array element (index of 2).   
      ix[0] = 2;        
      TESTHR(SafeArrayPutElement(pSa, ix, &vtTableName));  
  
      // There is no Variant constructor for a SafeArray, so manually set the   
      // type (SafeArray of Variant) and value (pointer to a SafeArray).  
  
      vtCriteria.vt = VT_ARRAY | VT_VARIANT;  
      vtCriteria.parray = pSa;  
  
      pRs = pCn->OpenSchema(adSchemaColumns, vtCriteria, vtMissing);  
  
      long limit = pRs->GetFields()->Count;  
      for ( long x = 0 ; x < limit ; x++ )  
         printf( "%d: %s\n", x + 1, ((char*) pRs->GetFields()->Item[x]->Name) );  
      // Note 4  
      pRs->Close();  
      pCn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Code meaning = %s\n", (char*) e.ErrorMessage());  
      printf("Source = %s\n", (char*) e.Source());  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   CoUninitialize();  
}  
```
  
### <a name="using-property-getputputref"></a>속성 Get/Put/PutRef를 사용 하 여  
 Visual basic에서 속성의 이름은 여부에 따라이 검색, 할당에 대 한 참조를 할당 한정 되지 않습니다.  
  
```vb
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```
  
 이 Visual c + + 예제는 **가져오기**/**배치**/**PutRef * * * 속성*합니다.  
  
#### <a name="notes"></a>참고  
 다음 정보는 코드 예제에서 주석 처리 된 섹션에 해당합니다.  
  
1.  이 예제에서는 두 가지 형태의 문자열 인수 없음: 상수를 명시적 **strMissing**, 및 컴파일러 임시를 만드는 데 사용할 문자열 **_bstr_t** 합니다 의범위에있는 **열기** 메서드.  
  
2.  피연산자를 캐스팅 하는 데 필요한 아닙니다 `rs->PutRefActiveConnection(cn)` 하 `(IDispatch *)` 피연산자의 형식이 이미 `(IDispatch *)`합니다.  
  
```cpp
// Visual_CPP_ado_prog_2.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _bstr_t strMissing(L"");  
      long oldPgSz = 0, newPgSz = 5;  
  
      // Note 1  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", strMissing, "", adConnectUnspecified);  
  
      oldPgSz = rs->GetPageSize();  
      // -or-  
      // oldPgSz = rs->PageSize;  
  
      rs->PutPageSize(newPgSz);  
      // -or-  
      // rs->PageSize = newPgSz;  
  
      // Note 2  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockReadOnly, adCmdTable);  
      printf("Original pagesize = %d, new pagesize = %d\n", oldPgSz, rs->GetPageSize());  
      rs->Close();  
      cn->Close();  
  
   }  
   catch (_com_error &e) {  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="using-getitemx-and-itemx"></a>GetItem(x) 및 항목 [x]를 사용 하 여  
 Visual Basic 예제에 대 한 표준 구문과 대체 구문을 보여 줍니다 **항목**().  
  
```vb
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```
  
 Visual c + + 예제를 보여 줍니다 **항목**합니다.  
  
> [!NOTE]
>  코드 예제에서 주석 처리 된 섹션에 해당 하는 다음 참고: 사용 하 여 해당 컬렉션에 액세스 하면 **항목**, 인덱스 **2**, 캐스팅 되어야 합니다 **긴** 하므로 적절 한 생성자가 호출 됩니다.  
  
```cpp
// Visual_CPP_ado_prog_3.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
void main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _variant_t vtFirstName;  
  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", "", "", adConnectUnspecified);  
  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockOptimistic, adCmdTable);  
      rs->MoveFirst();  
  
      // Note 1. Get a field.  
      vtFirstName = rs->Fields->GetItem((long)2)->GetValue();  
      // -or-  
      vtFirstName = rs->Fields->Item[(long)2]->Value;  
  
      printf( "First name = '%s'\n", (char*)( (_bstr_t)vtFirstName) );  
  
      rs->Fields->GetItem((long)2)->Value = L"TEST";  
      rs->Update(vtMissing, vtMissing);  
  
      // Restore name  
      rs->Fields->GetItem((long)2)->PutValue(vtFirstName);  
      // -or-  
      rs->Fields->GetItem((long)2)->Value = vtFirstName;  
      rs->Update(vtMissing, vtMissing);  
      rs->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>사용 하 여 ADO 개체 포인터 캐스팅 (IDispatch *)  
 다음 Visual c + + 예제를 사용 하 여 하는 방법을 보여 줍니다 (IDispatch *) 캐스트 ADO 개체 포인터에 대 한 합니다.  
  
#### <a name="notes"></a>참고  
 다음 정보는 코드 예제에서 주석 처리 된 섹션에 해당합니다.  
  
1.  개방적이 고 지정 **연결** 개체를 명시적으로 코딩된 **Variant**합니다. 사용 하 여 캐스팅 (IDispatch \*) 올바른 생성자를 호출 합니다. 또한 두 번째를 명시적으로 설정할 **_variant_t** 매개 변수를 기본값인 **true**이므로 때 개체 참조 횟수 수정 될를 **Recordset::Open** 작업이 종료 됩니다.  
  
2.  식 `(_bstr_t)`, 캐스트 아닙니다 하지만 **_variant_t** 추출 하는 연산자를 **_bstr_t** 에서 문자열을 **Variant** 반환한 **값** .  
  
 식 `(char*)`, 캐스트 되지 않지만 **_bstr_t** 캡슐화 된 문자열에 대 한 포인터를 추출 하는 연산자를 **_bstr_t** 개체.  
  
 이 섹션의 코드의 유용한 동작의 일부를 보여 줍니다 **_variant_t** 하 고 **_bstr_t** 연산자입니다.  
  
```cpp
// Visual_CPP_ado_prog_4.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr pConn("ADODB.Connection");  
      _RecordsetPtr pRst("ADODB.Recordset");  
  
      pConn->Provider = "sqloledb";  
      pConn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
  
      // Note 1.  
      pRst->Open("authors", _variant_t((IDispatch *) pConn, true), adOpenStatic, adLockReadOnly, adCmdTable);  
      pRst->MoveLast();  
  
      // Note 2.  
      printf("Last name is '%s %s'\n",   
         (char*) ((_bstr_t) pRst->GetFields()->GetItem("au_fname")->GetValue()),  
         (char*) ((_bstr_t) pRst->Fields->Item["au_lname"]->Value));  
  
      pRst->Close();  
      pConn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }     
   ::CoUninitialize();  
}  
```
