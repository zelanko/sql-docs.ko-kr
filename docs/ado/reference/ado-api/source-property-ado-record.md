---
title: Source 속성 (ADO 레코드) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::Source
- _Record::PutRefSource
- _Record::GetSource
- _Record::put_Source
- _Record::putref_Source
- _Record::get_Source
helpviewer_keywords:
- Source property [ADO Record]
ms.assetid: 2c18279e-6f35-4af0-b12e-8f1543d9ed20
author: rothja
ms.author: jroth
ms.openlocfilehash: 32b329d8365370560f51503129ac2c8d85517527
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759819"
---
# <a name="source-property-ado-record"></a>Source 속성(ADO 레코드)
[레코드로](../../../ado/reference/ado-api/record-object-ado.md)표시 되는 데이터 소스 또는 개체를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **레코드가**나타내는 엔터티를 나타내는 **Variant** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Source** 속성은 **Record** 개체 [Open](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드의 *원본* 인수를 반환 합니다. 절대 URL 또는 상대 URL 문자열을 포함할 수 있습니다. [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성을 설정 하지 않고 **Record** 개체를 직접 열려면 절대 URL을 사용할 수 있습니다. 이 경우에는 암시적 **연결** 개체가 생성 됩니다.  
  
 **원본** 속성에는 이미 열려 있는 레코드 **집합**에 대 한 참조도 포함 될 수 있습니다. 그러면 레코드 **집합**의 현재 행을 나타내는 **Record** 개체가 열립니다.  
  
 **원본** 속성에는 공급자의 단일 데이터 행을 반환 하는 [Command](../../../ado/reference/ado-api/command-object-ado.md) 개체에 대 한 참조도 포함 될 수 있습니다.  
  
 **ActiveConnection** 속성도 설정 된 경우 **Source** 속성은 해당 연결의 범위 내에 있는 일부 개체를 가리켜야 합니다. 예를 들어 트리 구조 네임 스페이스에서 **Source** 속성이 절대 url을 포함 하는 경우 연결 문자열에서 url로 식별 되는 노드의 범위 내에 있는 노드를 가리켜야 합니다. **원본** 속성에 상대 URL이 포함 된 경우 **ActiveConnection** 속성에 의해 설정 된 컨텍스트 내에서 유효성 검사가 수행 됩니다.  
  
 **Record 개체가** 닫혀 있는 동안에는 **원본** 속성이 읽기/쓰기이 고 **record** 개체가 열려 있는 동안에는 읽기 전용입니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Source 속성 (ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 속성(ADO 레코드 집합)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
