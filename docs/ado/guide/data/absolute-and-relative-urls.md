---
title: "절대 곡선과 상대 Url | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c87fea24a0f03bbf179c74102fbb5514873f134a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="absolute-and-relative-urls"></a>절대 곡선과 상대 Url
URL을 로컬 또는 네트워크 컴퓨터에 저장 된 대상의 위치를 지정 합니다. 파일, 디렉터리, HTML 페이지, 이미지, 프로그램 및 등의 대상이 될 수 있습니다*합니다.*  
  
 *절대 URL* 리소스를 찾는 데 필요한 모든 정보를 포함 합니다.  
  
 A *상대 URL* 절대 URL을 사용 하 여 시작 지점으로 리소스를 찾습니다. 실제로 "완전 한 URL"는 대상의 절대 곡선과 상대 Url을 연결 하 여 지정 됩니다.  
  
 *절대 URL* 다음과 같은 형식을 사용: *scheme://server/path/resource*  
  
 상대 URL을 일반적으로 구성 되어는 *경로*, 고 필요에 따라는 *리소스*, 없는 *구성표* 또는 *서버*합니다. 다음 표에서 완전 한 URL 형식의 개별 부분을 정의합니다.  
  
 *구성표*  
 지정 방법을 *리소스* 를 액세스 하 합니다.  
  
 *서버*  
 컴퓨터의 이름을 지정 합니다. 여기서는 *리소스* 있는 합니다.  
  
 *경로*  
 대상에 선행 하는 디렉터리의 순서를 지정 합니다. 경우 *리소스* 은 대상 값에 있는 마지막 디렉터리는 *경로*합니다.  
  
 *리소스*  
 포함 하는 경우 *리소스* 대상인 경우 이며 일반적으로 파일의 이름입니다. 수도 있습니다는 *단순한 파일* , 바이트의 단일 이진 스트림을 포함 하는 또는 *구조화 된 문서* 저장소 및 바이트의 이진 스트림을 하나 이상 포함 합니다.  
  
## <a name="url-scheme-registration"></a>URL 구성표 등록  
 공급자 Url을 지 원하는 경우 하나 이상의 URL 체계는 공급자에 등록 됩니다. 등록 의미 체계를 사용 하는 Url 등록 된 공급자는 자동으로 호출 합니다. 예를 들어는 *http* 구성표에 등록 된 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. ADO 웹 폴더 또는 파일을 사용 하 여 Internet Publishing 공급자와 함께 모든 Url "http" 접두사로 나타낼 가정 합니다. 공급자가 등록 된 구성표에 대 한 내용은 공급자 설명서를 참조 합니다.  
  
## <a name="defining-context-with-a-url"></a>URL과 컨텍스트를 정의합니다.  
 가 나타내는 열려 있는 연결의 한 함수는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체는 데이터 원본에 대 한 후속 작업을 제한 하는 해당 연결이 표시 합니다. 즉, 연결 후속 작업에 대 한 컨텍스트를 정의합니다.  
  
 2.7 이상을 ado, 절대 URL도 컨텍스트를 정의할 수 있습니다. 예를 들어,는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체 절대 URL을 열지는 **연결** URL로 지정 된 리소스를 나타내는 개체가 암시적으로 만들어집니다.  
  
 에 컨텍스트를 정의 하는 절대 URL을 지정할 수 있습니다는 *ActiveConnection* 의 매개 변수는 **레코드** 개체 [열려](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드. 절대 URL의 값으로 지정할 수도 있습니다는 "URL**=**" 키워드는 **연결** 개체 [열려](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드 * ConnectionString* 매개 변수 및 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드 *ActiveConnection* 매개 변수입니다.  
  
 열어 컨텍스트를 정의할 수도 있습니다는 **레코드** 또는 **레코드 집합** 이미 있기 때문에 이러한 개체는 암시적 또는 명시적으로 선언 된 디렉터리를 나타내는 개체 **연결 ** 컨텍스트를 지정 하는 개체입니다.  
  
## <a name="scoped-operations"></a>범위가 지정 된 작업  
 컨텍스트 범위 정의-즉, 디렉터리 및 후속 작업에 참여할 수 있는 하위 디렉터리입니다. **레코드** 개체 디렉터리에서 작동 하는 여러 범위 지정 된 메서드 및 모든 하위 디렉터리에 있습니다. 이러한 방법 포함 [범위란](../../../ado/reference/ado-api/copyrecord-method-ado.md), [범위란](../../../ado/reference/ado-api/moverecord-method-ado.md), 및 [참여할 수 있는](../../../ado/reference/ado-api/deleterecord-method-ado.md)합니다.  
  
## <a name="relative-urls-as-command-text"></a>명령 텍스트로 상대 Url  
 문자열을 입력 하 여 데이터 원본에 대해 실행할 명령을 지정할 수 있습니다는 *CommandText* 의 매개 변수는 **연결** 개체의 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드, 및는 * 소스* 의 매개 변수는 **레코드 집합** 개체의 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드.  
  
 에 대 한 상대 URL을 지정할 수 있습니다는 *CommandText* 또는 *소스* 매개 변수입니다. 상대 URL이 SQL 명령; 등의 명령을 실제로 나타내지 않습니다. 단지 매개 변수를 지정 합니다. 활성 연결의 컨텍스트는 절대 URL 이어야 합니다. 및 *옵션* 로 매개 변수를 설정 해야 **adCmdTableDirect**합니다.  
  
 다음 코드 예제를 여는 방법을 보여 줍니다 예를 들어 한 **레코드 집합** Winnt/system32 디렉터리의 Readme25.txt 파일에:  
  
```  
recordset.Open "system32/Readme25.txt", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 서버를 지정 하는 연결 문자열의 절대 URL (`YourServer`)의 경로 (`Winnt`). 이 URL도 컨텍스트를 정의합니다.  
  
 절대 URL을 사용 하 여 시작 지점으로 하 고 경로의 나머지 부분을 지정 하는 명령 텍스트에서 상대 URL (`system32`) 및 파일을 열 (`Readme25.txt`).  
  
 옵션 필드 (`adCmdTableDirect`) 명령 유형 상대 URL 임을 나타냅니다.  
  
 다음 코드 예를 들어 열립니다는 **레코드 집합** 의 내용에는 `Winnt` 디렉터리:  
  
```  
recordset.Open "", "URL=http://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>OLE DB 공급자가 제공한 URL 스키마  
 정규화 된 URL의 앞부분입니다는 *구성표* URL의 나머지 부분에 의해 식별 되는 리소스에 액세스 하는 데 사용 되는 합니다. 예로 HTTP (Hypertext Transfer Protocol) 및 FTP (파일 전송 프로토콜).  
  
 ADO는 자신의 URL 스키마를 인식 하는 OLE DB 공급자를 지원 합니다. 예를 들어는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)*,* "게시" Windows 2000 파일에 액세스 하는 기존 HTTP 체계를 인식 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

