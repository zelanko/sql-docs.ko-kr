---
description: ParentURL 속성(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e8e171362e66c9809e646eb33cecfbad91f30df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442755"
---
# <a name="parenturl-property-ado"></a>ParentURL 속성(ADO)
현재 **record** 개체의 부모 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 를 가리키는 절대 URL 문자열을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 부모 **레코드**의 URL을 나타내는 **문자열** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Parenturl** 속성은 **Record** 개체를 여는 데 사용 되는 원본에 따라 달라 집니다. 예를 들어 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성에서 참조 하는 디렉터리의 상대 경로 이름을 포함 하는 원본으로 **레코드** 를 열 수 있습니다.  
  
 "Second"는 "first" 아래에 포함 된 폴더 라고 가정 합니다. 다음 구문을 사용 하 여 **Record** 개체를 엽니다.  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 이제 `the` **parenturl** 속성의 값은 `"https://first"` **ActiveConnection**와 동일 합니다.  
  
 원본은와 같은 절대 URL 일 수도 있습니다 `"https://first/second"` . **Parenturl** 속성은 `"https://first"` 위의 수준입니다 `"second"` .  
  
 이 속성은 다음과 같은 경우에는 null 값이 될 수 있습니다.  
  
-   현재 개체의 부모가 없습니다. 예를 들어 **Record** 개체가 디렉터리의 루트를 나타내는 경우입니다.  
  
-   **Record** 개체는 URL을 사용 하 여 지정할 수 없는 엔터티를 나타냅니다.  
  
 이 속성은 읽기 전용입니다.  
  
> [!NOTE]
>  이 속성은 [Microsoft OLE DB Provider For Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)과 같은 문서 소스 공급자 에서만 지원 됩니다. 자세한 내용은 [레코드 및 공급자 제공 필드](../../../ado/guide/data/records-and-provider-supplied-fields.md)를 참조 하세요.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
> [!NOTE]
>  현재 레코드가 ADO **레코드 집합**의 데이터 레코드를 포함 하는 경우 **parenturl** 속성에 액세스 하면 URL이 없음을 나타내는 런타임 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)
