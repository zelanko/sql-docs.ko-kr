---
title: GetString 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
author: rothja
ms.author: jroth
ms.openlocfilehash: 166bfad93d994a4b85bdb944a5d5505987182044
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758749"
---
# <a name="getstring-method-ado"></a>GetString 메서드(ADO)
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 문자열로 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>Return Value  
 **레코드 집합** 을 문자열 반환 **Variant** (BSTR)로 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *StringFormat*  
 **레코드 집합** 을 문자열로 변환 하는 방법을 지정 하는 [stringformatenum](../../../ado/reference/ado-api/stringformatenum.md) 값입니다. *Rowdelimiter*, *Columndelimiter*및 *Nullexpr* 매개 변수는 **adClipString**의 *StringFormat* 사용 됩니다.  
  
 *NumRows*  
 (선택 사항) **레코드 집합**에서 변환할 행의 수입니다. *Numrows* 를 지정 하지 않거나 **레코드 집합**에 있는 행의 총 수보다 큰 경우에는 **레코드 집합** 의 모든 행이 변환 됩니다.  
  
 *ColumnDelimiter*  
 (선택 사항) 열 사이에 사용 되는 구분 기호입니다 (지정 된 경우). 그렇지 않으면 탭 문자입니다.  
  
 *RowDelimiter*  
 (선택 사항) 행 사이에 사용 되는 구분 기호입니다 (지정 된 경우). 그렇지 않으면 캐리지 리턴 문자가 사용 됩니다.  
  
 *NullExpr*  
 (선택 사항) Null 값 대신 사용 되는 식입니다 (지정 된 경우). 그렇지 않으면 빈 문자열입니다.  
  
## <a name="remarks"></a>설명  
 행 데이터는 있지만 스키마 데이터는 문자열에 저장 되지 않습니다. 따라서이 문자열을 사용 하 여 **레코드 집합** 을 다시 열 수 없습니다.  
  
 이 메서드는 RDO **GetClipString** 메서드와 동일 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [GetString 메서드 예제(VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
