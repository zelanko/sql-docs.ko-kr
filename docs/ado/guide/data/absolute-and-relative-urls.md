---
title: 절대 및 상대 Url | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f15c5890300687a2d587a58a586d00bf2c8d0fd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926363"
---
# <a name="absolute-and-relative-urls"></a>절대 및 상대 URL
로컬 또는 네트워크 컴퓨터에 저장 된 대상의 위치를 지정 하는 URL입니다. 대상 파일, 디렉터리, HTML 페이지, 이미지, 프로그램 및 등을 수 있습니다.  
  
 *절대 URL* 리소스를 찾는 데 필요한 모든 정보를 포함 합니다.  
  
 A *상대 URL* 시작 지점으로 절대 URL을 사용 하 여 리소스를 찾습니다. 실제로 "완전 한 URL" 대상의 절대 및 상대 Url을 연결 하 여 지정 됩니다.  
  
 *절대 URL* 형식을 사용 합니다. *scheme://server/path/resource*  
  
 상대 URL만 일반적으로 구성 됩니다는 *경로*, 및 필요에 따라 합니다 *리소스*, 없는 *구성표* 또는 *server*. 다음 표에서 전체 URL 형식의 각 부분을 정의합니다.  
  
 *scheme*  
 지정 하는 방법을 *리소스* 액세스 하는 것입니다.  
  
 *server*  
 컴퓨터의 이름을 지정 합니다. 여기서는 *리소스* 위치한.  
  
 *path*  
 대상에 선행 하는 디렉터리 시퀀스를 지정 합니다. 경우 *자원* 는 대상 값에 있는 마지막 디렉터리는 *경로*합니다.  
  
 *resource*  
 포함 하는 경우 *리소스* 대상 이며 일반적으로 파일의 이름입니다. 것을 *간단한 파일* 바이트의 단일 이진 스트림을 포함 하 또는 *구조화 된 문서* 저장소 및 바이트의 이진 스트림을 하나 이상 포함 합니다.  
  
## <a name="url-scheme-registration"></a>URL 구성표 등록  
 공급자 Url을 지 원하는 경우 공급자는 하나 이상의 URL 구성표 등록 됩니다. 등록은 Url 구성표를 사용 하 여 등록 된 공급자는 자동으로 호출을 의미 합니다. 예를 들어 합니다 *http* 구성표에 등록 되어 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. ADO에서는 모든 Url "http"를 접두사로 나타내는 웹 폴더 또는 파일 인터넷 게시 공급자와 함께 사용 될 가정 합니다. 공급자가 등록 된 스키마에 대 한 자세한 내용은 공급자 설명서를 참조 합니다.  
  
## <a name="defining-context-with-a-url"></a>URL 사용 하 여 컨텍스트를 정의합니다.  
 연결 하 여 표시 한 함수를 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체는 데이터 원본에 대 한 후속 작업을 제한 하는 해당 연결이 표시 됩니다. 즉, 연결 후속 작업에 대 한 컨텍스트를 정의합니다.  
  
 2\.7 이상 ADO를 사용 하 여 절대 URL에는 컨텍스트를 정의할 수도 있습니다. 예를 들어 경우는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 절대 URL을 사용 하 여 개체를 열을 **연결** URL에서 지정 된 리소스를 나타내는 개체가 암시적으로 만들어집니다.  
  
 컨텍스트를 정의 하는 절대 URL을 지정할 수 있습니다 합니다 *ActiveConnection* 의 매개 변수를 **레코드** 개체 [열기](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드. 절대 URL 값으로 지정할 수도 있습니다는 "URL =" 키워드를 **연결** 개체 [열려](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드 *ConnectionString* 매개 변수 및 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드 *ActiveConnection* 매개 변수입니다.  
  
 열어 컨텍스트를 정의할 수도 있습니다는 **레코드** 또는 **Recordset** 이미 있기 때문에 이러한 개체는 암시적 또는 명시적으로 선언 된 디렉터리를 나타내는 개체 **연결**  컨텍스트를 지정 하는 개체입니다.  
  
## <a name="scoped-operations"></a>범위가 지정 된 작업  
 컨텍스트 범위 정의-즉, 디렉터리 및 후속 작업에 참여할 수 있는 하위 디렉터리입니다. 합니다 **레코드** 개체 디렉터리에서 작동 하는 여러 범위 지정 된 메서드 및 모든 하위 디렉터리에 있습니다. 이러한 메서드를 포함 [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)하십시오 [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md), 및 [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)합니다.  
  
## <a name="relative-urls-as-command-text"></a>명령 텍스트로 상대 Url  
 문자열을 입력 하 여 데이터 원본에서 실행할 명령을 지정할 수 있습니다 합니다 *CommandText* 의 매개 변수를 **연결** 개체의 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드에는  *소스* 의 매개 변수를 **레코드 집합** 개체의 [오픈](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드.  
  
 상대 URL을 지정할 수 있습니다 합니다 *CommandText* 하거나 *원본* 매개 변수입니다. 상대 URL이 SQL 명령; 같은 명령에 실제로 나타내지 않습니다. 단순히 매개 변수를 지정 합니다. 활성 연결의 컨텍스트는 절대 URL 이어야 합니다. 및 *옵션* 매개 변수를 설정 해야 **adCmdTableDirect**합니다.  
  
 다음 코드 샘플을 여는 방법 표시 하는 예를 들어, 한 **레코드 집합** Winnt/system32 디렉터리의 Readme25.txt 파일:  
  
```  
recordset.Open "system32/Readme25.txt", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 서버를 지정 하는 연결 문자열에서 절대 URL (`YourServer`) 및 경로 (`Winnt`). 이 URL도 컨텍스트를 정의합니다.  
  
 명령 텍스트의 상대 URL의 절대 URL을 사용 하 여 시작 점으로 및 경로의 나머지 부분을 지정 합니다 (`system32`) 및 파일을 엽니다 (`Readme25.txt`).  
  
 옵션 필드 (`adCmdTableDirect`) 명령 유형을 상대 URL 임을 나타냅니다.  
  
 또 다른 예로, 다음 코드는 열립니다는 **Recordset** 의 내용에는 `Winnt` 디렉터리:  
  
```  
recordset.Open "", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>OLE DB 공급자가 제공한 URL 구성표  
 정규화 된 URL의 앞부분입니다 합니다 *구성표* URL의 나머지 부분에 의해 식별 되는 리소스에 액세스 하는 데 사용 되는 합니다. HTTP (Hypertext Transfer Protocol) 및 FTP (파일 전송 프로토콜)을 예로 들 수 있습니다.  
  
 ADO는 자신의 URL 구성표를 인식 하는 OLE DB 공급자를 지원 합니다. 예를 들어 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) *,* "게시" Windows 2000 파일에 액세스 하는 기존 HTTP 체계를 인식 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [레코드 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
