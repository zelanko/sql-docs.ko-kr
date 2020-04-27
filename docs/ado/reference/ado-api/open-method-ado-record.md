---
title: Open 메서드 (ADO 레코드) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97c7f1c143c83dd35ca5ff17e9776d79fb734ff9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917918"
---
# <a name="open-method-ado-record"></a>Open 메서드(ADO 레코드)
기존 [record](../../../ado/reference/ado-api/record-object-ado.md) 개체를 열거나 파일이 나 디렉터리와 같이 **레코드가**나타내는 새 항목을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 선택 사항입니다. 이 **Record** 개체, **명령**, 열린 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 또는 다른 **레코드** 개체, SQL SELECT 문 또는 테이블 이름이 포함 된 문자열을 나타내는 엔터티의 URL을 나타낼 수 있는 **Variant** 입니다.  
  
 *ActiveConnection*  
 선택 사항입니다. 연결 문자열 또는 열린 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체를 나타내는 **Variant** 입니다.  
  
 *모드*  
 선택 사항입니다. 결과 **레코드** 개체의 액세스 모드를 지정 하는 [connectmodeenum](../../../ado/reference/ado-api/connectmodeenum.md) 값입니다. 기본값은 **Admodeunknown**입니다.  
  
 *CreateOptions*  
 선택 사항입니다. 기존 파일 또는 디렉터리를 열어야 하는지 아니면 새 파일 또는 디렉터리를 만들어야 하는지를 지정 하는 [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md) 값입니다. 기본값은 **Adfailifnotexists**입니다. 이 값을 기본값으로 설정 하면 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 속성에서 액세스 모드를 가져옵니다. *원본* 매개 변수에 URL이 포함 되어 있지 않으면이 매개 변수는 무시 됩니다.  
  
 *옵션*  
 선택 사항입니다. **레코드**열기 옵션을 지정 하는 [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md) 값입니다. 기본값은 **Adopenrecordunspecified 되지 않음**입니다. 이러한 값은 결합할 수 있습니다.  
  
 *이름*  
 선택 사항입니다. 필요한 경우 *소스*에 대 한 액세스 권한을 부여 하는 사용자 ID를 포함 하는 **문자열** 값입니다.  
  
 *암호*  
 선택 사항입니다. 필요한 경우 *사용자 이름을*확인 하는 암호를 포함 하는 **문자열** 값입니다.  
  
## <a name="remarks"></a>설명  
 *소스* 는 다음과 같을 수 있습니다.  
  
-   URL입니다. URL의 프로토콜이 http 인 경우 기본적으로 인터넷 공급자가 호출 됩니다. URL이 실행 가능한 스크립트를 포함 하는 노드 (예:)를 가리키는 경우입니다. ASP 페이지)를 실행 하면 기본적으로 실행 되는 내용 대신 원본이 포함 된 **레코드가** 열립니다. *옵션* 인수를 사용 하 여이 동작을 수정할 수 있습니다.  
  
-   **Record** 개체입니다. 다른 **레코드** 에서 연 **record** 개체는 원래 **record** 개체를 복제 합니다.  
  
-   **명령** 개체입니다. 열린 **Record** 개체는 **명령을**실행 하 여 반환 된 단일 행을 나타냅니다. 결과에 하나 이상의 행이 포함 된 경우 첫 번째 행의 내용이 레코드에 배치 되 고 **오류 컬렉션에 오류가 추가** 될 수 있습니다.  
  
-   SQL SELECT 문입니다. 열린 **Record** 개체는 문자열의 내용을 실행 하 여 반환 된 단일 행을 나타냅니다. 결과에 하나 이상의 행이 포함 된 경우 첫 번째 행의 내용이 레코드에 배치 되 고 **오류 컬렉션에 오류가 추가** 될 수 있습니다.  
  
-   테이블 이름입니다.  
  
 **Record** 개체가 URL (예: 데이터베이스에서 파생 된 **레코드 집합** 의 행)을 사용 하 여 액세스할 수 없는 엔터티를 나타내는 경우 [parenturl](../../../ado/reference/ado-api/parenturl-property-ado.md) 속성과 **adRecordURL** 상수를 사용 하 여 액세스 하는 필드의 값이 모두 null입니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)
