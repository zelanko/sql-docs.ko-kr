---
title: ParentURL 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4a0217d4f2e79dc5876af9518a06d73d2ac924d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280684"
---
# <a name="parenturl-property-ado"></a>ParentURL 속성 (ADO)
부모를 가리키는 절대 URL 문자열을 나타내고 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 현재 **레코드** 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **문자열** 부모 URL을 나타내는 값 **레코드**합니다.  
  
## <a name="remarks"></a>Remarks  
 **ParentURL** 속성 여는 데 사용 하는 소스에 따라 다릅니다.는 **레코드** 개체입니다. 예를 들어는 **레코드** 에서 참조 하는 디렉터리의 상대 경로 이름을 포함 하는 원본으로 열 수는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성입니다.  
  
 가정 폴더 "first"에서 "두 번째" 포함 되어 있습니다. 열기는 **레코드** 다음 구문을 사용 하 여 개체:  
  
```  
record.ActiveConnection = "http://first"  
record.Open "second"  
```  
  
 값에 이제 `the` **ParentURL** 속성은 `"http://first"`, 동일 **ActiveConnection**합니다.  
  
 소스 수도 있습니다는 절대 URL와 같은 `"http://first/second"`합니다. **ParentURL** 속성은 다음 `"http://first"`, 상위 수준 `"second"`합니다.  
  
 이 속성 경우 null 값이 될 수 있습니다.  
  
-   현재 개체;에 대 한 부모인 예를 들어 경우는 **레코드** 개체는 디렉터리의 루트를 나타냅니다.  
  
-   **레코드** 개체는 url을 지정할 수 없는 엔터티를 나타냅니다.  
  
 이 속성은 읽기 전용입니다.  
  
> [!NOTE]
>  이 속성은 문서 소스 공급자에서와 같은 지원만 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [레코드 및 필드 공급자 제공](../../../ado/guide/data/records-and-provider-supplied-fields.md)합니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
> [!NOTE]
>  현재 레코드에서 ADO 데이터 레코드를 포함 하는 경우 **레코드 집합**, 액세스 하는 **ParentURL** URL이 가능 함을 나타내는 런타임 오류를 발생 시키는 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)
