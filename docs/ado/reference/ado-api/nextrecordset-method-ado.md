---
description: NextRecordset 메서드(ADO)
title: NextRecordset 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
author: rothja
ms.author: jroth
ms.openlocfilehash: 8ec3bb3a6c5f7e4f6d6654ca059e7ace7d97d9da
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443095"
---
# <a name="nextrecordset-method-ado"></a>NextRecordset 메서드(ADO)
현재 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 지우고 일련의 명령으로 이동 하 여 다음 **레코드 집합** 을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>Return Value  
 **레코드 집합** 개체를 반환 합니다. 구문 모델에서 *recordset1* 및 *Recordset2* 는 동일한 **레코드 집합** 개체 이거나 개별 개체를 사용할 수 있습니다. 별도의 **레코드 집합** 개체를 사용 하는 경우 **NextRecordset** 를 호출한 후 원래 **레코드 집합** (*recordset1*)에서 **ActiveConnection** 속성을 다시 설정 하면 오류가 발생 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *RecordsAffected*  
 (선택 사항) 공급자가 현재 작업에 영향을 받은 레코드 수를 반환 하는 **Long** 변수입니다.  
  
> [!NOTE]
>  이 매개 변수는 작업의 영향을 받는 레코드 수를 반환 합니다. 레코드 **집합**을 생성 하는 데 사용 되는 select 문에서 레코드 수를 반환 하지 않습니다.  
  
## <a name="remarks"></a>설명  
 **NextRecordset** 메서드를 사용 하 여 여러 결과를 반환 하는 복합 명령 문이나 저장 프로시저에서 다음 명령의 결과를 반환 합니다. 복합 명령 문 (예: "table1에서 선택")을 기반으로 하 여 **레코드 집합** 개체를 열 경우 \* SELECT \* FROM table2 ") [명령](../../../ado/reference/ado-api/command-object-ado.md) 에 대해 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드를 사용 하거나 **레코드 집합**의 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드를 사용 하 여 ADO는 첫 번째 명령만 실행 하 고 결과를 *레코드 집합*으로 반환 합니다. 문의 후속 명령에 대 한 결과에 액세스 하려면 **NextRecordset** 메서드를 호출 합니다.  
  
 추가 결과가 있고 복합 문을 포함 하는 **레코드 집합이** 프로세스 경계를 넘어 연결 되지 않거나 마샬링되는 경우 **NextRecordset** 메서드는 계속 해 서 **레코드 집합** 개체를 반환 합니다. 행 반환 명령이 성공적으로 실행 되지만 레코드를 반환 하지 않는 경우 반환 되는 **레코드 집합** 개체는 열려 있지만 비어 있습니다. [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 및 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성이 모두 **True**인지 확인 하 여이 사례를 테스트 합니다. 행을 반환 하지 않는 명령이 성공적으로 실행 되 면 반환 되는 **레코드 집합** 개체가 닫힙니다 .이는 **레코드 집합**에서 [State](../../../ado/reference/ado-api/state-property-ado.md) 속성을 테스트 하 여 확인할 수 있습니다. 결과가 더 이상 없는 경우에는 *레코드* 집합을 *Nothing*으로 설정 합니다.  
  
 **NextRecordset** 메서드는 연결이 끊어진 **레코드 집합** 개체에서 사용할 수 없습니다. 여기서 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 은 **Nothing** (Microsoft Visual Basic) 또는 NULL (다른 언어)로 설정 되어 있습니다.  
  
 즉시 업데이트 모드에서 편집이 진행 중인 경우 **NextRecordset** 메서드를 호출 하면 오류가 발생 합니다. [Update](../../../ado/reference/ado-api/update-method.md) 또는 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드를 먼저 호출 합니다.  
  
 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션을 채우거 나 원래 **Open** 또는 **Execute** 호출로 배열을 전달 하 여 복합 문에서 둘 이상의 명령에 대 한 매개 변수를 전달 하려면 매개 변수가 컬렉션 또는 배열에서 명령 계열의 각 명령과 동일한 순서 여야 합니다. 출력 매개 변수 값을 읽기 전에 모든 결과의 읽기를 완료 해야 합니다.  
  
 OLE DB 공급자는 복합 문의 각 명령이 실행 되는 시기를 결정 합니다. 예를 들어 [SQL Server에 대 한 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)는 복합 문을 받을 때 일괄 처리의 모든 명령을 실행 합니다. 결과 **레코드 집합** 은 **NextRecordset**를 호출할 때 반환 됩니다.  
  
 그러나 NextRecordset가 호출 된 후에 다른 공급자가 문에서 다음 명령을 실행할 수 있습니다. 이러한 공급자의 경우 전체 명령 문을 실행 하기 전에 **레코드 집합** 개체를 명시적으로 닫으면 ADO는 나머지 명령을 실행 하지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [NextRecordset 메서드 예제 (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [NextRecordset 메서드 예제(VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
