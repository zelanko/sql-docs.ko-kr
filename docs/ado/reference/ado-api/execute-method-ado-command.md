---
title: Execute 메서드 (ADO 명령) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9508b85bc73ebbec82ad7d3bea5af5148d7c674
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184801"
---
# <a name="execute-method-ado-command"></a>Execute 메서드(ADO 명령)
쿼리, SQL 문 또는 저장된 프로시저에 지정 된 실행 합니다 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 또는 [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성을 [명령 개체](../../../ado/reference/ado-api/command-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 참조, 스트림, 또는 **Nothing**합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *RecordsAffected*  
 (선택 사항) A **긴** 하려는 변수 공급자 작업에 영향을 받는 레코드 수를 반환 합니다. 합니다 *RecordsAffected* 매개 변수는 작업 쿼리 또는 저장된 프로시저에만 적용 됩니다. *RecordsAffected* 결과 반환 쿼리 또는 저장된 프로시저에서 반환 된 레코드의 수를 반환 하지 않습니다. 이 정보를 가져오려면 합니다 [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) 속성입니다. 합니다 **Execute** 메서드는 함께 사용할 경우 올바른 정보를 반환 하지 것입니다 **adAsyncExecute**, 단순히 경우 명령을 비동기적으로 실행 하 고, 영향을 받는 레코드 수를 아직 알 수 없습니다 시간에 메서드를 반환합니다.  
  
 *매개 변수*  
 (선택 사항) A **Variant** 입력된 문자열에서 지정 된 스트림에와 함께 사용 하는 매개 변수 값의 배열 **CommandText** 하거나 **CommandStream**합니다. (출력 매개 변수에 올바른 값이이 인수에 전달 될 때 반환 하지 않습니다.)  
  
 *Options*  
 (선택 사항) **긴** 공급자를 평가 해야 하는 방법을 나타내는 값을 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 또는 [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) 속성을 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다. 사용 하 여 비트 마스크 값일 수 있습니다 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 및/또는 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 값입니다. 예를 들어 사용할 수 있습니다 **adCmdText** 하 고 **adExecuteNoRecords** 조합 ADO의 값을 평가 하려는 경우에 **CommandText** 텍스트로 속성 및 명령을 삭제 하 고 명령 텍스트를 실행 하는 경우 발생할 수 있는 레코드를 반환 하지 해야 나타냅니다.  
  
> [!NOTE]
>  사용 된 **ExecuteOptionEnum** 값 **adExecuteNoRecords** 내부 처리를 최소화 하 여 성능 향상을 위해. 하는 경우 **adExecuteStream** 지정 된 옵션 **adAsyncFetch** 하 고 **adAsynchFetchNonBlocking** 무시 됩니다. 사용 하지 않는 합니다 **CommandTypeEnum** 의 값 **adCmdFile** 또는 **adCmdTableDirect** 사용 하 여 **Execute**합니다. 옵션으로 이러한 값만 사용할 수 있습니다는 [엽니다](../../../ado/reference/ado-api/open-method-ado-recordset.md) 및 [Requery](../../../ado/reference/ado-api/requery-method.md) 의 메서드를 **레코드 집합**합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여를 **Execute** 메서드를 **명령** 개체에 지정 된 쿼리를 실행 합니다 **CommandText** 속성 또는 **CommandStream** 개체의 속성입니다.  
  
 결과가 반환 됩니다는 **레코드 집합** (기본적으로) 또는 이진 정보 스트림으로. 이진 스트림에 가져오려면 지정 **adExecuteStream** 에서 *옵션*를 설정 하 여 입력 스트림을 **Command.Properties ("출력 Stream")**. ADO **Stream** 결과 받을 개체를 지정할 수 있습니다 또는 IIS 응답 개체와 같은 다른 스트림 개체를 지정할 수 있습니다. 스트림이 없습니다 호출 하기 전에 지정 된 경우 **Execute** 사용 하 여 **adExecuteStream**, 오류가 발생 합니다. 반환 된 스트림의 위치 **Execute** 공급자 다릅니다.  
  
 공급자가 반환 하는 경우 명령을 아닙니다 (예를 들어 SQL 업데이트 쿼리) 결과를 반환 **아무** 옵션으로 긴 **adExecuteNoRecords** 지정; 그렇지 않으면 반환을 실행는 닫힌 **레코드 집합**합니다. 일부 응용 프로그램 언어가 없으면 반환 값이 무시 하면 **레코드 집합** 이 필요 합니다.  
  
 **실행** 사용자에 대 한 값을 지정 하는 경우 오류를 발생 시킵니다 **CommandStream** 때의 **CommandType** 됩니다 **adCmdStoredProc**,  **adCmdTable**, 또는 **adCmdTableDirect**합니다.  
  
 현재 값에 대 한 쿼리 매개 변수가 합니다 **명령** 함께 전달 된 매개 변수 값을 사용 하 여이 재정의 하지 않는 한 개체의 매개 변수를 사용 합니다 **Execute** 호출 합니다. 호출할 때 매개 변수 중 일부에 대 한 새 값을 생략 하면 매개 변수의 하위 집합을 재정의할 수 있습니다 합니다 **Execute** 메서드. 매개 변수를 지정 하는 순서가 메서드에 전달 하는 순서와 동일 합니다. 예를 들어 첫 번째 및 네 번째 매개 변수에 새 값을 전달 하려는 전달 하는 4 개 (이상) 매개 변수가 `Array(var1,,,var4)` 으로 *매개 변수* 인수입니다.  
  
> [!NOTE]
>  출력 매개 변수에서 전달 될 때 올바른 값을 반환 하지 것입니다 합니다 *매개 변수* 인수입니다.  
  
 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) 이 작업이 때 이벤트가 발생 합니다.  
  
> [!NOTE]
>  Url을 포함 하는 명령 실행, http 체계를 사용 하 여 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [실행, requery, Clear 메서드 예제 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [실행, requery, Clear 메서드 예제 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, requery, Clear 메서드 예제 (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandStream 속성 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Execute 메서드 (ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete 이벤트(ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
