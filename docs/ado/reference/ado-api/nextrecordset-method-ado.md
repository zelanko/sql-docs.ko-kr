---
title: NextRecordset 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1df02b14168a15f9bccc476b62583334b2f0c3f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35279642"
---
# <a name="nextrecordset-method-ado"></a>NextRecordset 메서드 (ADO)
현재 지웁니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 하 고 다음 반환 **레코드 집합** 는 일련의 명령을 통해 이동 하 여 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **레코드 집합** 개체입니다. 구문 모델에서 *recordset1* 및 *recordset2* 동일할 수 **레코드 집합** 개체 또는 있습니다 별도 개체를 사용할 수 있습니다. 별도 사용 하는 경우 **레코드 집합** 개체를 다시 설정 하는 **ActiveConnection** 속성을 원래 **레코드 집합** (*recordset1*) 후 **NextRecordset** 가 호출한 오류를 생성 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *RecordsAffected*  
 (선택 사항) A **긴** 있는 변수 공급자 현재 작업이 영향 받는 레코드 수를 반환 합니다.  
  
> [!NOTE]
>  이 매개 변수는 작업에서 영향 받는 레코드 수 반환 생성 하는 데 사용 하는 select 문의 레코드 수를 반환 하지 않습니다는 **레코드 집합**합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **NextRecordset** 메서드 복합 명령문의 다음 명령 또는 여러 결과 반환 하는 저장된 프로시저의 결과를 반환 합니다. 여는 경우는 **레코드 집합** 복합 명령문을 기반으로 하는 개체 (예를 들어, "선택 \* table1;에서 선택 \* table2에서 ")를 사용 하 여는 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드를 한 [명령](../../../ado/reference/ado-api/command-object-ado.md) 또는 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 에서 메서드는 **레코드 집합**, 만 첫 번째 명령은 실행 하 고 결과 반환 하는 ADO *레코드 집합*합니다. 호출 문에서 후속 명령의 결과 액세스 하려면는 **NextRecordset** 메서드.  
  
 추가 결과가 있음을으로 및 **레코드 집합** 복합 문을 포함 하지 연결 되어 있지 않거나 프로세스 경계를 넘어 마샬링할는 **NextRecordset** 메서드는 계속 반환할 **레코드 집합** 개체입니다. 행을 반환 하는 명령 실행 되지만 반환 된 없는 레코드를 반환 하는 경우 **레코드 집합** 열려 있지만 빈 개체 수입니다. 있는지 확인 하 여이 경우에 대 한 테스트는 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 및 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성은 모두 **True**합니다. 행 반환 하지 않는 명령 반환 된 성공적으로 실행 하는 경우 **레코드 집합** 개체는 닫히고, 테스트 하 여 확인할 수 있는 [상태](../../../ado/reference/ado-api/state-property-ado.md) 속성에는 **레코드 집합**. 더 이상 결과가 없는 경우 *레코드 집합* 로 설정 됩니다 *Nothing*합니다.  
  
 **NextRecordset** 메서드에서 사용할 수 없으면 연결이 끊긴 **레코드 집합** 개체를 여기서 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 가로 설정 된 **Nothing**(Microsoft Visual Basic) 또는 NULL (의 경우 다른 언어의 경우).  
  
 편집 하는 즉시 업데이트 모드에 있는 동안 진행 중인 경우 호출는 **NextRecordset** 오류가 발생; 호출는 [업데이트](../../../ado/reference/ado-api/update-method.md) 또는 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드 첫 번째입니다.  
  
 입력 하 여 복합 문에서 둘 이상의 명령에 대 한 매개 변수를 전달 하는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션 또는 원래 배열을 전달 함으로써 **열려** 또는 **Execute** 호출에서 각 명령의 명령 시리즈의 컬렉션 또는 배열의 같은 순서로 매개 변수 여야 합니다. 출력 매개 변수 값을 읽기 전에 모든 결과 읽기를 완료 해야 합니다.  
  
 OLE DB 공급자는 복합 문이 각 명령이 실행 되는 시기를 결정 합니다. [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), 예를 들어 복합 문을 받으면 일괄 처리에서 모든 명령을 실행 합니다. 그 결과 **레코드 집합** 호출 하는 경우 단순히 반환될지 **NextRecordset**합니다.  
  
 그러나 다른 공급자 NextRecordset 호출 된 후에 문에서 다음 명령을 실행할 수 있습니다. 명시적으로 닫으면 이러한 공급자는 **레코드 집합** 전체 명령문을 단계별로 실행 하기 전에 개체 ADO에 나머지 명령을 실행 하지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [NextRecordset 메서드 예제 (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [NextRecordset 메서드 예제(VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
