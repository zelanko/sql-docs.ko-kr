---
description: Execute 메서드(ADO 명령)
title: Execute 메서드 (ADO 명령) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
author: rothja
ms.author: jroth
ms.openlocfilehash: 5bd7e8d98f7d7ccecfce2ce66852f92efa1dae77
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973514"
---
# <a name="execute-method-ado-command"></a>Execute 메서드(ADO 명령)
[명령 개체](../../../ado/reference/ado-api/command-object-ado.md)의 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 또는 [commandstream](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성에 지정 된 쿼리, SQL 문 또는 저장 프로시저를 실행 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>Return Value  
 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 참조, 스트림 또는 **Nothing**을 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *RecordsAffected*  
 선택 사항입니다. 공급자가 작업에서 영향을 받은 레코드 수를 반환 하는 **Long** 변수입니다. *RecordsAffected* 매개 변수는 동작 쿼리 또는 저장 프로시저에만 적용 됩니다. *RecordsAffected* 는 결과가 반환 하는 쿼리 또는 저장 프로시저에서 반환 된 레코드 수를 반환 하지 않습니다. 이 정보를 얻으려면 [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) 속성을 사용 합니다. 명령이 비동기적으로 실행 될 때 영향을 받는 레코드의 수는 메서드가 반환 될 때 아직 알려지지 않을 수 있기 때문에 **execute** 메서드는 **adasyncexecute**와 함께 사용 될 때 올바른 정보를 반환 하지 않습니다.  
  
 *매개 변수*  
 선택 사항입니다. **CommandText** 또는 **commandstream**에 지정 된 입력 문자열 또는 스트림과 함께 사용 되는 매개 변수 값의 **Variant** 배열입니다. 출력 매개 변수는이 인수에 전달 될 때 올바른 값을 반환 하지 않습니다.  
  
 *Options*  
 선택 사항입니다. 공급자가 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체의 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 또는 [commandstream](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성을 평가 하는 방법을 나타내는 **Long** 값입니다. [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 및/또는 [executevalue 열거형](../../../ado/reference/ado-api/executeoptionenum.md) 값을 사용 하 여 만든 비트 마스크 값일 수 있습니다. 예를 들어 ADO에서 **CommandText** 속성의 값을 텍스트로 평가 하 고 명령 텍스트가 실행 될 때 생성 될 수 있는 레코드를 반환 하지 않아야 함을 나타내려면 **adcmdtext** 및 **adExecuteNoRecords** 를 조합 하 여 사용할 수 있습니다.  
  
> [!NOTE]
>  내부 처리를 최소화 하 여 성능을 향상 시키려면 **ExecuteadExecuteNoRecords 열거형** 값을 사용 합니다. **adExecuteNoRecords** **AdExecuteStream** 가 지정 된 경우 **adasyncfetch** 및 **adAsynchFetchNonBlocking** 옵션이 무시 됩니다. **Adcmdfile** 또는 **adCmdTableDirect** 의 **CommandTypeEnum** 값을 **Execute**와 함께 사용 하지 마세요. 이러한 값은 **레코드 집합**의 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 및 [Requery](../../../ado/reference/ado-api/requery-method.md) 메서드에서 옵션 으로만 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **명령** 개체에 **Execute** 메서드를 사용 하면 개체의 **CommandText** 속성 또는 **commandstream** 속성에 지정 된 쿼리가 실행 됩니다.  
  
 결과는 **레코드 집합** (기본적으로) 또는 이진 정보의 스트림으로 반환 됩니다. 이진 스트림을 가져오려면 *옵션*에 **adExecuteStream** 을 지정 하 고 **Command. Properties ("Output stream")** 를 설정 하 여 스트림을 제공 합니다. 결과를 수신 하기 위해 ADO **스트림** 개체를 지정 하거나 IIS 응답 개체와 같은 다른 스트림 개체를 지정할 수 있습니다. **AdExecuteStream**를 사용 하 여 **Execute** 를 호출 하기 전에 스트림을 지정 하지 않은 경우 오류가 발생 합니다. **Execute** 에서 반환 되는 스트림의 위치는 공급자별로 다릅니다.  
  
 명령이 결과를 반환 하기에 적합 하지 않은 경우 (예: SQL 업데이트 쿼리) **adExecuteNoRecords** 옵션이 지정 된 경우에는 공급자가 **아무 것도** 반환 하지 않습니다. 그렇지 않으면 Execute는 닫힌 **레코드 집합**을 반환 합니다. 일부 응용 프로그램 언어에서는 **레코드 집합** 을 사용할 수 없는 경우이 반환 값을 무시할 수 있습니다.  
  
 **CommandType** 이 **adCmdStoredProc**, **adcmdtable**또는 **adCmdTableDirect**일 때 **commandstream** 에 대 한 값을 지정 하는 경우 **Execute** 가 오류를 발생 시킵니다.  
  
 쿼리에 매개 변수가 있는 경우 **Execute** 호출에 전달 된 매개 변수 값으로 재정의 하지 않으면 **Command** 개체의 매개 변수에 대 한 현재 값이 사용 됩니다. **Execute** 메서드를 호출할 때 일부 매개 변수의 새 값을 생략 하 여 매개 변수의 하위 집합을 재정의할 수 있습니다. 매개 변수를 지정 하는 순서는 메서드가 해당 매개 변수를 전달 하는 순서와 동일 합니다. 예를 들어 4 개 이상의 매개 변수가 있고 첫 번째와 네 번째 매개 변수에 대해서만 새 값을 전달 하려는 경우 `Array(var1,,,var4)` *매개 변수* 인수로를 전달 합니다.  
  
> [!NOTE]
>  Output 매개 변수는 *parameters* 인수에 전달 될 때 올바른 값을 반환 하지 않습니다.  
  
 이 작업이 완료 되 면 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) 이벤트가 발생 합니다.  
  
> [!NOTE]
>  Url을 포함 하는 명령을 실행 하는 경우 http 체계를 사용 하는 명령은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Execute, Requery 및 Clear 메서드 예제 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery 및 Clear 메서드 예제 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery 및 Clear 메서드 예제 (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandStream 속성 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Execute 메서드 (ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete 이벤트(ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
