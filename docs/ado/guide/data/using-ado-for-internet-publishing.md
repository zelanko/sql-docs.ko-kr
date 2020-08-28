---
description: 인터넷 게시용 ADO 사용
title: 인터넷 게시에 ADO 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 774ff9b0728d362822c72047b573ab9def944d18
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979039"
---
# <a name="using-ado-for-internet-publishing"></a>인터넷 게시용 ADO 사용
[인터넷 게시용 OLE DB 공급자는](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) ADO를 사용 하 여 다른 유형의 데이터에 액세스 하는 특정 예제를 보여 줍니다. 이 섹션의 예제는 인터넷 게시 공급자를 사용 하는 것과 관련 된 것 이지만, 다른 공급자와 함께 ADO를 사용 하 여 전자 메일 저장소에 대 한 공급자와 같은 다른 유형의 데이터를 사용 하는 경우에도 이와 비슷한 원칙이 사용 됩니다.  
  
## <a name="urls"></a>URL  
 Url (Uniform Resource Locator)을 연결 문자열과 명령 텍스트 대신 사용 하 여 데이터 원본 및 파일 및 디렉터리의 위치를 지정할 수 있습니다. 기존 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 및 레코드 **집합** 개체와 함께 Url과 **레코드** 및 **스트림** 개체를 사용할 수 있습니다.  
  
 Url을 사용 하는 방법에 대 한 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="record-fields"></a>레코드 필드  
 다른 유형의 데이터와 동일한 데이터의 차이점은 전자의 경우에는 데이터의 각 행 이나 **레코드**에 다른 열 집합이 나 **필드가**있을 수 있습니다. 유형이 같은 데이터의 경우 각 행에 동일한 열 집합이 있습니다. 인터넷 게시 공급자와 관련 된 필드에 대 한 자세한 내용은 [레코드 및 공급자 제공 추가 필드](../../../ado/guide/data/records-and-provider-supplied-fields.md)를 참조 하십시오.  
  
### <a name="appending-new-fields"></a>새 필드 추가  
 여러 ADO 개체가 **Record** 및 **Stream** 개체와 함께 작동 하도록 향상 되었습니다.  
  
-   [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션 [Append](../../../ado/reference/ado-api/append-method-ado.md) 메서드는 [필드 개체를](../../../ado/reference/ado-api/field-object.md) 만들어 컬렉션에 추가 하 고 **필드**의 값도 지정할 수 있습니다.  
  
-   [Update](../../../ado/reference/ado-api/update-method.md) 메서드는 컬렉션에 대 한 필드의 추가 또는 삭제를 마무리 합니다.  
  
-   **Append** 메서드에 대 한 바로 가기와 대안은 정의 되지 않았거나 이전에 삭제 한 필드에 값을 할당 하 여 필드를 만들 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [인터넷 게시용 OLE DB 공급자](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [절대 및 상대 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [레코드 및 공급자 제공 필드](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>참고 항목  
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Stream 개체 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 기록](../../../ado/guide/ado-history.md)
