---
title: Source 속성 (ADO 레코드) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc3c0abd277bee41dc22c700d735f54c2914458a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="source-property-ado-record"></a>Source 속성 (ADO 레코드)
데이터 원본이 나가 나타내는 개체를 나타냅니다는 [레코드](../../../ado/reference/ado-api/record-object-ado.md)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **Variant** 가 나타내는 엔터티를 나타내는 값의 **레코드**합니다.  
  
## <a name="remarks"></a>주의  
 **소스** 속성에서 반환 된 *소스* 의 인수는 **레코드** 개체 [열려](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드. 절대 또는 상대 URL 문자열을 포함할 수 있습니다. 절대 URL을 설정 하지 않고 사용할 수는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성을 직접 열어서는 **레코드** 개체입니다. 암시적 **연결** 개체가 경우에 생성 됩니다.  
  
 **소스** 속성에 대 한 참조를 포함할 수도 있습니다 **레코드 집합**, 열립니다는 **레코드** 의 현재 행을 나타내는 개체는  **레코드 집합**합니다.  
  
 **소스** 속성에 대 한 참조를 포함할 수도 수는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체는 공급자에서 데이터의 단일 행을 반환 합니다.  
  
 경우는 **ActiveConnection** 속성이 설정 된 경우 **소스** 속성 해당 연결의 범위 내에 있는 일부 개체를 가리켜야 합니다. 예를 들어, 트리 구조 네임 스페이스의에서 경우는 **소스** 절대 URL을 포함 하는 속성, 연결 문자열에 URL이 나타내는 노드의 범위 내에 있는 노드를 가리켜야 합니다. 경우는 **소스** 설정한 컨텍스트 내에서 유효성을 검사 한 다음 상대 URL을 포함 하는 속성은 **ActiveConnection** 속성입니다.  
  
 **소스** 속성은 읽기/쓰기 하는 동안는 **레코드** 개체 닫혀 있고 하는 동안 읽기 전용는 **레코드** 개체가 열려 있습니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Source 속성 (ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 속성(ADO 레코드 집합)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
