---
title: "Source 속성 (ADO 레코드 집합) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::putref_Source
- Recordset15::Source
- Recordset15::PutSource
- Recordset15::get_Source
- Recordset15::GetSource
- Recordset15::PutRefSource
- Recordset15::put_Source
helpviewer_keywords:
- Source property [ADO Recordset]
ms.assetid: a05ba2c9-2821-4343-8607-4de9b764ec91
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ea45eae107fa55355adeb195e7e4fc5cf0a3c762
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="source-property-ado-recordset"></a>Source 속성 (ADO 레코드 집합)
에 대 한 데이터 원본을 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 집합은 **문자열** 값 또는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체 참조가;만 반환는 **문자열** 의 소스를 나타내는 값은 **레코드 집합**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **소스** 속성에 대 한 데이터 원본을 지정 하는 **레코드 집합** 개체는 다음 중 하나를 사용 하 여:는 **명령** 개체 변수, SQL 문, 저장된 프로시저 또는 테이블 이름입니다.  
  
 설정 하는 경우는 **소스** 속성을는 **명령** 개체는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 의 속성에서 **레코드 집합** 개체가 상속 합니다는 값은 **ActiveConnection** 속성에서 지정 된 **명령** 개체입니다. 그러나 읽기는 **소스** 속성을 반환 하지 않습니다는 **명령** 대신 반환; 개체는 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성의는 **명령** 개체를 설정 하는 **소스** 속성입니다.  
  
 경우는 **소스** 속성은 SQL 문, 저장된 프로시저 또는 테이블 이름, 적절 한 전달 하 여 성능을 최적화할 수 있습니다 *옵션* 인수를는 [열고](../../../ado/reference/ado-api/open-method-ado-recordset.md)메서드를 호출 합니다.  
  
 **소스** 종료에 대 한 속성은 읽기/쓰기 **레코드 집합** 개체 읽기 전용 및 열기에 대 한 **레코드 집합** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [원본 속성 예제 (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Source 속성 (ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 속성(ADO 레코드)](../../../ado/reference/ado-api/source-property-ado-record.md)

