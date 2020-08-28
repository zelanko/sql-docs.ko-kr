---
description: Source 속성(ADO 레코드 집합)
title: Source 속성 (ADO 레코드 집합) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a71efe111a58ab8f799db512e77da4365ba5f48
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988904"
---
# <a name="source-property-ado-recordset"></a>Source 속성(ADO 레코드 집합)
[레코드 집합](./recordset-object-ado.md) 개체에 대 한 데이터 원본을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **문자열** 값 또는 [명령](./command-object-ado.md) 개체 참조를 설정 합니다. **레코드 집합**의 원본을 나타내는 **문자열** 값만 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Source** 속성을 사용 하 여 **명령** 개체 변수, SQL 문, 저장 프로시저 또는 테이블 이름 중 하나를 사용 하 여 **레코드 집합** 개체에 대 한 데이터 원본을 지정할 수 있습니다.  
  
 **Source** 속성을 **Command** 개체로 설정 하면 **레코드 집합** 개체의 [ActiveConnection](./activeconnection-property-ado.md) 속성이 지정 된 **명령** 개체의 **ActiveConnection** 속성 값을 상속 합니다. 그러나 **Source** 속성을 읽으면 **Command** 개체가 반환 되지 않습니다. 대신 **원본** 속성을 설정 하는 **Command** 개체의 [CommandText](./commandtext-property-ado.md) 속성을 반환 합니다.  
  
 **원본** 속성이 SQL 문, 저장 프로시저 또는 테이블 이름인 경우 [Open](./open-method-ado-recordset.md) 메서드 호출에 적절 한 *Options* 인수를 전달 하 여 성능을 최적화할 수 있습니다.  
  
 **원본** 속성은 닫힌 **레코드 집합** 개체에 대 한 읽기/쓰기이 고, 열려 있는 **레코드 집합** 개체에 대 한 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Source 속성 예제 (VB)](./source-property-example-vb.md)   
 [Source 속성 (ADO 오류)](./source-property-ado-error.md)   
 [Source 속성(ADO 레코드)](./source-property-ado-record.md)