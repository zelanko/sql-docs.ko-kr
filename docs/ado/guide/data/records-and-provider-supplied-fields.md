---
title: 레코드 및 필드 공급자가 제공한 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d929238274b5b92e9bdf7b89a369e7988c06b3fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="records-and-provider-supplied-fields"></a>레코드 및 필드 공급자 제공
경우는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체가 열릴, 소스에서 현재 열린 행 수 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 절대 URL 또는 열린와 함께에서 상대 URL [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 .  
  
 경우는 **레코드** 에서 열린는 **레코드 집합**, **레코드** 개체 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션은 의모든필드가포함됩니다 **레코드 집합**, 기본 공급자가 추가 된 모든 필드와 합니다.  
  
 공급자의 보조 특성을 제공 하는 추가 필드를 삽입할 수 있습니다는 **레코드**합니다. 결과적으로, 한 **레코드** 에 있지 않은 고유 필드를 할 수는 **레코드 집합** 전체 호스트 또는 모든 **레코드** 의 다른 행에서 파생 된는 **레코드 집합**.  
  
 예를 들어 모든 행을 한 **레코드 집합** 데이터 원본 열에는 이러한에서 및 주체 전자 메일에서 파생 합니다. A **레코드** 하에서 파생 된 **레코드 집합** 동일한 필드를 갖게 됩니다. 그러나는 **레코드** 다른 필드를 표시 하는 특정 메시지에 고유한 있을 **레코드**, 첨부 파일 및 받는 사람 등입니다.  
  
 하지만 **레코드** 개체 및 현재 행의는 **레코드 집합** 동일한 필드가 다른 때문에 **레코드** 및 **레코드 집합**개체는 다른 메서드 및 속성입니다.  
  
 공통적으로 보유 하는 필드는 **레코드** 및 **레코드 집합** 어느 한 개체에서 수정할 수 있습니다. 그러나에 필드를 삭제할 수 없습니다는 **레코드** 기본 공급자는 필드를 null로 설정할 수는 있지만 개체입니다.  
  
 후의 **레코드** 는 열을 프로그래밍 방식으로 필드를 추가할 수 있습니다. 필드를 추가 하면를 삭제할 수도 있지만 원래에서 필드를 삭제할 수 없습니다 **레코드 집합**합니다.  
  
 열 수도 있습니다는 **레코드** URL에서 직접 개체입니다. 필드에 추가 하는 경우에 **레코드** 기본 공급자에 따라 달라 집니다. 대부분의 공급자가 나타내는 엔터티를 설명 하는 필드의 집합을 추가 하는 현재는 **레코드**합니다. 엔터티가 같은 단순한 파일 바이트 스트림 구성 하는 경우는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 에서 일반적으로 개체를 열 수는 **레코드**합니다.  
  
## <a name="special-fields-for-document-source-providers"></a>문서에 대 한 특수 필드 원본 공급자  
 공급자를 호출 하는 특별 한 종류 *소스 공급자 문서*, 폴더를 관리 및에 대해 설명 합니다. 때는 **레코드** 개체에서 나타내는 문서 또는 **레코드 집합** 개체 문서 폴더를 나타내고, 문서 소스 공급자 설명 하는 필드의 고유 집합으로 해당 개체를 채웁니다. 문서의 특성 대신 실제 문서 자체에 있습니다. 하나의 필드에 대 한 참조를 포함 하는 일반적으로 **스트림** 문서를 나타내는입니다.  
  
 리소스를 구성 하는 이러한 필드 **레코드** 또는 **레코드 집합** 에서 지원 되는 특정 공급자에 대해 나열 된 및 [부록 a: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)합니다.  
  
 두 개 상수 인덱스는 **필드** 리소스의 컬렉션 **레코드** 또는 **레코드 집합** 를 자주 사용 되는 필드의 쌍을 검색 합니다. **필드** 개체 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성 원하는 콘텐츠를 반환 합니다.  
  
-   사용 하 여 액세스 하는 필드는 **adDefaultStream** 상수에는 연결 된 기본 스트림이 포함 되어는 **레코드** 또는 **레코드 집합** 개체입니다. 공급자는 개체에 기본 스트림이 할당합니다.  
  
-   사용 하 여 액세스 하는 필드는 **adRecordURL** 문서를 식별 하는 절대 URL을 포함 하는 상수입니다.  
  
 문서 소스 공급자가 지원 하지는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 **레코드** 및 **필드** 개체입니다. 콘텐츠는 **속성** 컬렉션이 해당 개체에 대해서는 null입니다.  
  
 문서 소스 공급자와 같은 공급자별 속성을 추가할 수 있습니다 **데이터 원본 유형을** 문서 소스 공급자 인지 식별할 수 있습니다. 공급자 유형을 결정 하는 방법에 대 한 자세한 내용은 공급자 설명서를 참조 합니다.  
  
## <a name="resource-recordset-columns"></a>리소스 레코드 집합 열  
 A *리소스 레코드 집합* 다음 열으로 구성 됩니다.  
  
|열 이름|유형|Description|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|읽기 전용입니다. 리소스의 URL을 나타냅니다.|  
|RESOURCE_PARENTNAME|AdVarWChar|읽기 전용입니다. 부모 레코드의 절대 URL을 나타냅니다.|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|읽기 전용입니다. PARENTNAME 및 PARSENAME의 연결 된 리소스의 절대 URL을 나타냅니다.|  
|RESOURCE_ISHIDDEN|adBoolean|True 이면 리소스 숨겨집니다. 행이 없는 행 집합을 명시적으로 만드는 명령 행 RESOURCE_ISHIDDEN가 True가 반환 됩니다.|  
|RESOURCE_ISREADONLY|adBoolean|리소스 읽기 전용 이면 true입니다. DB_E_READONLY DBBINDFLAG_WRITE 및가를이 리소스를 열려고 시도 실패 합니다. 리소스에만 열어 읽으려고 하는 경우에이 속성을 편집할 수 있습니다.|  
|RESOURCE_CONTENTTYPE|AdVarWChar|문서의 용도 나타냅니다-변호사의 간단한 예를 들어 있습니다. 문서를 만드는 데 사용 하는 Office 템플릿을에 해당 합니다.|  
|RESOURCE_CONTENTCLASS|AdVarWChar|와 같은 형식을 나타내는 문서의 MIME 형식을 나타내는 "`text/html`"입니다.|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|콘텐츠가 저장 된 언어를 나타냅니다.|  
|RESOURCE_CREATIONTIME|adFileTime|읽기 전용입니다. 리소스를 만든 시간을 포함 하는 FILETIME 구조를 나타냅니다. 시간이는 utc (협정 세계시) 형식으로 보고 됩니다.|  
|RESOURCE_LASTACCESSTIME|AdFileTime|읽기 전용입니다. 리소스를 마지막으로 액세스 하는 시간을 포함 하는 FILETIME 구조를 나타냅니다. 시간은 UTC 형식에서입니다. FILETIME 멤버는 공급자는이 시간 멤버를 지원 하지 않는 경우 0입니다.|  
|RESOURCE_LASTWRITETIME|AdFileTime|읽기 전용입니다. 리소스를 마지막으로 쓴 시간을 포함 하는 FILETIME 구조를 나타냅니다. 시간은 UTC 형식에서입니다. FILETIME 멤버는 공급자는이 시간 멤버를 지원 하지 않는 경우 0입니다.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|읽기 전용입니다. 리소스의 기본 스트림에 바이트의 크기를 나타냅니다.|  
|RESOURCE_ISCOLLECTION|adBoolean|읽기 전용입니다. True 이면 리소스 디렉터리와 같은 컬렉션입니다. 리소스가 간단한 파일 인 경우 false입니다.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|True 이면 리소스 구조적된 문서입니다. False 이면 리소스 구조화 된 문서가 아닙니다. 또는 간단한 파일 컬렉션 수 있습니다.|  
|DEFAULT_DOCUMENT|AdVarWChar|읽기 전용입니다. 이 리소스에는 폴더의 기본 단순 문서 또는 구조화 된 문서에 대 한 URL이 포함 되어 있음을 나타냅니다. 기본 스트림을 리소스에서 요청 될 때 사용 됩니다. 이 속성은 간단한 파일을 비워 둡니다.|  
|CHAPTERED_CHILDREN|AdChapter|읽기 전용입니다. (선택 사항) 리소스의 자식을 포함 하는 행 집합의 장을 나타냅니다. (의 *OLE DB Provider for Internet Publishing* 이 열을 사용 하지 않습니다.)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|읽기 전용입니다. 리소스의 표시 이름을 나타냅니다.|  
|RESOURCE_ISROOT|adBoolean|읽기 전용입니다. True 이면 리소스 컬렉션 또는 구조화 된 문서 루트입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
