---
title: 인터넷 게시에 ADO를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ac7922dda2d486f4783d1230296dc89b81cb4fe3
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718611"
---
# <a name="using-ado-for-internet-publishing"></a>인터넷 게시용 ADO 사용
[OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) ADO 사용 하 여 다른 유형의 데이터에 액세스 하는 특정 예제를 보여 줍니다. 이 섹션의 예에서는 인터넷 게시 공급자를 사용 하 여 특정 하지만 전자 메일 저장소 공급자와 같은 다른 유형의 데이터를 다른 공급자와 함께 ADO 사용 하는 경우에 원리와 유사한 이어야 합니다.  
  
## <a name="urls"></a>URL  
 Url (uniform Resource Locator) 데이터 원본 및 파일 및 디렉터리의 위치를 지정 하려면 연결 문자열을 명령 텍스트는 대 안으로 사용할 수 있습니다. 기존 Url을 사용할 수 있습니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 하 고 **레코드 집합** 개체와는 **레코드** 및 **Stream** 개체입니다.  
  
 Url을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="record-fields"></a>레코드 필드  
 유형이 다른 데이터와 같은 데이터 간의 가장 큰 차이점은 전자의 경우 데이터의 각 행에는 나 **레코드**, 다양 한 열을 가질 수 있습니다 또는 **필드**합니다. 유형이 같은 데이터에 대 한 각 행에 동일한 열 집합이 있습니다. 인터넷 게시 공급자에 게 특정 필드에 대 한 자세한 내용은 참조 하세요. [레코드 및 공급자 제공 필드를 추가](../../../ado/guide/data/records-and-provider-supplied-fields.md)합니다.  
  
### <a name="appending-new-fields"></a>새 필드 추가  
 여러 ADO 개체와 함께 작동 하도록 향상 되었습니다 **레코드** 하 고 **Stream** 개체입니다.  
  
-   [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션 [추가](../../../ado/reference/ado-api/append-method-ado.md) 메서드를 만들고 추가 [필드](../../../ado/reference/ado-api/field-object.md) 컬렉션에 개체의 값을 지정할 수도 있습니다는 **필드**.  
  
-   합니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 추가 하거나 컬렉션에 필드의 삭제 작업을 마무리 합니다.  
  
-   바로 가기로 사용 하거나 대신 합니다 **Append** 메서드를 정의 되지 않았거나 이전에 삭제 된 필드에 값을 할당 하 여 필드를 만들 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [인터넷 게시용 OLE DB 공급자](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [절대 및 상대 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [레코드 및 공급자 제공 필드](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>관련 항목  
 [레코드 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Stream 개체 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 버전 이력](../../../ado/guide/ado-history.md)
