---
title: "ADO를 사용 하 여 인터넷 게시를 위해 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9b26261c83932005ba0852b67e4f246cea47b8e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-ado-for-internet-publishing"></a>ADO를 사용 하 여 인터넷 게시에 대 한
[OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) ADO 사용 하 여 다른 유형의 데이터에 액세스 하는 특정 예제를 보여 줍니다. 이 섹션의 예는 인터넷 게시 공급자를 사용 하 여 특정 다르지만 원리 비슷해야 전자 메일 저장소 공급자와 같은 다른 유형의 데이터를 다른 공급자와 함께 ADO를 사용 하는 경우.  
  
## <a name="urls"></a>URL  
 (Url) uniform Resource Locator 데이터 원본 및 파일 및 디렉터리의 위치를 지정 하는 대신 연결 문자열 및 명령 텍스트를 사용할 수 있습니다. Url을 사용 하 여 기존 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 및 **레코드 집합** 개체와는 **레코드** 및 **스트림** 개체입니다.  
  
 Url을 사용 하는 방법에 대 한 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="record-fields"></a>레코드 필드  
 유형이 다른 데이터와 같은 데이터 간의 가장 큰 차이점은 전자의 경우 데이터의 각 행은 또는 **레코드**, 다른 집합의 열을 가질 수 있습니다 또는 **필드**합니다. 유형이 같은 데이터에 대 한 각 행에 동일한 열 집합이 있습니다. Internet Publishing 공급자와 관련 필드에 대 한 자세한 내용은 참조 [레코드와 공급자 추가 필드](../../../ado/guide/data/records-and-provider-supplied-fields.md)합니다.  
  
### <a name="appending-new-fields"></a>새 필드 추가  
 여러 ADO 개체와 함께 작동 하도록 향상 되었습니다 **레코드** 및 **스트림** 개체입니다.  
  
-   [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션 [Append](../../../ado/reference/ado-api/append-method-ado.md) 를 만들고 추가 하는 메서드는 [필드](../../../ado/reference/ado-api/field-object.md) 컬렉션에 개체, 값을 지정할 수도 **필드**.  
  
-   [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 추가 또는 삭제 컬렉션에 필드를 작업을 마무리 합니다.  
  
-   바로 가기 및에 대 한 대안으로는 **Append** 메서드를 정의 되지 않았거나 이전에 삭제 된 필드에 값을 할당 하 여 필드를 만들 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [인터넷 게시용 OLE DB 공급자](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [절대 및 상대 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [레코드 및 공급자 제공 필드](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [스트림 개체 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 기록](../../../ado/guide/ado-history.md)

