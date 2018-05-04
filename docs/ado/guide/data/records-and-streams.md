---
title: 레코드 및 스트림 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcdfedc61d9a748f2d42064ac9821bf691f37e4d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="records-and-streams"></a>레코드 및 스트림
ADO 현재 제공 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 관계형 데이터베이스와 같은 데이터 원본의 정보에에서 액세스 하는 주요 수단으로 하는 개체입니다. 그러나 일부 공급자는 지원의 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 및 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체 변수로 대체 또는 보조 개체는 공급자에서 데이터를 조작할 수 있습니다. 에 사양에 대 한 **레코드** 동작을 공급자의 설명서를 참조 하십시오.  
  
## <a name="records"></a>레코드  
 **레코드** 개체가 기본적으로 한 행을 작동 **레코드 집합**s입니다. 그러나 **레코드** 에 비해 기능이 제한 **레코드 집합** 하 고 다른 속성 및 메서드를 갖습니다. 데이터에 대 한 소스는 **레코드** 개체 공급자에서 데이터의 한 행을 반환 하는 명령 일 수 있습니다. 사용 하 여 **레코드** 개체 보다는 **레코드 집합** 데이터의 한 행을 반환 하는 쿼리에서 결과 받는 개체에 대 한 보다 복잡 한 인스턴스화 작업과 오버 헤드가 제거 **레코드 집합**  개체입니다.  
  
 **레코드** 개체와 같은 다른 목적으로 기존의 관계형 데이터베이스 이외의 데이터 원본에 대 한 공급자와 특히 사용할 수 있습니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 대부분의 정보를 처리 해야 하는 데이터베이스에 테이블로 않고 메시지로 전자 메일 시스템 및 파일에에서 있습니다 최신 파일 시스템. **레코드** 및 **스트림** 개체를 관계형 데이터베이스 이외의 원본에 저장 된 정보에 대 한 액세스를 쉽게 합니다.  
  
 **레코드** 개체를 나타내고 전자 메일 시스템의 메시지 또는 폴더와 파일 시스템의 디렉터리 및 파일 등의 데이터를 관리할 수 있습니다. 이러한 목적에 대 한 소스는 **레코드** 열린의 현재 행 수 **레코드 집합**, 절대 URL 또는 열린와 함께에서 상대 URL [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
 일반적으로 **레코드 집합** 컨테이너 또는 폴더 또는 디렉터리와 같은 계층에서 부모를 나타내는 데 사용할 수 있습니다. A **레코드** 는 부모 컨테이너와 같은 파일 또는 문서에서에서 노드 하나에 대 한 특정 정보를 반환 하는 데 사용할 수 있습니다. 주된 이유 **레코드** 이러한 종류의 정보를 나타내는 데 사용 되며 이러한 데이터 소스에 다른 유형의 된다는 점입니다. 즉, 각 **레코드** 필드의 수와 다른 집합에 있을 수 있습니다. 기존의 **레코드 집합** 데이터베이스에서 행을 포함 형식 이므로, 형식이 같은 필드의 종류와 같은 수의 각 행에 있습니다.  
  
 사용 하는 방법에 대 한 자세한 내용은 **레코드** Internet Publishing 공급자와 같은 공급자에서이 다른 유형의 데이터를 처리 하기 위해 개체, 참조 [for Internet Publishing ADO를 사용 하 여](../../../ado/guide/data/using-ado-for-internet-publishing.md)합니다.  
  
## <a name="streams"></a>스트림  
 **스트림** 개체 읽기, 쓰기, 및의 바이트 스트림을 관리 하는 방법을 제공 합니다. 이 바이트 스트림에 텍스트 또는 이진 수 있으며 시스템 리소스에 의해서만 크기가 제한 됩니다. 일반적으로 ADO **스트림** 개체는 다음과 같은 용도로 사용 됩니다.  
  
-   데이터를 포함 하는 **레코드 집합** XML 형식으로 저장 합니다. 이러한 XML 스트림을 저장 **레코드 집합**s 새를 열 때의 원본으로 사용할 수 있습니다 **레코드 집합**합니다. 자세한 내용은 참조 [스트림 및 지 속성](../../../ado/guide/data/streams-and-persistence.md)합니다.  
  
-   포함 하도록 [CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md) 하는 대신 공급자에 대해 실행할 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)합니다. 예를 들어, XML Updategram 사용할 수는 원본으로 Microsoft OLE DB Provider에 대 한 명령에 대 한 SQL Server에 대 한 합니다.  
  
-   형식에서 공급자에서 아닌 다른 결과 받으려면는 **레코드 집합**, Microsoft OLE DB Provider for SQL Server XML 결과 같이 합니다. 자세한 내용은 참조 [스트림으로 검색 결과 집합과](../../../ado/guide/data/retrieving-resultsets-into-streams.md)합니다.  
  
-   텍스트 또는 파일 또는 for Internet Publishing 일반적으로 Microsoft OLE DB Provider와 같은 공급자와 함께 사용 하는 메시지를 구성 하는 바이트를 포함 합니다. 이 사용이에 대 한 자세한 내용은 **스트림** 개체 참조 [for Internet Publishing ADO를 사용 하 여](../../../ado/guide/data/using-ado-for-internet-publishing.md)합니다.  
  
 A **스트림** 개체에서 열 수 있습니다.  
  
-   URL로 지정 하는 간단한 파일입니다.  
  
-   필드는 **레코드** 또는 **레코드 집합** 포함 하는 **스트림** 개체입니다.  
  
-   기본 스트림에 **레코드** 또는 **레코드 집합** 디렉터리 또는 복합 파일을 나타내는 개체입니다.  
  
-   단순한 파일의 URL을 포함 하는 리소스 필드입니다.  
  
-   에 특정 원본이 없습니다. 이 경우는 **스트림** 개체가 메모리에서 열립니다. 데이터에 기록할 및 다음 다른에 저장할 수 **스트림** 또는 파일입니다.  
  
-   BLOB의 필드에는 **레코드 집합**합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [스트림 및 지속성](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [명령 스트림](../../../ado/guide/data/command-streams.md)  
  
-   [스트림으로 결과 집합 검색](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [인터넷 게시에 ADO 사용](../../../ado/guide/data/using-ado-for-internet-publishing.md)
