---
title: 레코드 및 스트림 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 19fc6e61a10e1a92f0f674a23d00f1e1b06a596c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701692"
---
# <a name="records-and-streams"></a>레코드 및 스트림
ADO는 현재 제공 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 관계형 데이터베이스와 같은 데이터 원본에 있는 정보에 액세스 하는 기본 수단으로는 개체입니다. 그러나 일부 공급자를 지원 합니다 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 및 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체로 대체 또는 보조 개체는 공급자에서 데이터를 조작할 수 있습니다. 에 대 한 **레코드** 동작 공급자의 설명서를 참조 하세요.  
  
## <a name="records"></a>레코드  
 **레코드** 개체에는 기본적으로 한 행으로 함수 **레코드 집합**s입니다. 그러나 **레코드** 제한 된 기능만 비교할 **레코드 집합** 다양 한 속성 및 메서드를 갖습니다. 데이터에 대 한 소스를 **레코드** 개체 공급자에서 데이터 행 하나를 반환 하는 명령 수입니다. 사용 하 여 **레코드** 개체 대신 **Recordset** 복잡할수록을 인스턴스화하는 오버 헤드를 제거 하는 개체에서 데이터 행 하나를 반환 하는 쿼리 결과 받으려면 **레코드 집합**  개체입니다.  
  
 **레코드** 개체와 같은 다른 목적으로 전통적인 관계형 데이터베이스 이외의 데이터 원본에 대 한 공급자를 사용 하 여 특히 사용할 수는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 대부분의 처리 해야 하는 정보가 있지만, 데이터베이스에서 테이블 아니라 메시지로 전자 메일 시스템 및 파일에서 최신 파일 시스템에서. **레코드** 하 고 **Stream** 개체 관계형 데이터베이스 이외의 원본에서 저장 된 정보에 대 한 액세스를 용이 하 게 합니다.  
  
 합니다 **레코드** 개체를 나타내고 전자 메일 시스템의 메시지 또는 폴더와 파일 시스템에서 디렉터리 및 파일과 같은 데이터를 관리할 수 있습니다. 이러한 목적에 대 한 소스를 **레코드** 개방적이 고의 현재 행 수 **레코드 집합**, 개방적이 고와 함께에서 상대 URL 또는 절대 URL [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
 일반적으로 **레코드 집합** 컨테이너 또는 폴더 또는 디렉터리와 같은 계층의 부모를 나타내는 데 사용할 수 있습니다. A **레코드** 파일 또는 문서와 같은 부모 컨테이너에서 노드 하나에 대 한 특정 정보를 반환할 수 있습니다. 주된 이유 **레코드** 이러한 종류의 정보를 나타내는 데 사용 되며 다른 유형의 데이터의 이러한 소스는 합니다. 즉, 각 **레코드** 필드의 수와 다른 집합에 있을 수 있습니다. 기존의 **레코드 집합** 데이터베이스의 행을 포함 하는 동종. 즉, 각 행에 동일한 수와 유형의 필드입니다.  
  
 사용에 대 한 자세한 내용은 합니다 **레코드** 인터넷 게시 공급자와 같은 공급자에서이 다른 유형의 데이터를 처리 하기 위한 개체를 참조 하십시오 [for Internet Publishing ADO를 사용 하 여](../../../ado/guide/data/using-ado-for-internet-publishing.md)입니다.  
  
## <a name="streams"></a>스트림  
 합니다 **Stream** 개체를 읽고, 쓰고, 바이트 스트림을 관리 하는 방법을 제공 합니다. 이 바이트 스트림을 텍스트 또는 이진 수 있으며 시스템 리소스에 의해서만 크기가 제한 됩니다. 일반적으로 ADO **Stream** 개체는 다음 용도로 사용 됩니다.  
  
-   데이터를 포함 하는 **레코드 집합** XML 형식으로 저장 합니다. 이러한 XML 스트림을 저장 **Recordset**s 새 열면를 원본으로 사용할 수 있습니다 **Recordset**합니다. 자세한 내용은 [스트림 및 지 속성](../../../ado/guide/data/streams-and-persistence.md)합니다.  
  
-   포함할 [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) 대안을 공급자에 대해 실행할 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)합니다. 예를 들어, XML Updategram 용도 원본으로 Microsoft OLE DB Provider에 대 한 명령에 대 한 SQL Server에 대 한 합니다.  
  
-   이외의 다른 형식으로 공급자에서 결과 수신 하는 **레코드 집합**, Microsoft OLE DB Provider for SQL Server의에서 XML 결과 등. 자세한 내용은 [검색 결과를 스트림으로](../../../ado/guide/data/retrieving-resultsets-into-streams.md)합니다.  
  
-   텍스트 또는 파일 또는 for Internet Publishing Microsoft OLE DB 공급자와 같은 공급자를 사용 하 여 일반적으로 사용 되는 메시지를 구성 하는 바이트를 포함 합니다. 이 사용에 대 한 자세한 내용은 **Stream** 개체를 참조 하십시오 [for Internet Publishing ADO를 사용 하 여](../../../ado/guide/data/using-ado-for-internet-publishing.md)입니다.  
  
 A **Stream** 개체에서 열 수 있습니다.  
  
-   URL로 지정 하는 간단한 파일.  
  
-   필드를 **레코드** 또는 **레코드 집합** 포함 하는 **Stream** 개체입니다.  
  
-   기본 스트림을 한 **레코드** 또는 **레코드 집합** 디렉터리 또는 복합 파일을 나타내는 개체입니다.  
  
-   간단한 파일의 URL을 포함 하는 리소스 필드입니다.  
  
-   전혀 없는 특정 소스입니다. 이 경우에 **Stream** 개체가 메모리에 열려 있습니다. 데이터를 작성할 수 있고 다른 저장 수 **Stream** 또는 파일입니다.  
  
-   BLOB 필드에는 **레코드 집합**합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [스트림 및 지속성](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [명령 스트림](../../../ado/guide/data/command-streams.md)  
  
-   [스트림으로 결과 집합 검색](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [인터넷 게시에 ADO 사용](../../../ado/guide/data/using-ado-for-internet-publishing.md)
