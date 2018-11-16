---
title: ParentURL 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e67ac30883a7665368f6f46045ff61d9375b8cd1
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51603023"
---
# <a name="parenturl-property-ado"></a>ParentURL 속성(ADO)
부모를 가리키는 절대 URL 문자열을 나타냅니다 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 현재 **레코드** 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **문자열** 부모의 URL을 나타내는 값 **레코드**합니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **ParentURL** 속성을 여는 데 원본에 따라 달라 집니다 합니다 **레코드** 개체입니다. 예를 들어 합니다 **레코드** 에서 참조 하는 디렉터리의 상대 경로 이름을 포함 하는 소스를 사용 하 여 열 수 있습니다 합니다 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성입니다.  
  
 가정 폴더 "first"에서 "두 번째" 포함 되어 있습니다. 엽니다는 **레코드** 다음 구문을 사용 하 여 개체:  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 이제 `the` **ParentURL** 속성이 `"https://first"`의 동일 **ActiveConnection**합니다.  
  
 원본 수도 있습니다 절대 URL 같은 `"https://first/second"`합니다. 합니다 **ParentURL** 속성이 다음 `"https://first"`, 상위 수준 `"second"`합니다.  
  
 이 속성 경우 null 값일 수 있습니다.  
  
-   현재 개체에 대 한 부모인 예를 들어 경우는 **레코드** 개체는 디렉터리의 루트를 나타냅니다.  
  
-   합니다 **레코드** 개체 URL을 사용 하 여 지정할 수 없는 엔터티를 나타냅니다.  
  
 이 속성은 읽기 전용입니다.  
  
> [!NOTE]
>  이 속성은 문서 소스 공급자와 같은 지원만 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [레코드 및 공급자 제공 필드](../../../ado/guide/data/records-and-provider-supplied-fields.md)합니다.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
> [!NOTE]
>  현재 레코드에서 ADO 데이터 레코드를 포함 하는 경우 **레코드 집합**에 액세스 합니다 **ParentURL** 속성 URL이 없습니다 수 임을 나타내는 런타임 오류를 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)
