---
description: 레코드 및 공급자 제공 필드
title: 레코드 및 공급자 제공 필드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
author: rothja
ms.author: jroth
ms.openlocfilehash: 6cd737ce36a53643503a5c76dfaafe2127c93f9b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453005"
---
# <a name="records-and-provider-supplied-fields"></a>레코드 및 공급자 제공 필드
[Record](../../../ado/reference/ado-api/record-object-ado.md) 개체를 열면 해당 원본은 열린 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체와 함께 열린 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)의 현재 행, 절대 url 또는 상대 url 일 수 있습니다.  
  
 레코드 **집합**에서 **레코드** 를 열면 **레코드** 개체 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에는 **레코드 집합**의 모든 필드와 기본 공급자가 추가한 필드가 모두 포함 됩니다.  
  
 공급자는 **레코드**의 보충 특성 역할을 하는 추가 필드를 삽입할 수 있습니다. 따라서 **레코드** 는 레코드 **집합** 에 없는 고유 필드 또는 레코드 **집합**의 다른 행에서 파생 된 **레코드** 를 가질 수 있습니다.  
  
 예를 들어 전자 메일 데이터 원본에서 파생 된 **레코드 집합** 의 모든 행에는 보낸 사람, 받는 사람, 제목 등의 열이 있을 수 있습니다. 해당 레코드 **집합** 에서 파생 된 **레코드** 는 동일한 필드를 갖게 됩니다. 그러나 **레코드** 에는 첨부 파일 및 참조 (참조)와 같이 해당 **레코드가**나타내는 특정 메시지에 고유한 다른 필드가 있을 수도 있습니다.  
  
 **레코드 개체와** 레코드 **집합** 의 현재 행에는 동일한 필드가 있지만 **레코드** 및 **레코드 집합** 개체의 메서드와 속성은 서로 다르기 때문에 서로 다릅니다.  
  
 **레코드** 및 레코드 **집합** 에서 공통적으로 보유 한 필드는 두 개체에서 수정할 수 있습니다. 그러나 기본 공급자가 필드를 null로 설정 하는 것을 지원할 수 있지만 **Record** 개체에서는 필드를 삭제할 수 없습니다.  
  
 **레코드** 를 연 후에는 프로그래밍 방식으로 필드를 추가할 수 있습니다. 추가한 필드를 삭제할 수도 있지만 원래 **레코드 집합**에서 필드를 삭제할 수는 없습니다.  
  
 URL에서 직접 **Record** 개체를 열 수도 있습니다. 이 경우 **레코드** 에 추가 된 필드는 기본 공급자에 따라 달라 집니다. 현재 대부분의 공급자는 **레코드가**나타내는 엔터티를 설명 하는 필드 집합을 추가 합니다. 엔터티가 단순 파일과 같은 바이트 스트림으로 구성 된 경우 일반적으로 **레코드**에서 [stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체를 열 수 있습니다.  
  
## <a name="special-fields-for-document-source-providers"></a>문서 소스 공급자의 특수 필드  
 *문서 소스 공급자*라는 특수 한 공급자 클래스는 폴더 및 문서를 관리 합니다. **Record** 개체가 문서를 나타내거나 **레코드 집합** 개체가 문서 폴더를 나타내는 경우 문서 원본 공급자는 이러한 개체를 실제 문서 자체 대신 문서의 특성을 설명 하는 고유한 필드 집합으로 채웁니다. 일반적으로 하나의 필드는 문서를 나타내는 **스트림에** 대 한 참조를 포함 합니다.  
  
 이러한 필드는 리소스 **레코드** 또는 **레코드 집합** 을 구성 하며 [부록 a: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)에서 지 원하는 특정 공급자를 위해 나열 됩니다.  
  
 두 상수는 리소스 **레코드** 또는 **레코드 집합** 의 **fields** 컬렉션을 인덱싱하고 일반적으로 사용 되는 필드 쌍을 검색 합니다. **Field** object [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성은 원하는 내용을 반환 합니다.  
  
-   **Addefaultstream** 상수를 사용 하 여 액세스 한 필드에는 **레코드** 또는 레코드 **집합** 개체와 연결 된 기본 스트림이 포함 되어 있습니다. 공급자는 개체에 기본 스트림을 할당 합니다.  
  
-   **AdRecordURL** 상수를 사용 하 여 액세스 되는 필드에는 문서를 식별 하는 절대 URL이 포함 됩니다.  
  
 문서 소스 공급자는 **Record** 및 **Field** 개체의 [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션을 지원 하지 않습니다. 이러한 개체에 대 한 **속성** 컬렉션의 내용이 null입니다.  
  
 문서 소스 공급자는 **데이터 원본 유형과** 같은 공급자별 속성을 추가 하 여 문서 원본 공급자 인지 여부를 식별할 수 있습니다. 공급자 유형을 결정 하는 방법에 대 한 자세한 내용은 공급자 설명서를 참조 하세요.  
  
## <a name="resource-recordset-columns"></a>리소스 레코드 집합 열  
 *리소스 레코드 집합* 은 다음과 같은 열로 구성 됩니다.  
  
|열 이름|Type|설명|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|읽기 전용입니다. 리소스의 URL을 나타냅니다.|  
|RESOURCE_PARENTNAME|AdVarWChar|읽기 전용입니다. 부모 레코드의 절대 URL을 나타냅니다.|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|읽기 전용입니다. PARENTNAME 및 PARSENAME의 연결 인 리소스의 절대 URL을 나타냅니다.|  
|RESOURCE_ISHIDDEN|AdBoolean|리소스가 숨겨져 있으면 True입니다. 행 집합을 만드는 명령이 RESOURCE_ISHIDDEN가 True 인 행을 명시적으로 선택 하지 않으면 행이 반환 되지 않습니다.|  
|RESOURCE_ISREADONLY|AdBoolean|리소스가 읽기 전용 이면 True입니다. DBBINDFLAG_WRITE를 사용 하 여이 리소스를 열려고 시도 하 고 DB_E_READONLY와 함께 실패 합니다. 리소스를 읽기용 으로만 연 경우에도이 속성을 편집할 수 있습니다.|  
|RESOURCE_CONTENTTYPE|AdVarWChar|문서를 사용 하는 경우 (예: lawyer의 brief)를 나타냅니다. 이는 문서를 만드는 데 사용 된 Office 템플릿에 해당할 수 있습니다.|  
|RESOURCE_CONTENTCLASS|AdVarWChar|""와 같은 형식을 나타내는 문서의 MIME 형식을 나타냅니다 `text/html` .|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|콘텐츠가 저장 되는 언어를 나타냅니다.|  
|RESOURCE_CREATIONTIME|adFileTime|읽기 전용입니다. 리소스를 만든 시간을 포함 하는 FILETIME 구조체를 나타냅니다. 시간은 UTC (협정 세계시) 형식으로 보고 됩니다.|  
|RESOURCE_LASTACCESSTIME|AdFileTime|읽기 전용입니다. 리소스를 마지막으로 액세스 한 시간을 포함 하는 FILETIME 구조체를 나타냅니다. 시간은 UTC 형식입니다. 공급자가이 시간 멤버를 지원 하지 않는 경우 FILETIME 멤버가 0입니다.|  
|RESOURCE_LASTWRITETIME|AdFileTime|읽기 전용입니다. 리소스를 마지막으로 쓴 시간을 포함 하는 FILETIME 구조체를 나타냅니다. 시간은 UTC 형식입니다. 공급자가이 시간 멤버를 지원 하지 않는 경우 FILETIME 멤버가 0입니다.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|읽기 전용입니다. 리소스의 기본 스트림 크기 (바이트)를 나타냅니다.|  
|RESOURCE_ISCOLLECTION|AdBoolean|읽기 전용입니다. 리소스가 디렉터리와 같은 컬렉션인 경우 True입니다. 리소스가 단순 파일 이면 False입니다.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|AdBoolean|리소스가 구조화 된 문서인 경우 True입니다. 리소스가 구조화 된 문서가 아닌 경우 False입니다. 컬렉션 또는 간단한 파일 일 수 있습니다.|  
|DEFAULT_DOCUMENT|AdVarWChar|읽기 전용입니다. 이 리소스에는 폴더의 기본 단순 문서 또는 구조화 된 문서에 대 한 URL이 포함 되어 있음을 나타냅니다. 리소스에서 기본 스트림을 요청 하는 경우에 사용 됩니다. 단순 파일의 경우이 속성은 비어 있습니다.|  
|CHAPTERED_CHILDREN|AdChapter|읽기 전용입니다. (선택 사항) 리소스의 자식을 포함 하는 행 집합의 챕터를 나타냅니다. *인터넷 게시용 OLE DB 공급자* 는이 열을 사용 하지 않습니다.|  
|RESOURCE_DISPLAYNAME|AdVarWChar|읽기 전용입니다. 리소스의 표시 이름을 나타냅니다.|  
|RESOURCE_ISROOT|AdBoolean|읽기 전용입니다. 리소스가 컬렉션 또는 구조화 된 문서의 루트 이면 True입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
