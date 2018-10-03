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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b053fdeae5016d7a1b489133b3a26067da7eab2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47803051"
---
# <a name="source-property-ado-record"></a>Source 속성(ADO 레코드)
데이터 소스를 나타내는 개체를 나타내는 합니다 [레코드](../../../ado/reference/ado-api/record-object-ado.md)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 **Variant** 가 나타내는 엔터티를 나타내는 값을 **레코드**합니다.  
  
## <a name="remarks"></a>Remarks  
 **원본** 속성에서 반환 합니다 *원본* 인수의 **레코드** 개체 [열기](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드. 절대 또는 상대 URL 문자열을 포함할 수 있습니다. 절대 URL을 설정 하지 않고 사용할 수는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성을 직접 열을 **레코드** 개체입니다. 암시적인 **연결** 개체가 경우에 생성 됩니다.  
  
 합니다 **원본** 속성에 대 한 참조를 포함할 수도 있습니다 **레코드 집합**, 열리는 **레코드** 의 현재 행을 나타내는 개체를  **레코드 집합**합니다.  
  
 합니다 **소스** 속성에 대 한 참조를 포함할 수 있습니다를 [명령](../../../ado/reference/ado-api/command-object-ado.md) 공급자에서 데이터의 단일 행을 반환 하는 개체입니다.  
  
 경우는 **ActiveConnection** 속성이 설정 된 경우 **원본** 속성은 해당 연결의 범위 내에 있는 일부 개체를 가리켜야 합니다. 예를 들어, 트리 구조 네임 스페이스의에서 경우는 **원본** 절대 URL을 포함 하는 속성, 연결 문자열에 대 한 URL로 식별 된 노드 범위 내에 있는 노드를 가리키도록 해야 합니다. 경우는 **소스** 상대 URL을 포함 하는 속성을 설정한 컨텍스트 내에서 유효성이 검사 되는 **ActiveConnection** 속성입니다.  
  
 **원본** 속성은 읽기/쓰기 동안는 **레코드** 개체는 닫히지 않고 읽기 전용 이지만 **레코드** 개체가 열려.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Source 속성 (ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 속성(ADO 레코드 집합)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
