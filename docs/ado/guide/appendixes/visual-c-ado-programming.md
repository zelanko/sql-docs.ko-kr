---
description: Visual C++ ADO 프로그래밍
title: Visual C++ ADO 프로그래밍 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 66d06630a6bc39c49b9a3e55276bed574869d40d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806766"
---
# <a name="visual-c-ado-programming"></a>Visual C++ ADO 프로그래밍
ADO API 참조는 Microsoft Visual Basic와 비슷한 구문을 사용 하 여 ADO API (응용 프로그래밍 인터페이스)의 기능을 설명 합니다. 대상 사용자가 모든 사용자 이기는 하지만 ADO 프로그래머는 Visual Basic, Visual C++ ( **#import** 지시문 포함 및 제외) 및 Visual j + + (ADO/WFC 클래스 패키지 사용)와 같은 다양 한 언어를 사용 합니다.  

> [!NOTE]
> Microsoft에서 2004의 Visual j + +에 대 한 지원을 종료 했습니다.

 이러한 다양성을 수용 하기 위해 [Visual C++ 구문 인덱스에 대 한 ADO](./using-ado-with-microsoft-visual-c.md) 는 API 참조에서 기능, 매개 변수, 예외 동작 등에 대 한 일반적인 설명에 대 한 링크와 함께 Visual C++ 언어별 구문을 제공 합니다.  
  
 ADO는 COM (구성 요소 개체 모델) 인터페이스를 사용 하 여 구현 됩니다. 그러나 프로그래머가 다른 프로그래밍 언어로 COM을 사용 하는 것이 더 쉽습니다. 예를 들어, COM을 사용 하는 거의 모든 세부 정보는 Visual Basic 프로그래머에 게 암시적으로 처리 되는 반면 Visual C++ 프로그래머는 해당 세부 정보에 참석 해야 합니다.  
  
 다음 섹션에서는 ADO 및 **#import** 지시어를 사용 하는 c 및 c + + 프로그래머에 대 한 세부 정보를 요약 합니다. COM (**Variant**, **BSTR**및 **SafeArray**)에 특정 한 데이터 형식 및 오류 처리 (_com_error)에 중점을 둘 수 있습니다.  
  
## <a name="using-the-import-compiler-directive"></a>#Import 컴파일러 지시문 사용  
 **#Import** Visual C++ 컴파일러 지시문은 ADO 메서드 및 속성을 사용 하 여 작업을 간소화 합니다. 지시문은 Msado15.dll ()와 같은 형식 라이브러리를 포함 하는 파일의 이름을 사용 하 고, typedef 선언, 인터페이스에 대 한 스마트 포인터 및 열거 된 상수를 포함 하는 헤더 파일을 생성 합니다. 각 인터페이스는 클래스에 캡슐화 되거나 래핑됩니다.  
  
 클래스 내의 각 작업 (즉, 메서드 또는 속성 호출)에 대해 작업을 직접 호출 하는 선언 (즉, 작업의 "원시" 형식) 및 작업을 성공적으로 실행 하지 못한 경우에는 원시 작업을 호출 하 고 COM 오류를 throw 하는 선언이 있습니다. 작업이 속성 인 경우 일반적으로 Visual Basic와 같은 구문이 있는 작업에 대 한 대체 구문을 만드는 컴파일러 지시문이 있습니다.  
  
 속성의 값을 검색 하는 작업에는 **Get**_property_형식의 이름이 있습니다. 속성의 값을 설정 하는 작업에는 **Put**_속성_형식의 이름이 있습니다. ADO 개체에 대 한 포인터를 사용 하 여 속성 값을 설정 하는 작업에는 **Putref**_속성_형식의 이름이 있습니다.  
  
 이러한 형식의 호출을 통해 속성을 가져오거나 설정할 수 있습니다.  
  
```cpp
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```
  
## <a name="using-property-directives"></a>속성 지시문 사용  
 **__Declspec (속성 ...)** 컴파일러 지시문은 속성으로 사용 되는 함수를 선언 하 여 대체 구문을 포함 하는 Microsoft 전용 C 언어 확장입니다. 따라서 Visual Basic와 비슷한 방식으로 속성 값을 설정 하거나 가져올 수 있습니다. 예를 들어 다음과 같은 방법으로 속성을 설정 하 고 가져올 수 있습니다.  
  
```cpp
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```
  
 코드를 사용할 필요가 없습니다.  
  
```cpp
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```
  
 컴파일러는 **Get** _-_ 선언 된 대체 구문 및 속성을 읽거나 쓸지 여부를 기반으로 적절 한 Get, **Put**또는 **putref**_속성_ 호출을 생성 합니다.  
  
 **__Declspec (속성 ...)** 컴파일러 지시문은 함수에 대 한 **get**, **put**또는 **get** 및 **put** 구문도 선언할 수 있습니다. 읽기 전용 작업에는 **get** 선언만 있습니다. 쓰기 전용 작업에는 **put** 선언만 있습니다. 읽기 및 쓰기 작업에는 모두 **get** 및 **put** 선언이 있습니다.  
  
 이 지시문을 사용 하는 경우 두 개의 선언만 가능 합니다. 그러나 각 속성에는 속성 **가져오기**_,_ **배치**_속성_및 **putref**_속성_의 세 가지 속성 함수가 있을 수 있습니다. 이 경우 두 가지 형식의 속성에만 대체 구문이 있습니다.  
  
 예를 들어 **Command** object **ActiveConnection** 속성은 **Get**_ActiveConnection_ 및 **putref**_ActiveConnection_에 대 한 대체 구문으로 선언 됩니다. 예를 들어 **Putref**구문은 일반적으로이 속성에 열린 **연결** 개체 (즉, **연결** 개체 포인터)를 배치 하는 것이 좋습니다. 반면에 **레코드 집합** 개체에는 **Get**, **Put**및 **putref**_ActiveConnection_ 연산이 있지만 대체 구문은 없습니다.  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>컬렉션, GetItem 메서드 및 Item 속성  

 ADO는 **필드**, **매개 변수**, **속성**및 **오류**를 비롯 한 여러 컬렉션을 정의 합니다. Visual C++에서 **GetItem (_인덱스_)** 메서드는 컬렉션의 멤버를 반환 합니다. *Index* 는 **Variant**이며이 값은 컬렉션에 있는 멤버의 숫자 인덱스 이거나 멤버의 이름을 포함 하는 문자열입니다.  
  
 **__Declspec (속성 ...)** 컴파일러 지시문은 **Item** 속성을 각 컬렉션의 기본 **GetItem ()** 메서드에 대 한 대체 구문으로 선언 합니다. 대체 구문은 대괄호를 사용 하 고 배열 참조와 유사 하 게 보입니다. 일반적으로 두 가지 형태는 다음과 같습니다.  
  
```cpp
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```
  
 예를 들어 **pubs** 데이터베이스의 **authors** 테이블에서 파생 된 **_rs_** 라는 **레코드 집합** 개체의 필드에 값을 할당 합니다. **Item ()** 속성을 사용 하 여 **레코드 집합** 개체 **필드** 컬렉션의 세 번째 **필드** 에 액세스 합니다. 컬렉션은 0에서 인덱싱됩니다. 세 번째 필드의 이름은 **_au \_ fname_** 이라고 가정 합니다. 그런 다음 **Field** 개체에서 **value ()** 메서드를 호출 하 여 문자열 값을 할당 합니다.  
  
 다음 네 가지 방법으로 Visual Basic 표현할 수 있습니다. 마지막 두 형식은 Visual Basic에 고유 하며 다른 언어에는 해당 사항이 없습니다.  
  
```cpp
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```
  
 위의 처음 두 폼에 Visual C++에 해당 하는 것은 다음과 같습니다.  
  
```cpp
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```
  
 -또는-( **Value** 속성에 대 한 대체 구문도 표시 됨)  
  
```cpp
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```
  
 컬렉션을 반복 하는 예제는 "ADO 참조"의 "ADO 컬렉션" 섹션을 참조 하세요.  
  
## <a name="com-specific-data-types"></a>COM 특정 데이터 형식  
 일반적으로 ADO API 참조에서 찾을 수 있는 모든 Visual Basic 데이터 형식에는 해당 하는 Visual C++ 있습니다. 여기에는 Visual Basic **바이트**에 대 한 **unsigned char** 와 같은 표준 데이터 형식, **정수**에 대 한 short **및 long의** **long** 이 포함 됩니다. **short** 구문 Indexesto에서 지정 된 메서드 또는 속성의 피연산자에 필요한 것을 정확 하 게 확인 합니다.  
  
 이 규칙에 대 한 예외는 COM에 한정 된 **Variant**, **BSTR**및 **SafeArray**의 데이터 형식입니다.  
  
### <a name="variant"></a>Variant  
 **변형은** 값 멤버 및 데이터 형식 멤버를 포함 하는 구조화 된 데이터 형식입니다. **Variant** 에는 다른 VARIANT, BSTR, Boolean, IDispatch 또는 IUnknown 포인터, 통화, 날짜 등을 비롯 한 다양 한 데이터 형식이 포함 될 수 있습니다. 또한 COM은 한 데이터 형식을 다른 데이터 형식으로 쉽게 변환할 수 있게 해 주는 메서드를 제공 합니다.  
  
 **_Variant_t** 클래스는 **variant** 데이터 형식을 캡슐화 하 고 관리 합니다.  
  
 ADO API 참조에서 메서드 또는 속성 피연산자가 값을 사용 하는 경우 일반적으로 값이 **_variant_t**전달 됨을 의미 합니다.  
  
 ADO API 참조 항목의 **매개 변수** 섹션에서 피연산자가 **Variant**라고 표시 되는 경우이 규칙은 명시적으로 true입니다. 한 가지 예외는 설명서에서 명시적으로 피연산자가 **Long** 또는 **Byte**또는 열거와 같은 표준 데이터 형식을 사용 하는 경우입니다. 또 다른 예외는 피연산자가 **문자열**을 사용 하는 경우입니다.  
  
### <a name="bstr"></a>BSTR  
 **BSTR** (**B**이 있습니다 **STR**)은 문자열 및 문자열 길이를 포함 하는 구조화 된 데이터 형식입니다. COM은 **BSTR**을 할당 하 고 조작 하 고 해제 하는 메서드를 제공 합니다.  
  
 **_Bstr_t** 클래스는 **bstr** 데이터 형식을 캡슐화 하 고 관리 합니다.  
  
 ADO API 참조에서 메서드 또는 속성이 **문자열** 값을 사용 하는 것으로 표시 되는 경우이 값은 **_bstr_t**형식으로 되어 있음을 의미 합니다.  
  
### <a name="casting-_variant_t-and-_bstr_t-classes"></a>_Variant_t 및 _bstr_t 클래스 캐스팅  
 작업에 대 한 인수에서 **_variant_t** 또는 **_bstr_t** 를 명시적으로 코딩할 필요가 없는 경우가 종종 있습니다. **_Variant_t** 또는 **_bstr_t** 클래스에 인수의 데이터 형식과 일치 하는 생성자가 있는 경우 컴파일러에서 적절 한 **_variant_t** 또는 **_bstr_t**를 생성 합니다.  
  
 그러나 인수가 모호한 경우, 즉 인수의 데이터 형식이 둘 이상의 생성자와 일치 하는 경우 올바른 생성자를 호출 하려면 인수를 적절 한 데이터 형식으로 캐스팅 해야 합니다.  
  
 예를 들어 **Recordset:: Open** 메서드의 선언은 다음과 같습니다.  
  
```cpp
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```
  
 `ActiveConnection`인수는 연결 문자열 또는 열린 **연결** 개체에 대 한 포인터로 코딩할 수 있는 **_variant_t**에 대 한 참조를 사용 합니다.  
  
 "" **_variant_t** 와 같은 문자열 `DSN=pubs;uid=MyUserName;pwd=MyPassword;` 또는 ""와 같은 포인터를 전달 하는 경우 올바른 _variant_t 생성 됩니다 `(IDispatch *) pConn` .  
  
> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.  
  
 또는 ""와 같은 포인터를 포함 하는 **_variant_t** 를 명시적으로 코딩할 수 있습니다 `_variant_t((IDispatch *) pConn, true)` . Cast는 `(IDispatch *)` IUnknown 인터페이스에 대 한 포인터를 사용 하는 다른 생성자를 사용 하 여 모호성을 해결 합니다.  
  
 매우 중요 하지만 ADO가 IDispatch 인터페이스 이기는 하지만 거의 언급 되지 않습니다. ADO 개체에 대 한 포인터가 **Variant**로 전달 되어야 할 때마다 해당 포인터를 IDispatch 인터페이스에 대 한 포인터로 캐스팅 해야 합니다.  
  
 마지막 사례는 선택적의 기본값인를 사용 하 여 생성자의 두 번째 부울 인수를 명시적으로 코딩 합니다 `true` . 이 인수를 통해 **Variant** 생성자는 ado 메서드 또는 속성 호출이 완료 될 때 **_Variant_t:: Release**() 메서드를 자동으로 호출 하는 ado를 보정 하는 **AddRef**() 메서드를 호출 합니다.  
  
### <a name="safearray"></a>SafeArray  
 **SafeArray** 는 다른 데이터 형식의 배열을 포함 하는 구조화 된 데이터 형식입니다. **SafeArray** 는 각 배열 차원의 범위에 대 한 정보를 포함 하 고 해당 범위 내의 배열 요소에 대 한 액세스를 제한 하기 때문에 *safe* 라고 합니다.  
  
 ADO API 참조에서 메서드 또는 속성이 배열을 사용 하거나 반환 하는 경우 메서드 또는 속성이 네이티브 C/c + + 배열이 아닌 **SafeArray**를 사용 하거나 반환 하는 것을 의미 합니다.  
  
 예를 들어 **Connection** object **OpenSchema** 메서드의 두 번째 매개 변수에는 **변형** 값 배열이 필요 합니다. 이러한 **변형** 값은 **safearray**의 요소로 전달 되어야 하며, **safearray** 는 다른 **variant**의 값으로 설정 되어야 합니다. **OpenSchema**의 두 번째 인수로 전달 되는 다른 **변형이** 있습니다.  
  
 추가 예제에서 **Find** 메서드의 첫 번째 인수는 값이 1 차원 **SafeArray**인 **Variant** 입니다. **AddNew** 의 첫 번째 및 두 번째 선택적 인수는 1 차원 **SafeArray**입니다. **GetRows** 메서드의 반환 값은 값이 2 차원 **SafeArray**인 **Variant** 입니다.  
  
## <a name="missing-and-default-parameters"></a>누락 및 기본 매개 변수  
 Visual Basic 메서드에서 누락 된 매개 변수를 허용 합니다. 예를 들어 **레코드 집합** 개체의 **Open** 메서드에 5 개의 매개 변수가 있지만 중간 매개 변수를 건너뛰고 후행 매개 변수는 벗어날 수 있습니다. 기본 **BSTR** 또는 **Variant** 는 누락 된 피연산자의 데이터 형식에 따라 대체 됩니다.  
  
 C/c + +에서는 모든 피연산자를 지정 해야 합니다. 데이터 형식이 문자열 인 누락 된 매개 변수를 지정 하려면 null 문자열을 포함 하는 **_bstr_t** 를 지정 합니다. 데이터 형식이 **Variant**인 누락 된 매개 변수를 지정 하려면 DISP_E_PARAMNOTFOUND 값 및 VT_ERROR 유형을 사용 하 여 **_variant_t** 를 지정 합니다. 또는 **#import** 지시문에서 제공 하는 동등한 **_Variant_t** 상수 ( **vtMissing**)를 지정 합니다.  
  
 세 가지 메서드는 일반적인 **vtMissing**사용에 대 한 예외입니다. 이는 **Connection** 및 **Command** 개체의 **Execute** 메서드와 **Recordset** 개체의 **NextRecordset** 메서드입니다. 해당 서명은 다음과 같습니다.  
  
```cpp
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```
  
 *RecordsAffected* 및 *parameters*매개 변수는 **변형**에 대 한 포인터입니다. *매개 변수* 는 실행 중인 명령을 수정 하는 단일 매개 변수 또는 매개 변수 배열을 포함 하는 **Variant** 의 주소를 지정 하는 입력 매개 변수입니다. *RecordsAffected* 는 메서드의 영향을 받는 행 수가 반환 되는 **변형의**주소를 지정 하는 출력 매개 변수입니다.  
  
 **Command** object **Execute** 메서드에서 *매개 변수* 를 `&vtMissing` (권장) 또는 null 포인터 ( **null** 또는 0)로 설정 하 여 매개 변수를 지정 하지 않았음을 지정 합니다. *매개 변수가* null 포인터로 설정 된 경우 메서드는 내부적으로 **vtMissing**의 해당 항목을 대체 한 다음 작업을 완료 합니다.  
  
 모든 메서드에서 *RecordsAffected* 을 null 포인터로 설정 하 여 영향을 받는 레코드 수를 반환 하지 않아야 함을 표시 합니다. 이 경우, 메서드는 영향을 받는 레코드 수를 취소 해야 한다는 것을 나타내는 매개 변수가 없기 때문에 null 포인터가 아닙니다.  
  
 따라서이 세 가지 방법의 경우 다음과 같은 코드를 사용할 수 있습니다.  
  
```cpp
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```
  
## <a name="error-handling"></a>오류 처리  
 COM에서 대부분의 작업은 함수가 성공적으로 완료 되었는지 여부를 나타내는 HRESULT 반환 코드를 반환 합니다. **#Import** 지시문은 각 "raw" 메서드 또는 속성에 대 한 래퍼 코드를 생성 하 고 반환 된 HRESULT를 확인 합니다. HRESULT가 실패를 나타내면 래퍼 코드는 HRESULT 반환 코드를 인수로 사용 하 여 _com_issue_errorex ()를 호출 하 여 COM 오류를 throw 합니다. COM 오류 개체는 **try** - **catch** 블록에서 catch 할 수 있습니다. 효율성을 높이기 위해 **_com_error** 개체에 대 한 참조를 catch 합니다.  
  
 Ado 오류가 발생 하 여 ado 작업이 실패 하는 것을 명심 해야 합니다. 기본 공급자가 반환 하는 오류는 **연결** 개체 **오류** 컬렉션에 **오류** 개체로 표시 됩니다.  
  
 **#Import** 지시문은 ADO .dll에 선언 된 메서드 및 속성에 대 한 오류 처리 루틴만 만듭니다. 그러나 사용자 고유의 오류 검사 매크로나 인라인 함수를 작성 하 여 이와 동일한 오류 처리 메커니즘을 활용할 수 있습니다. 예제는 다음 섹션의 [Visual C++ 확장](./visual-c-extensions-for-ado.md)또는 코드 항목을 참조 하세요.  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual C++ 해당 Visual Basic 규칙  
 다음은 ADO 설명서에서 Visual Basic 코딩 된 몇 가지 규칙에 대 한 요약 및 Visual C++의 해당 항목입니다.  
  
### <a name="declaring-an-ado-object"></a>ADO 개체 선언  
 Visual Basic에서 ADO 개체 변수 (이 경우 **레코드 집합** 개체의 경우)는 다음과 같이 선언 됩니다.  
  
```vb
Dim rst As ADODB.Recordset  
```
  
 "" 절은 `ADODB.Recordset` 레지스트리에 정의 된 **레코드 집합** 개체의 ProgID입니다. **Record** 개체의 새 인스턴스는 다음과 같이 선언 됩니다.  
  
```vb
Dim rst As New ADODB.Recordset  
```
  
 또는  
  
```vb
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```
  
 Visual C++에서 **#import** 지시문은 모든 ADO 개체에 대 한 스마트 포인터 형식 선언을 생성 합니다. 예를 들어 **_Recordset** 개체를 가리키는 변수는 **_RecordsetPtr**형식이 며 다음과 같이 선언 됩니다.  
  
```cpp
_RecordsetPtr  rs;  
```
  
 **_Recordset** 개체의 새 인스턴스를 가리키는 변수는 다음과 같이 선언 됩니다.  
  
```cpp
_RecordsetPtr  rs("ADODB.Recordset");  
```
  
 또는  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```
  
 또는  
  
```cpp
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```
  
 **CreateInstance** 메서드를 호출한 후에는 변수를 다음과 같이 사용할 수 있습니다.  
  
```cpp
rs->Open(...);  
```
  
 하나는 `.` 변수가 클래스의 인스턴스인 것 처럼 "" 연산자를 사용 하 `rs.CreateInstance` 고, 다른 경우에는 `->` 변수가 인터페이스 ()에 대 한 포인터인 것 처럼 "" 연산자를 사용 `rs->Open` 합니다.  
  
 " `->` " 연산자는 클래스의 인스턴스가 인터페이스에 대 한 포인터 처럼 동작 하도록 하기 위해 오버 로드 되기 때문에 두 가지 방법으로 하나의 변수를 사용할 수 있습니다. 인스턴스 변수의 private 클래스 멤버가 **_Recordset** 인터페이스에 대 한 포인터를 포함 합니다. " `->` " 연산자는 해당 포인터를 반환 하 고 반환 된 포인터는 **_Recordset** 개체의 멤버에 액세스 합니다.  
  
### <a name="coding-a-missing-parameter---string"></a>누락 된 매개 변수-문자열 코딩  
 Visual Basic에서 누락 된 **문자열** 피연산자를 코딩 해야 하는 경우 피연산자를 생략 하기만 하면 됩니다. Visual C++에서 피연산자를 지정 해야 합니다. 값으로 빈 문자열을 포함 하는 **_bstr_t** 을 코딩 합니다.  
  
```cpp
_bstr_t strMissing(L"");  
```
  
### <a name="coding-a-missing-parameter---variant"></a>누락 된 매개 변수-Variant 코딩  
 Visual Basic에서 누락 된 **Variant** 피연산자를 코딩 해야 하는 경우 피연산자를 생략 하기만 하면 됩니다. Visual C++에 모든 피연산자를 지정 해야 합니다. **_Variant_t** 특수 값, DISP_E_PARAMNOTFOUND 및 형식 VT_ERROR으로 설정 된 누락 된 **Variant** 매개 변수를 코딩 합니다. 또는 **#import** 지시문에서 제공 하는 해당 하는 미리 정의 된 상수인 **vtMissing**를 지정 합니다.  
  
```cpp
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```
  
 -또는 사용-  
  
```cpp
...vtMissing...;  
```
  
### <a name="declaring-a-variant"></a>변형 선언  
 Visual Basic에서 **Variant** 는 다음과 같이 **Dim** 문으로 선언 됩니다.  
  
```vb
Dim VariableName As Variant  
```
  
 Visual C++에서 변수를 **_variant_t**형식으로 선언 합니다. 다음과 같은 몇 가지 도식 **_variant_t** 선언이 있습니다.  
  
> [!NOTE]
>  이러한 선언은 자신의 프로그램에서 코드를 작성 하는 것에 대 한 대략적인 아이디어를 제공 합니다. 자세한 내용은 아래 예제 및 Visual C + + 설명서를 참조 하세요.  
  
```cpp
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```
  
### <a name="using-arrays-of-variants"></a>변형 배열 사용  
 Visual Basic에서 **variant** 배열을 **Dim** 문으로 코딩 하거나 다음 예제 코드에서 설명한 대로 **배열** 함수를 사용할 수 있습니다.  
  
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
  
 다음 Visual C++ 예제에서는 **_variant_t**에서 사용 되는 **SafeArray** 를 사용 하는 방법을 보여 줍니다.  
  
#### <a name="notes"></a>참고  
 다음 메모는 코드 예제의 주석 처리 된 섹션에 해당 합니다.  
  
1.  다시 한 번 TESTHR () 인라인 함수를 정의 하 여 기존 오류 처리 메커니즘을 활용 합니다.  
  
2.  1 차원 배열만 필요 하므로 범용 **Safearraybound** 선언 및 **safearraybound** 함수 대신 **SafeArrayCreateVector**를 사용할 수 있습니다. **Safearraycreate**를 사용 하는 것과 같은 코드는 다음과 같습니다.  
  
    ```cpp
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```
  
3.  열거형 상수 ( **adSchemaColumns**)로 식별 되는 스키마는 TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME 및 COLUMN_NAME의 네 가지 제약 조건 열과 연결 되어 있습니다. 따라서 네 개의 요소가 있는 **Variant** 값 배열이 생성 됩니다. 그런 다음 세 번째 열 TABLE_NAME에 해당 하는 제약 조건 값이 지정 됩니다.  
  
     반환 되는 **레코드 집합** 은 몇 개의 열, 즉 제약 조건 열인 하위 집합으로 구성 됩니다. 반환 된 각 행에 대 한 제약 조건 열의 값은 해당 제약 조건 값과 동일 해야 합니다.  
  
4.  **Safearray** 에 익숙한 경우에는 종료 전에 **safearraydestroy**()이 호출 되지 않을 수 있습니다. 실제로이 경우 **Safearraydestroy**()을 호출 하면 런타임 예외가 발생 합니다. 그 이유는에 대 한 소멸자는 `vtCriteria` **_variant_t** 범위를 벗어날 때 **VariantClear**()를 호출 하므로 **SafeArray**가 해제 됩니다. **_Variant_t**를 수동으로 지우지 않고 **safearraydestroy**를 호출 하면 소멸자가 잘못 된 **SafeArray** 포인터를 지우도록 시도 합니다.  
  
     **Safearraydestroy** 를 호출한 경우 코드는 다음과 같습니다.  
  
    ```cpp
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```
  
     그러나 **_variant_t** 에서 **SafeArray**를 관리 하는 것이 훨씬 더 간단 합니다.  
  
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
  
### <a name="using-property-getputputref"></a>Property Get/Put/PutRef 사용  
 Visual Basic에서 속성의 이름은 검색, 할당 또는 참조에 할당 되었는지 여부에 관계 없이 정규화 되지 않습니다.  
  
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
  
 이 Visual C++ 예제에서는 **Get** / **Put** / **putref**_속성_을 보여 줍니다.  
  
#### <a name="notes"></a>참고  
 다음 메모는 코드 예제의 주석 처리 된 섹션에 해당 합니다.  
  
1.  이 예제에서는 두 가지 형식의 누락 된 문자열 인수를 사용 합니다. 명시적 상수, **Strmissing**및 컴파일러가 **Open** 메서드의 범위에 대해 존재 하는 임시 **_bstr_t** 을 만드는 데 사용 하는 문자열입니다.  
  
2.  `rs->PutRefActiveConnection(cn)` `(IDispatch *)` 피연산자의 형식이 이미 이므로의 피연산자를로 캐스팅할 필요가 없습니다 `(IDispatch *)` .  
  
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
  
### <a name="using-getitemx-and-itemx"></a>GetItem (x) 및 Item 사용 [x]  
 이 Visual Basic 예제에서는 **Item**()의 표준 및 대체 구문을 보여 줍니다.  
  
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
  
 이 Visual C++ 예제에서는 **항목**을 보여 줍니다.  
  
> [!NOTE]
>  다음은 코드 예제에서 주석으로 처리 된 섹션에 해당 하는 내용입니다. **Item**을 사용 하 여 컬렉션에 액세스 하는 경우 인덱스 **2**를 **long** 으로 캐스팅 해야 적절 한 생성자가 호출 됩니다.  
  
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
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>를 사용 하 여 ADO 개체 포인터 캐스팅 (IDispatch *)  
 다음 Visual C++ 예제에서는 (IDispatch *)를 사용 하 여 ADO 개체 포인터를 캐스팅 하는 방법을 보여 줍니다.  
  
#### <a name="notes"></a>참고  
 다음 메모는 코드 예제의 주석 처리 된 섹션에 해당 합니다.  
  
1.  명시적으로 코딩 된 **Variant**에서 열린 **연결** 개체를 지정 합니다. (IDispatch)로 캐스팅 하면 \* 올바른 생성자가 호출 됩니다. 또한 두 번째 **_variant_t** 매개 변수를 기본값인 **true**로 명시적으로 설정 하면 **Recordset:: Open** 작업이 종료 될 때 개체 참조 개수가 올바릅니다.  
  
2.  식은 `(_bstr_t)` 캐스트가 아니지만 **값**으로 반환 된 **변형** 에서 **_bstr_t** 문자열을 추출 하는 **_variant_t** 연산자입니다.  
  
 식은 캐스트가 아니라 `(char*)` **_bstr_t** 개체의 캡슐화 된 문자열에 대 한 포인터를 추출 하는 **_bstr_t** 연산자입니다.  
  
 코드의이 섹션에서는 **_variant_t** 및 **_bstr_t** 연산자에 대 한 몇 가지 유용한 동작을 보여 줍니다.  
  
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