---
title: Visual c + + ADO 프로그래밍 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 37c00d7256beef1041ee9c24484449971c3dceee
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="visual-c-ado-programming"></a>Visual c + + ADO 프로그래밍
ADO API 참조는 ADO 응용 프로그램 프로그래밍 인터페이스의 (API) Microsoft Visual Basic과 유사한 구문을 사용 하 여 기능을 설명 합니다. ADO 프로그래머 Visual Basic, Visual c + + 등의 다양 한 언어를 사용 하지만 사용자는 모든 사용자, (하거나 사용 하지 않고는 **#import** 지시문), 및 Visual J++ (ADO/WFC 클래스 패키지)와 함께 합니다.  

> [!NOTE]
> 2004 년에 Microsoft에 지원을 Visual J++에 대 한 종료 되었습니다.

 이러한 다양성을 수용 하기 위해는 [Visual c + + 구문 인덱스에 대 한 ADO](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) 기능, 매개 변수, 예외 동작 및 API에 대 한 일반적인 설명으로의 링크와 함께 Visual c + + 언어 관련 구문을 제공 참조입니다.  
  
 ADO는 COM (구성 요소 개체 모델) 인터페이스를 사용 하 여 구현 됩니다. 그러나 다른 사용자 보다는 특정 프로그래밍 언어로 COM을 사용 하는 프로그래머를 위한 쉽습니다. 예를 들어 COM을 사용 하 여 거의 모든 세부 사항은 암시적으로 처리 Visual Basic 프로그래머를 위한 Visual c + + 프로그래머는 해당 정보 자체에 참석 해야 하는 반면 합니다.  
  
 다음 섹션에서는 ADO를 사용 하는 C 및 c + + 프로그래머를 위한 세부 정보를 요약 및 **#import** 지시문입니다. COM에 관련 된 데이터 형식에 중점을 둡니다 (**Variant**, **BSTR**, 및 **SafeArray**), 및 오류 처리 (_com_error).  
  
## <a name="using-the-import-compiler-directive"></a>#Import 컴파일러 지시문을 사용 하 여  
 **#import** Visual c + + 컴파일러 지시문에는 ADO 메서드 및 속성 사용 작업을 간소화 합니다. 지시문은 ADO.dll (Msado15.dll) 등의 형식 라이브러리를 포함 하는 파일의 이름을 사용 하 고 형식 정의 선언, 인터페이스 및 열거 상수에 대 한 스마트 포인터를 포함 하는 헤더 파일을 생성 합니다. 각 인터페이스 캡슐화 또는 클래스에 래핑됩니다.  
  
 클래스 (즉, 메서드 또는 속성이 호출) 내에서 각 작업에는 해당 작업을 직접 (즉, "원시"의 형태 작업)를 호출 하는 선언 및 원시 작업을 호출 하 고 succ를 실행 하는 작업이 실패 한 경우 COM 오류를 throw 하는 선언 essfully 합니다. 작업 속성 인 경우는 일반적으로 컴파일러 지시문 Visual Basic 같은 구문이 있는 작업에 대 한 대체 구문을 만드는입니다.  
  
 속성의 값을 검색 하는 작업 이름이 양식의 **가져오기 * * * 속성*합니다. 속성의 값을 설정 하는 작업 이름이 양식의 **배치 * * * 속성*합니다. ADO 개체에 대 한 포인터를 사용 하 여 속성의 값을 설정 하는 작업 이름이 양식의 **PutRef * * * 속성*합니다.  
  
 이러한 형식으로 호출 하 여 속성을 설정 또는 얻을 수 있습니다.  
  
```  
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```  
  
## <a name="using-property-directives"></a>속성 지시문을 사용 하 여  
 **__declspec**  컴파일러 지시문은 대체 구문의을 속성으로 사용 하는 함수를 선언 하는 Microsoft 전용 C 언어 확장입니다. 결과적으로, 설정 또는 Visual Basic에서와 비슷한 방식으로 속성의 값을 얻을 수 있습니다. 예를 들어 설정할 수 있으며 이러한 방식으로 속성 가져오기:  
  
```  
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```  
  
 코드에 없는 주의 사항:  
  
```  
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```  
  
 컴파일러는 적절 한 생성 **Get * * *-*, **배치**-, 또는 **PutRef * * * 속성* 호출 되는 대체 구문을 선언 되었고 속성 인지에 따라 읽기 또는 쓰기 대상입니다.  
  
 **__declspec**  컴파일러 지시문만 선언할 수 **가져오기**, **배치**, 또는 **가져오기** 및 **배치** 함수에 대 한 대체 구문입니다. 읽기 전용 작업을 하나만 **가져오기** 선언; 쓰기 전용 작업을 하나만 **배치** 선언; 읽기는 모두 및 쓰기 둘 다 있어야 하는 작업 **가져오기** 및 **배치** 선언 합니다.  
  
 두 개의 선언이이 지시문; 가능있지 않습니다. 그러나 각 속성 구문이 있을 수: **가져오기 * * * 속성*, **배치 * * * 속성*, 및 **PutRef * * * 속성*합니다. 이 경우에 두 가지 형태의 속성은 대체 구문이 있습니다.  
  
 예를 들어는 **명령** 개체 **ActiveConnection** 속성에 대 한 대체 구문이 선언 **가져오기 * * * ActiveConnection* 및 **PutRef * * * ActiveConnection*합니다. **PutRef**-구문은 실제로 일반적으로 배치 하려면 열려 있는 하므로 좋은 선택 **연결** 개체 (즉, 한 **연결** 개체 포인터)이 속성입니다. 반면에 **레코드 집합** 개체에 **가져오기**-, **배치**-, 및 **PutRef * * * ActiveConnection* 작업 하지만 대안이 없는 구문입니다.  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>컬렉션, GetItem 메서드 및 항목 속성  
 포함 하는 여러 컬렉션을 정의 하는 ADO **필드**, **매개 변수**, **속성**, 및 **오류**합니다. Visual c + +에서는 **GetItem (***인덱스***)** 메서드가 컬렉션의 멤버를 반환 합니다. *인덱스* 는 **Variant**, 해당 값은 컬렉션에서 멤버의 숫자 인덱스 또는 멤버의 이름을 포함 하는 문자열입니다.  
  
 **__declspec**  컴파일러 지시문 선언 된 **항목** 각 컬렉션에는 대체 구문으로 속성의 기본 **GetItem()** 메서드. 대체 구문 대괄호를 사용 하 고 배열 참조와 비슷합니다. 일반적으로 두 가지 형태는 다음과 같습니다.  
  
```  
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```  
  
 예를 들어 필드에 값을 할당 한 **레코드 집합** 라는 개체 ***rs***에서 파생 된는 **작성자** 테이블의는 **pubs** 데이터베이스입니다. 사용 하 여는 **Item()** 속성에는 세 번째 액세스 **필드** 의 **레코드 집합** 개체 **필드** 컬렉션 (컬렉션에서는 또는 인덱스 0입니다. 세 번째 필드 라고 가정 ***au_fname***). 그런 다음 호출에서 **value ()** 메서드를는 **필드** 문자열 값을 할당 하는 개체입니다.  
  
 이 수를 표시할 수 Visual Basic에서 다음 네 가지 방법 (Visual Basic에 고유한는 마지막 두 형식, 다른 언어 없고):  
  
```  
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```  
  
 위의 처음 두 형식에 해당 Visual c + +에서은입니다.  
  
```  
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```  
  
 -또는-(대체 구문에 대 한는 **값** 속성 표시 됨)  
  
```  
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```  
  
 에 대 한 예제는 컬렉션을 반복 하십시오 "ADO 참조"의 "ADO 컬렉션" 섹션을 참조 합니다.  
  
## <a name="com-specific-data-types"></a>COM 별 데이터 형식  
 일반적으로 ADO API 참조에서 찾기는 Visual Basic 데이터 형식에는 Visual c + + 해당 있습니다. 여기에 표준 데이터 형식 같은 **unsigned char** Visual basic **바이트**, **짧은** 에 대 한 **정수**, 및  **긴** 에 대 한 **긴**합니다. 구문 Indexesto 찾는 위치 정확 하 게 위해 꼭 필요한 특정된 메서드 또는 속성의 피연산자는 참조 합니다.  
  
 이 규칙에 대 한 예외는 COM에 특정 데이터 형식: **Variant**, **BSTR**, 및 **SafeArray**합니다.  
  
### <a name="variant"></a>Variant  
 A **Variant** 값 멤버 및 데이터 형식 멤버를 포함 하는 구조화 된 데이터 형식입니다. A **Variant** 다양 한 범위의 다른 Variant, BSTR, 부울, IDispatch 또는 IUnknown 포인터, 통화, 날짜 및 등을 비롯 한 다른 데이터 형식에 포함 될 수 있습니다. COM를 쉽게 하는 메서드를 다른 데이터 형식 변환도 제공 합니다.  
  
 **_variant_t** 캡슐화 하 고 관리 하는 클래스는 **Variant** 데이터 형식입니다.  
  
 ADO API 참조 표시는 메서드 또는 속성 피연산자 값을 사용 하는 경우 일반적으로 의미에 값이 전달 되는 **_variant_t**합니다.  
  
 이 규칙은 명시적으로 true는 **매개 변수** ADO API 참조 항목의 섹션에 따르면 피연산자는 **Variant**합니다. 한 가지 예외는 피연산자는 표준 데이터 형식을와 같은 사용 설명서 명시적으로 표시 되 면 **긴** 또는 **바이트**, 나 열거 합니다. 다른 예외는 피연산자를 사용 하는 경우는 **문자열**합니다.  
  
### <a name="bstr"></a>BSTR  
 A **BSTR** (**B**있습니다 **STR**연산)은 문자열 및 문자열의 길이 포함 하는 구조화 된 데이터 형식입니다. 할당, 조작 및 해제 하는 메서드를 제공 하는 COM는 **BSTR**합니다.  
  
 **_bstr_t** 캡슐화 하 고 관리 하는 클래스는 **BSTR** 데이터 형식입니다.  
  
 ADO API 참조 메서드 또는 속성을 표시 하는 경우 사용 되는 **문자열** 값, 즉 값 형식으로 **_bstr_t**합니다.  
  
### <a name="casting-variantt-and-bstrt-classes"></a>캐스팅 _variant_t 및 _bstr_t 클래스  
 종종 필요한 경우가 아니라면 명시적으로 코드에는 **_variant_t** 또는 **_bstr_t** 인수에 작업입니다. 경우는 **_variant_t** 또는 **_bstr_t** 클래스에 생성자 인수 데이터 형식과 일치 하는, 컴파일러는 적절 한 생성 **_variant_t** 또는 **_bstr_t**합니다.  
  
 그러나 인수가 모호 합니다. 즉, 인수의 데이터 형식이 일치 둘 이상의 생성자, 올바른 생성자를 호출 하려면 적절 한 데이터 형식의 인수를 캐스팅 해야 합니다.  
  
 예를 들어에 대 한 선언을 **Recordset::Open** 방법은:  
  
```  
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```  
  
 `ActiveConnection` 인수에 대 한 참조에는 한 **_variant_t**, 연결 문자열 또는 열린에 대 한 포인터로 코딩할 수 있습니다는 **연결** 개체입니다.  
  
 올바른 **_variant_t** 와 같은 문자열을 전달 하는 경우 암시적으로 생성 될 "`DSN=pubs;uid=MyUserName;pwd=MyPassword;`", 또는와 같은 포인터 "`(IDispatch *) pConn`"입니다.  
  
> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 또는 **통합 보안 = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.  
  
 명시적으로 코딩할 수 있습니다 또는 **_variant_t** 대 한 포인터를 같은 포함 된 "`_variant_t((IDispatch *) pConn, true)`" 합니다. 캐스트를 `(IDispatch *)`는 IUnknown 인터페이스에 대 한 포인터를 사용 하는 다른 생성자를 사용 하는 모호성을 해결 합니다.  
  
 거의 된다는 사실에 입각, ADO의 IDispatch 인터페이스를 설명 하는 있지만 중요 합니다. 때마다 변수로 ADO 개체에 대 한 포인터를 전달 되어야 합니다는 **Variant**, 해당 포인터는 IDispatch 인터페이스에 대 한 포인터로 캐스팅 해야 합니다.  
  
 마지막 경우 선택적 기본값인의 생성자의 두 번째 부울 인수를 명시적으로 코딩 `true`합니다. 이 인수로 인해는 **Variant** 호출할 생성자를 해당 **AddRef**() 메서드를 자동으로 호출 하는 ADO에 대 한 보정는 **_variant_t::Release**() 메서드 ADO 메서드 또는 속성이 호출 하는 경우 완료 합니다.  
  
### <a name="safearray"></a>SafeArray  
 A **SafeArray** 는 다른 데이터 형식의 배열이 포함 된 구조적된 데이터 형식입니다. A **SafeArray** 라고 *안전* 각 배열 차원의 경계에 대 한 정보를 포함 하 고 해당 범위 내에서 배열 요소에 대 한 액세스를 제한 합니다.  
  
 때 ADO API 참조 표시는 메서드 또는 속성 하거나 배열을 반환, 의미 메서드 또는 속성 하거나 반환는 **SafeArray**, 네이티브 C/c + + 배열이 아닌 합니다.  
  
 두 번째 매개 변수 예를 들어는 **연결** 개체 **OpenSchema** 메서드를 사용 하려면 배열을 **Variant** 값입니다. 이러한 **Variant** 값의 요소 변수로 전달 되어야 합니다는 **SafeArray**, 하 고 **SafeArray** 다른 값으로 설정 되어야 합니다 **Variant** . 다른 **Variant** 의 두 번째 인수로 전달 되는 **OpenSchema**합니다.  
  
 대로 예제에서 첫 번째 인수는 **찾을** 메서드는 한 **Variant** 값이 1 차원 **SafeArray**각 선택적 첫 번째 및 두 번째 인수 **AddNew** 는 1 차원 **SafeArray**;의 반환 값과는 **GetRows** 메서드는 한 **Variant** 인 값은 2 차원 **SafeArray**합니다.  
  
## <a name="missing-and-default-parameters"></a>누락 된 및 기본 매개 변수  
 Visual Basic에서는 메서드에 매개 변수가 없습니다. 예를 들어는 **레코드 집합** 개체 **열려** 메서드에 5 개의 매개 변수가 있지만 중간 매개 변수를 건너뛰고 뒤에 매개 변수를 생략할 수 있습니다. 기본 **BSTR** 또는 **Variant** 누락 피연산자의 데이터 형식에 따라 대체 됩니다.  
  
 C/c + +에서는 모든 피연산자를 지정 해야 합니다. 데이터 형식이 문자열인 누락 된 매개 변수를 지정 하려는 경우, 지정 된 **_bstr_t** null 문자열을 포함 하 합니다. 누락 된 매개 변수 데이터 형식이 지정 하려는 경우는 **Variant**, 지정는 **_variant_t** DISP_E_PARAMNOTFOUND 및 VT_ERROR 유형의 값을 사용 합니다. 또는 해당 지정할 **_variant_t** 상수, **vtMissing**에서 제공 되는 **#import** 지시문입니다.  
  
 세 가지 메서드는 예외를 사용 하는 일반적인 **vtMissing**합니다. 이들은 **Execute** 의 메서드는 **연결** 및 **명령** 개체 및 **NextRecordset** 는 방식의**레코드 집합** 개체입니다. 대리자의 시그니처가 다음과 같습니다.  
  
```  
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```  
  
 매개 변수를 *RecordsAffected* 및 *매개 변수*에 대 한 포인터는 **Variant**합니다. *매개 변수* 의 주소를 지정 하는 입력 매개 변수는 **Variant** 하나만 포함 된 매개 변수 또는 매개 변수는 실행 중인 명령을 수정 하는 배열입니다. *RecordsAffected* 의 주소를 지정 하는 출력 매개 변수는 **Variant**메서드에 의해 영향을 받는 행 수가 반환 됩니다.  
  
 에 **명령** 개체 **Execute** 메서드를 설정 하 여 매개 변수가 지정 되어 있는지를 나타내는 *매개 변수* 을 `&vtMissing` (권장 됨) 또는 null 포인터 (즉, **NULL** 또는 영 (0)). 경우 *매개 변수* 설정 되어 null 포인터를 메서드가 내부적으로 대체 하는 것에 해당 **vtMissing**, 한 후 작업을 완료 합니다.  
  
 모든 방법에서 영향 받는 레코드 수를 설정 하 여 하지 반환 되어야 함을 나타내는 *RecordsAffected* null 포인터입니다. 이 경우 null 포인터 매개 변수가 아닙니다 정도로 누락 확인 메서드가 영향을 받는 레코드 수를 무시 해야 합니다.  
  
 다음 세 가지 방법에 대 한 즉와 같은 코딩 하 합니다.  
  
```  
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```  
  
## <a name="error-handling"></a>오류 처리  
 COM, 대부분의 작업 함수 완료 되었는지 여부를 나타내는 HRESULT 반환 코드를 반환 합니다. **#import** 지시문 주위 각 "원시" 메서드 또는 속성에 래퍼 코드를 생성 하 고 반환된 된 HRESULT를 확인 합니다. HRESULT 오류를 나타내는 래퍼 코드는 인수로 서 COM 오류를 HRESULT 반환 코드 _com_issue_errorex()를 호출 하 여 throw 합니다. COM 오류 개체에서 낼 수 있습니다는 **시도**-**catch** 블록입니다. (효율성의 위해서에 대 한 참조를 catch 한 **_com_error** 개체입니다.)  
  
 ADO 오류입니다: ADO 작업이 실패에서 하 여 발생 합니다. 기본 공급자에서 반환한 오류로 표시 **오류** 개체에 **연결** 개체 **오류** 컬렉션입니다.  
  
 **#import** 지시문 오류만 메서드와 ADO.dll에 선언 된 속성에 대 한 처리 루틴을 만듭니다. 그러나이 동일한 오류 처리 메커니즘을 직접 오류 매크로 또는 인라인 함수 검사를 작성 하 여 활용을 걸릴 수 있습니다. 항목을 참조 [Visual c + + 확장](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md), 또는 예제를 보려면 다음 섹션의 코드입니다.  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual Basic 규칙의 visual c + + 해당 항목  
 다음은 몇 가지 규칙으로 Visual Basic, Visual c + +에서에 해당 하는 코딩 된 ADO 설명서에 대 한 요약입니다.  
  
### <a name="declaring-an-ado-object"></a>ADO 개체를 선언합니다.  
 Visual basic에서는 ADO 개체 변수 (이 경우에 **레코드 집합** 개체) 다음과 같이 선언 됩니다.  
  
```  
Dim rst As ADODB.Recordset  
```  
  
 절을 사용 하면 "`ADODB.Recordset`"의 ProgID는는 **레코드 집합** 레지스트리에 정의 된 개체입니다. 새 인스턴스는 **레코드** 개체는 다음과 같이 선언 됩니다.  
  
```  
Dim rst As New ADODB.Recordset  
```  
  
 -또는-  
  
```  
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```  
  
 Visual c + +에서는 **#import** 지시어 모든 ADO 개체에 대 한 스마트 포인터 형식 선언을 생성 합니다. 예를 들어 가리키는 변수는 **_Recordset** 형식의 개체는 **_RecordsetPtr**, 다음과 같이 선언 됩니다.  
  
```  
_RecordsetPtr  rs;  
```  
  
 새 인스턴스를 가리키는 변수는 **_Recordset** 개체는 다음과 같이 선언 됩니다.  
  
```  
_RecordsetPtr  rs("ADODB.Recordset");  
```  
  
 -또는-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```  
  
 -또는-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```  
  
 이후에 **CreateInstance** 메서드가 호출 되 면 변수를 다음과 같이 사용할 수 있습니다.  
  
```  
rs->Open(...);  
```  
  
 한 가지 경우에서는 "`.`" 연산자 변수가 클래스의 인스턴스인 것 처럼 사용 됩니다 (`rs.CreateInstance`), 및 다른 경우에는 "`->`" 마치 것 처럼 변수는 인터페이스에 대 한 포인터 연산자가 사용 (`rs->Open`).  
  
 때문에 두 가지 방법으로 하나의 변수를 사용할 수 있습니다는 "`->`" 인터페이스에 대 한 포인터 처럼 동작 하는 클래스의 인스턴스를 연산자가 오버 로드 합니다. 인스턴스 변수 전용 클래스 멤버에 대 한 포인터에 포함 되어는 **_Recordset** 인터페이스는 "`->`" 연산자 반환 해당 포인터; 및 반환된 된 포인터의 멤버에 액세스는 **_Recordset**  개체입니다.  
  
### <a name="coding-a-missing-parameter--string"></a>누락 된 매개 변수 코딩-문자열  
 누락 된 코딩 해야 하는 경우 **문자열** 피연산자 Visual basic의 경우 단순히 피연산자가 생략 합니다. Visual c + +에서 피연산자를 지정 해야 합니다. 코드는 **_bstr_t** 있는 값으로 빈 문자열입니다.  
  
```  
_bstr_t strMissing(L"");  
```  
  
### <a name="coding-a-missing-parameter--variant"></a>누락 된 매개 변수 코딩-Variant  
 누락 된 코딩 해야 하는 경우 **Variant** 피연산자 Visual basic의 경우 단순히 피연산자가 생략 합니다. Visual c + +에서 모든 피연산자를 지정 해야 합니다. 누락 된 코드 **Variant** 매개 변수는 **_variant_t** 는 특수 값, DISP_E_PARAMNOTFOUND, 및 유형, VT_ERROR로 설정 합니다. 또는 지정할 **vtMissing**에서 제공 하는 해당 하는 미리 정의 된 상수는 **#import** 지시문입니다.  
  
```  
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```  
  
 또는 사용  
  
```  
...vtMissing...;  
```  
  
### <a name="declaring-a-variant"></a>Variant 선언  
 Visual Basic의 경우에 **Variant** 선언는 **Dim** 문은 다음과 같이:  
  
```  
Dim VariableName As Variant  
```  
  
 Visual c + +에서 형식으로 변수를 선언 **_variant_t**합니다. 몇 가지 구성도 **_variant_t** 선언은 다음과 같습니다.  
  
> [!NOTE]
>  대략적으로 프로그램에서 코드는 이러한 선언을 제공 합니다. 자세한 내용은 아래 예제 및 Visual C++ 설명서를 참조 하십시오.  
  
```  
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```  
  
### <a name="using-arrays-of-variants"></a>Variant의 배열 사용  
 Visual Basic의 배열에서 **변형** 으로 코딩 될 수 있습니다는 **Dim** 문 또는 있습니다 사용할 수는 **배열** 다음 예제 코드에서와 같이 함수:  
  
```  
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```  
  
 다음 Visual c + + 예제는 **SafeArray** 사용한는 **_variant_t**합니다.  
  
#### <a name="notes"></a>참고  
 다음 참고 코드 예제에서 주석 처리 된 섹션에 해당합니다.  
  
1.  다시 한 번 TESTHR() 인라인 함수는 기존 오류 처리 메커니즘을 활용 하도록 정의 됩니다.  
  
2.  하기만 하면 1 차원 배열에 사용할 수 있도록 **SafeArrayCreateVector**, 대신 일반 용도의 **SAFEARRAYBOUND** 선언 및 **SafeArrayCreate** 함수입니다. 다음은 해당 코드는 사용과 같은 표시 **SafeArrayCreate**:  
  
    ```  
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```  
  
3.  열거형된 상수인으로 식별 되는 스키마 **adSchemaColumns**, 4 개의 제약 조건 열과 연결 된: TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME 및 COLUMN_NAME 합니다. 따라서 배열을 **Variant** 네 가지 요소로 된 값이 생성 됩니다. 다음 세 번째 열인 TABLE_NAME에 해당 하는 제약 조건 값을 지정 합니다.  
  
     **레코드 집합** 반환 하는 하위 집합은 제약 조건 열, 여러 열으로 구성 됩니다. 반환 된 각 행에 대 한 제약 조건 열 값의 해당 제약 조건 값과 일치 해야 합니다.  
  
4.  익숙한 **SafeArrays** 될 수 있습니다는 달라진 **SafeArrayDestroy**종료 하기 전에 () 호출 되지 않습니다. 실제로 호출 **SafeArrayDestroy**()이 경우에 런타임 예외가 발생 합니다. 에 대 한 소멸자는 이유는 `vtCriteria` 호출 **VariantClear**() 때는 **_variant_t** 을 확보 범위를 벗어날는 **SafeArray**합니다. 호출 **SafeArrayDestroy**를 수동으로 지우는 없이 **_variant_t**, 잘못 된의 선택을 취소 하려고 소멸자로 인해 **SafeArray** 포인터입니다.  
  
     경우 **SafeArrayDestroy** 된 호출, 코드는 다음과 같습니다.  
  
    ```  
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```  
  
     그러나 것이 훨씬 간단 수 있도록는 **_variant_t** 관리는 **SafeArray**합니다.  
  
```  
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
 Visual Basic에서 속성의 이름은 되었는지 검색, 할당, 여부 참조를 할당 하 여 한정 되지 않습니다.  
  
```  
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```  
  
 이 Visual c + + 예제는 **가져오기**/**배치**/**PutRef * * * 속성*합니다.  
  
#### <a name="notes"></a>참고  
 다음 참고 코드 예제에서 주석 처리 된 섹션에 해당합니다.  
  
1.  이 예에서는 두 가지 형태의 문자열 인수 없음: 명시적 상수인 **strMissing**, 및 컴파일러에서 임시을 사용 하는 문자열로 **_bstr_t** 는 의범위에있는 **열기** 메서드.  
  
2.  피연산자를 캐스팅 필요 없는 `rs->PutRefActiveConnection(cn)` 를 `(IDispatch *)` 피연산자의 형식이 이미 `(IDispatch *)`합니다.  
  
```  
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
 이 Visual Basic 예제에서는 표준 구문과 대체 구문을 보여 주는 **항목**().  
  
```  
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```  
  
 이 Visual c + + 예제에서는 **항목**합니다.  
  
> [!NOTE]
>  다음 코드 예제에서 주석 처리 된 섹션에 해당: 컬렉션으로 액세스 하는 경우 **항목**, 인덱스, **2**,으로 캐스팅 해야 **긴** 하므로 적절 한 생성자가 호출 됩니다.  
  
```  
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
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>와 ADO 개체 포인터 캐스팅 (IDispatch *)  
 다음 Visual c + + 예제를 사용 하 여 보여 줍니다 (IDispatch *) 캐스트 ADO 개체 포인터에 대 한 합니다.  
  
#### <a name="notes"></a>참고  
 다음 참고 코드 예제에서 주석 처리 된 섹션에 해당합니다.  
  
1.  열린 지정 **연결** 개체에서 명시적으로 코딩 된 **Variant**합니다. 사용 하 여 캐스팅 (IDispatch \*) 올바른 생성자를 호출 합니다. 또한 명시적으로 설정 하 고 두 번째 **_variant_t** 매개 변수를 기본값인 **true**이므로 때 개체 참조 횟수 수정 될는 **Recordset::Open** 작업을 종료합니다.  
  
2.  식 `(_bstr_t)`, 캐스트 않습니다 하지만 **_variant_t** 추출 연산자는 **_bstr_t** 에서 문자열은 **Variant** 반환한 **값** .  
  
 식 `(char*)`, 캐스트 않습니다 하지만 **_bstr_t** 연산자에는 캡슐화 된 문자열에 대 한 포인터를 추출 하는 **_bstr_t** 개체입니다.  
  
 이 섹션의 코드의 유용한 동작이의 일부를 보여 줍니다 **_variant_t** 및 **_bstr_t** 연산자입니다.  
  
```  
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
