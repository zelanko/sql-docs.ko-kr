---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54d55926d2bec89b0764b751bf165586e8d3c6c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924512"
---
# <a name="records-and-provider-supplied-fields"></a>레코드 및 공급자 제공 필드
경우는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체를 열, 해당 소스에서 현재 열려 있는 행 수 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 개방적이 고와 함께에서 상대 URL 또는 절대 URL [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 .  
  
 경우는 **레코드** 에서 열리는 **레코드 집합**의 **레코드** 개체 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션 는의모든필드에포함됩니다 **레코드 집합**, 기본 공급자가 추가 된 모든 필드와 합니다.  
  
 공급자의 보조 특성으로 사용 되는 추가 필드를 삽입할 수 있습니다 합니다 **레코드**합니다. 결과적으로 **레코드** 에 있지 않은 고유 필드가 있을 합니다 **레코드 집합** 또는 전체적으로 **레코드** 의 다른 행에서 파생 된는 **레코드집합**.  
  
 예를 들어 모든 행을 **레코드 집합** 데이터 원본 열에는 이러한 From, 및 주체 전자 메일에서 파생 됩니다. A **레코드** 에서 파생 된 **레코드 집합** 같은 필드가 포함 됩니다. 그러나 합니다 **레코드** 가 나타내는 특정 메시지에 고유한 다른 필드를 있을 수도 있습니다 **레코드**, 첨부 파일 등 Cc (참조에 포함할 복사).  
  
 하지만 **레코드** 개체와의 현재 행의 **레코드 집합** 있는 동일한 필드를 서로 때문에 **레코드** 및 **레코드집합**개체에는 서로 다른 메서드 및 속성입니다.  
  
 공통 소유 하는 필드를 **레코드** 하 고 **레코드 집합** 개체에서 수정할 수 있습니다. 그러나 필드를 삭제할 수 없습니다 합니다 **레코드** 기본 공급자는 필드를 null로 설정 지원할 수 있지만 개체입니다.  
  
 후 합니다 **레코드** 는 열린 하 필드를 프로그래밍 방식으로 추가할 수 있습니다. 에 추가 된 필드를 삭제할 수도 있습니다 하지만 원래에서 필드를 삭제할 수 없습니다 **레코드 집합**합니다.  
  
 열 수도 있습니다는 **레코드** URL에서 직접 개체입니다. 필드에 추가 하는 경우에 **레코드** 기본 공급자에 따라 달라 집니다. 현재 대부분의 공급자가 나타내는 엔터티를 설명 하는 필드의 집합을 추가 합니다 **레코드**합니다. 엔터티는 간단한 파일 등의 바이트 스트림을 구성 된 경우는 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 에서 일반적으로 개체를 열 수는 **레코드**합니다.  
  
## <a name="special-fields-for-document-source-providers"></a>문서에 대 한 특별 한 필드가 소스 공급자  
 공급자 라는 특수 클래스 *소스 공급자 문서*, 폴더를 관리 하 고 설명 합니다. 경우는 **레코드** 문서 또는 개체에서 나타내는 **레코드 집합** 개체가 나타내는 문서 폴더, 문서 소스 공급자를 설명 하는 필드의 고유 집합과 해당 개체를 채웁니다 문서의 특성 대신 실제 문서 자체에 있습니다. 하나의 필드에 대 한 참조를 포함 하는 일반적으로 **Stream** 문서를 나타내는입니다.  
  
 이러한 필드는 리소스 구성 **레코드** 또는 **recordset** 에 지원 되는 특정 공급자에 대해 나열 된 및 [부록 a: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)합니다.  
  
 두 상수 인덱스는 **필드** 리소스의 컬렉션 **레코드** 하거나 **레코드 집합** 일반적으로 사용 되는 필드의 쌍을 검색 하 합니다. 합니다 **필드** 개체 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성에는 원하는 콘텐츠를 반환 합니다.  
  
-   액세스할 필드를 **adDefaultStream** 상수와 연결 된 기본 스트림이 포함 된 **레코드** 또는 **레코드 집합** 개체. 공급자에 기본 스트림이 개체에 할당 합니다.  
  
-   액세스할 필드를 **adRecordURL** 상수 문서를 식별 하는 절대 URL을 포함 합니다.  
  
 문서 소스 공급자를 지원 하지 않습니다 합니다 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션인 **레코드** 및 **필드** 개체입니다. 콘텐츠를 **속성** 컬렉션이 해당 개체에 대 한 null입니다.  
  
 문서 소스 공급자와 같은 공급자별 속성을 추가할 수 있습니다 **데이터 원본 유형** 문서 소스 공급자 인지를 식별 합니다. 공급자 유형을 결정 하는 방법에 대 한 자세한 내용은 공급자 설명서를 참조 하세요.  
  
## <a name="resource-recordset-columns"></a>리소스 레코드 집합 열  
 A *리소스 레코드 집합* 다음 열으로 구성 됩니다.  
  
|열 이름|형식|설명|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|읽기 전용입니다. 리소스의 URL을 나타냅니다.|  
|RESOURCE_PARENTNAME|AdVarWChar|읽기 전용입니다. 부모 레코드의 절대 URL을 나타냅니다.|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|읽기 전용입니다. PARENTNAME 및 PARSENAME 연결 되는 리소스의 절대 URL을 나타냅니다.|  
|RESOURCE_ISHIDDEN|adBoolean|리소스 숨겨진 경우 true입니다. 행이 없는 행 집합을 명시적으로 만드는 명령 RESOURCE_ISHIDDEN True 인 행을 선택 하지 않으면 반환 됩니다.|  
|RESOURCE_ISREADONLY|adBoolean|리소스 읽기 전용 이면 true입니다. DB_E_READONLY DBBINDFLAG_WRITE 되며를 사용 하 여이 리소스를 열려고 시도 실패 합니다. 읽기에 대 한 리소스만 열린 경우에이 속성을 편집할 수 있습니다.|  
|RESOURCE_CONTENTTYPE|AdVarWChar|문서의 용도 나타냅니다-변호사와 상의 간단한 예를 들어 있습니다. 이 문서를 만드는 데 사용한 Office 템플릿을 해당할 수 있습니다.|  
|RESOURCE_CONTENTCLASS|AdVarWChar|와 같은 형식을 나타내는 문서의 MIME 형식을 나타내는 "`text/html`"입니다.|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|콘텐츠가 저장 되는 언어를 나타냅니다.|  
|RESOURCE_CREATIONTIME|adFileTime|읽기 전용입니다. 리소스를 만든 시간을 포함 하는 FILETIME 구조체를 나타냅니다. 시간 (UTC) 협정 세계시 형식으로 보고 됩니다.|  
|RESOURCE_LASTACCESSTIME|AdFileTime|읽기 전용입니다. 리소스를 마지막으로 액세스 하는 시간을 포함 하는 FILETIME 구조체를 나타냅니다. 시간은 UTC 형식에서입니다. FILETIME 멤버는 공급자는이 시간 멤버를 지원 하지 않는 경우 0입니다.|  
|RESOURCE_LASTWRITETIME|AdFileTime|읽기 전용입니다. 리소스를 마지막으로 쓴 시간을 포함 하는 FILETIME 구조체를 나타냅니다. 시간은 UTC 형식에서입니다. FILETIME 멤버는 공급자는이 시간 멤버를 지원 하지 않는 경우 0입니다.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|읽기 전용입니다. 리소스의 기본 스트림에 바이트의 크기를 나타냅니다.|  
|RESOURCE_ISCOLLECTION|adBoolean|읽기 전용입니다. 리소스가 디렉터리 같은 컬렉션에 있으면 true입니다. 리소스는 간단한 파일을 false로 지정 합니다.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|리소스는 구조화 된 문서 이면 true입니다. 리소스 구조화 된 문서가 아닌 경우 false입니다. 또는 간단한 파일 컬렉션 수 있습니다.|  
|DEFAULT_DOCUMENT|AdVarWChar|읽기 전용입니다. 이 리소스에는 폴더의 기본 단순 문서 또는 구조화 된 문서에 대 한 URL이 포함 되어 있음을 나타냅니다. 기본 스트림에 리소스에서 요청 될 때 사용 합니다. 이 속성은 간단한 파일에 대 한 비어 있습니다.|  
|CHAPTERED_CHILDREN|adChapter|읽기 전용입니다. (선택 사항) 리소스의 자식을 포함 하는 행 집합의 장을 나타냅니다. (합니다 *OLE DB Provider for Internet Publishing* 이 열을 사용 하지 않습니다.)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|읽기 전용입니다. 리소스의 표시 이름을 나타냅니다.|  
|RESOURCE_ISROOT|adBoolean|읽기 전용입니다. 리소스 컬렉션 또는 구조화 된 문서 루트 이면 true입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [레코드 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
