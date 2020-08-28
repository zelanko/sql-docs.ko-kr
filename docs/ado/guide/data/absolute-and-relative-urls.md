---
description: 절대 및 상대 URL
title: 절대 및 상대 Url | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- relative URLs [ADO]
- absolute URLs [ADO]
- URLs [ADO]
ms.assetid: 6a34a7ef-50cc-4c3d-82f7-106b9a8f3caf
author: rothja
ms.author: jroth
ms.openlocfilehash: 19ade6a2c9501523e97d30f496249a423445d3c0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991794"
---
# <a name="absolute-and-relative-urls"></a>절대 및 상대 URL
URL은 로컬 또는 네트워크에 저장 된 컴퓨터에 저장 된 대상의 위치를 지정 합니다. 대상은 파일, 디렉터리, HTML 페이지, 이미지, 프로그램 등이 될 수 있습니다.  
  
 *절대 URL* 은 리소스를 찾는 데 필요한 모든 정보를 포함 합니다.  
  
 *상대 url* 은 절대 url을 시작 점으로 사용 하 여 리소스를 찾습니다. 실제로 절대 URL과 상대 Url을 연결 하 여 대상의 "전체 URL"을 지정 합니다.  
  
 *절대 URL* 은 다음 형식을 사용 합니다. *scheme://server/path/resource*  
  
 상대 URL은 일반적으로 *경로로*만 구성 *되며 필요에* 따라 *리소스로*만 구성 *됩니다.* 다음 표에서는 전체 URL 형식의 개별 부분을 정의 합니다.  
  
 *scheme*  
 *리소스* 에 액세스 하는 방법을 지정 합니다.  
  
 *server*  
 *리소스가* 있는 컴퓨터의 이름을 지정 합니다.  
  
 *path*  
 대상으로 이어지는 디렉터리 시퀀스를 지정 합니다. *리소스* 를 생략 하면 대상은 *경로*에서 마지막 디렉터리입니다.  
  
 *리소스나*  
 포함 되는 경우 *리소스* 는 대상 이며 일반적으로 파일의 이름입니다. 단일 이진 바이트를 포함 하는 *간단한 파일* 이거나 하나 이상의 저장소 및 이진 바이트 스트림을 포함 하는 *구조화 된 문서* 일 수 있습니다.  
  
## <a name="url-scheme-registration"></a>URL 체계 등록  
 공급자가 Url을 지 원하는 경우 공급자가 하나 이상의 URL 스키마를 등록 합니다. 등록 이란 스키마를 사용 하는 모든 Url이 등록 된 공급자를 자동으로 호출 함을 의미 합니다. 예를 들어, *http* 체계가 [인터넷 게시용 Microsoft OLE DB 공급자](../appendixes/microsoft-ole-db-provider-for-internet-publishing.md)에 등록 되어 있습니다. ADO에서는 "http"로 시작 하는 모든 Url이 인터넷 게시 공급자에서 사용할 수 있는 웹 폴더 또는 파일 임을 가정 합니다. 공급자가 등록 하는 구성표에 대 한 자세한 내용은 공급자 설명서를 참조 하세요.  
  
## <a name="defining-context-with-a-url"></a>URL로 컨텍스트 정의  
 [연결](../../reference/ado-api/connection-object-ado.md) 개체로 표시 되는 열려 있는 연결의 한 함수는 해당 연결로 표시 되는 데이터 원본에 대 한 후속 작업을 제한 하는 것입니다. 즉, 연결에서 후속 작업에 대 한 컨텍스트를 정의 합니다.  
  
 ADO 2.7 이상에서는 절대 URL을 사용 하 여 컨텍스트를 정의할 수도 있습니다. 예를 들어 절대 URL을 사용 하 여 [Record](../../reference/ado-api/record-object-ado.md) 개체를 열면 url로 지정 된 리소스를 나타내기 위해 **연결** 개체가 암시적으로 생성 됩니다.  
  
 컨텍스트를 정의 하는 절대 URL은 **Record** object [Open](../../reference/ado-api/open-method-ado-record.md) 메서드의 *ActiveConnection* 매개 변수에 지정할 수 있습니다. 또한 절대 URL은 **Connection** object [open](../../reference/ado-api/open-method-ado-connection.md) method *CONNECTIONSTRING* 매개 변수에서 "URL =" 키워드의 값으로 지정 하 고 [Recordset](../../reference/ado-api/recordset-object-ado.md) 개체의 [open](../../reference/ado-api/open-method-ado-recordset.md) method *ActiveConnection* 매개 변수 값으로 지정할 수 있습니다.  
  
 컨텍스트를 지정 하는 암시적 또는 명시적으로 선언 된 **연결** 개체가 이미 있기 때문에 디렉터리를 나타내는 **레코드** 또는 레코드 **집합** 개체를 열어 컨텍스트를 정의할 수도 있습니다.  
  
## <a name="scoped-operations"></a>범위가 지정 된 작업  
 또한 컨텍스트는 범위 즉, 디렉터리와 후속 작업에 참여할 수 있는 하위 디렉터리를 정의 합니다. **Record** 개체에는 디렉터리와 모든 하위 디렉터리에서 작동 하는 여러 범위 지정 메서드가 있습니다. 이러한 메서드에는 [Copyrecord](../../reference/ado-api/copyrecord-method-ado.md), [MoveRecord](../../reference/ado-api/moverecord-method-ado.md)및 [DeleteRecord](../../reference/ado-api/deleterecord-method-ado.md)가 포함 됩니다.  
  
## <a name="relative-urls-as-command-text"></a>명령 텍스트인 상대 Url  
 **연결** 개체의 [Execute](../../reference/ado-api/execute-method-ado-connection.md) 메서드 및 **레코드 집합** 개체의 [Open](../../reference/ado-api/open-method-ado-recordset.md) 메서드의 *원본* *매개 변수에 문자열* 을 입력 하 여 데이터 원본에서 실행할 명령을 지정할 수 있습니다.  
  
 상대 URL은 *CommandText* 또는 *Source* 매개 변수에 지정할 수 있습니다. 상대 URL은 실제로 SQL 명령과 같은 명령을 표시 하지 않습니다. 단지 매개 변수만 지정 합니다. 활성 연결의 컨텍스트는 절대 URL 이어야 하 고 *Option* 매개 변수는 **adCmdTableDirect**로 설정 해야 합니다.  
  
 예를 들어 다음 코드 샘플은 Winnt/system32 디렉터리의 Readme25.txt 파일에서 **레코드 집합** 을 여는 방법을 보여 줍니다.  
  
```  
recordset.Open "system32/Readme25.txt", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
 연결 문자열의 절대 URL은 서버 ( `YourServer` )와 경로 ()를 지정 합니다 `Winnt` . 또한이 URL은 컨텍스트를 정의 합니다.  
  
 명령 텍스트의 상대 URL은 절대 URL을 시작 점으로 사용 하 고 경로 ()의 나머지 부분과 `system32` 열려는 파일 ()을 지정 합니다 `Readme25.txt` .  
  
 옵션 필드 ( `adCmdTableDirect` )는 명령 유형이 상대 URL 임을 나타냅니다.  
  
 또 다른 예로, 다음 코드는 디렉터리의 내용에 대 한 **레코드 집합** 을 엽니다 `Winnt` .  
  
```  
recordset.Open "", "URL=https://YourServer/Winnt/",,,adCmdTableDirect  
```  
  
## <a name="ole-db-provider-supplied-url-schemes"></a>OLE DB 공급자 제공 URL 체계  
 정규화 된 URL의 선행 부분은 URL의 나머지 부분에 의해 식별 되는 리소스에 액세스 하는 데 사용 되는 *체계* 입니다. 예를 들면 HTTP (하이퍼텍스트 전송 프로토콜)와 FTP (파일 전송 프로토콜)가 있습니다.  
  
 ADO는 자체 URL 체계를 인식 하는 OLE DB 공급자를 지원 합니다. 예를 들어 "*게시 된"* Windows 2000 파일에 액세스 하는 [인터넷 게시용 Microsoft OLE DB 공급자](../appendixes/microsoft-ole-db-provider-for-internet-publishing.md)는 기존 HTTP 체계를 인식 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Connection 개체 (ADO)](../../reference/ado-api/connection-object-ado.md)   
 [Record 개체 (ADO)](../../reference/ado-api/record-object-ado.md)   
 [레코드 집합 개체(ADO)](../../reference/ado-api/recordset-object-ado.md)