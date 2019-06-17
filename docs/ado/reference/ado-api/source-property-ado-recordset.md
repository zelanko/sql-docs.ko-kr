---
title: Source 속성 (ADO 레코드 집합) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 59a043b6258de83986e447c87209fa781a1ae352
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711120"
---
# <a name="source-property-ado-recordset"></a>Source 속성(ADO 레코드 집합)
에 대 한 데이터 원본을 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 집합을 **문자열** 값 또는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체 참조가;만 반환를 **문자열** 의 소스를 나타내는 값을 **레코드 집합**.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **원본** 에 대 한 데이터 원본을 지정 하려면 속성을 **레코드 집합** 다음 중 하나를 사용 하 여 개체:를 **명령** 개체 변수, SQL 문, 저장된 프로시저를 또는 테이블 이름입니다.  
  
 설정 하는 경우를 **원본** 속성을를 **명령** 개체를 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 의 속성을 **레코드 집합** 개체가 상속 합니다는 값을 **ActiveConnection** 지정 된 속성 **명령** 개체입니다. 그러나 읽기를 **원본** 속성을 반환 하지 않습니다를 **명령** 개체; 대신 반환 합니다를 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성은 **명령** 를 설정 하는 개체를 **소스** 속성입니다.  
  
 경우는 **소스** 속성은 SQL 문, 저장된 프로시저 또는 테이블 이름, 적절 한 전달 하 여 성능을 최적화할 수 있습니다 *옵션* 인수를는 [엽니다](../../../ado/reference/ado-api/open-method-ado-recordset.md)메서드를 호출 합니다.  
  
 **원본** 종료에 대 한 속성은 읽기/쓰기 **Recordset** 개체 및 읽기 전용 열기에 대 한 **레코드 집합** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Source 속성 예제 (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Source 속성 (ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 속성(ADO 레코드)](../../../ado/reference/ado-api/source-property-ado-record.md)
