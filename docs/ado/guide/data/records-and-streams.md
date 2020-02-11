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
ms.openlocfilehash: 4636df1451ba946b9a7bfb62e3d6775c35b1d6f3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924493"
---
# <a name="records-and-streams"></a>레코드 및 스트림
ADO는 현재 관계형 데이터베이스와 같은 데이터 원본의 정보에 액세스 하는 기본 수단으로 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 제공 합니다. 그러나 일부 공급자는 공급자의 데이터를 조작할 수 있는 대체 또는 보조 개체로 [Record](../../../ado/reference/ado-api/record-object-ado.md) 및 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체를 지원 합니다. **레코드** 동작에 대 한 자세한 내용은 공급자 설명서를 참조 하세요.  
  
## <a name="records"></a>레코드  
 **Record** 개체는 기본적으로 단일 행 **레코드 집합**으로 작동 합니다. 그러나 **레코드** 는 레코드 **집합** 에 비해 제한 된 기능을 가지 며 속성 및 메서드는 다릅니다. **Record** 개체의 데이터 원본은 공급자의 데이터 행 하나를 반환 하는 명령 일 수 있습니다. 레코드 **집합** 개체가 아닌 **Record** 개체를 사용 하 여 하나의 데이터 행을 반환 하는 쿼리의 결과를 수신 하면 더 복잡 한 **레코드 집합** 개체를 인스턴스화하는 오버 헤드가 제거 됩니다.  
  
 특히 [Microsoft OLE DB Provider For Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)과 같은 기존 관계형 데이터베이스 이외의 데이터 원본에 대 한 공급자를 사용 하는 경우 **Record** 개체는 다른 용도로 사용할 수 있습니다. 처리 해야 하는 대부분의 정보는 데이터베이스의 테이블이 아니라 전자 메일 시스템의 메시지와 최신 파일 시스템의 파일로 존재 합니다. **Record** 및 **Stream** 개체를 사용 하면 관계형 데이터베이스 이외의 원본에 저장 된 정보에 쉽게 액세스할 수 있습니다.  
  
 **Record** 개체는 파일 시스템의 디렉터리 및 파일, 전자 메일 시스템의 폴더 및 메시지와 같은 데이터를 표시 하 고 관리할 수 있습니다. 이러한 목적을 위해 **레코드** 의 원본은 열린 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체와 함께 열린 **레코드 집합**의 현재 행, 절대 url 또는 상대 url 일 수 있습니다.  
  
 일반적으로 **레코드 집합** 은 폴더 또는 디렉터리와 같은 계층의 컨테이너 또는 부모를 나타내는 데 사용할 수 있습니다. **레코드** 는 파일이 나 문서와 같이 부모 컨테이너에 있는 하나의 노드에 대 한 특정 정보를 반환 하는 데 사용할 수 있습니다. 이러한 유형의 정보를 나타내는 데 주로 **사용 되는 이유는** 이러한 데이터의 소스가 다른 것입니다. 즉, 각 **레코드** 의 집합 및 필드 수가 다를 수 있습니다. 데이터베이스의 행을 포함 하는 기존 **레코드 집합** 은 동일 합니다. 즉, 각 행에 동일한 수와 유형의 필드가 있음을 의미 합니다.  
  
 Data **개체를 사용 하 여 인터넷** 게시 공급자와 같은 공급자의 다른 유형의 데이터를 처리 하는 방법에 대 한 자세한 내용은 [인터넷 게시용 ADO 사용](../../../ado/guide/data/using-ado-for-internet-publishing.md)을 참조 하세요.  
  
## <a name="streams"></a>스트림  
 **Stream** 개체는 바이트 스트림을 읽고 쓰고 관리 하는 방법을 제공 합니다. 이 바이트 스트림은 텍스트 또는 이진 일 수 있으며 시스템 리소스에 의해서만 크기가 제한 됩니다. 일반적으로 ADO **Stream** 개체는 다음과 같은 용도로 사용 됩니다.  
  
-   XML 형식으로 저장 된 **레코드 집합** 의 데이터를 포함 하려면입니다. 저장 된 **레코드 집합**의 이러한 XML 스트림은 새 **레코드 집합**을 열 때 원본으로 사용할 수 있습니다. 자세한 내용은 [스트림 및 지 속성](../../../ado/guide/data/streams-and-persistence.md)을 참조 하세요.  
  
-   [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)대신 공급자에 대해 실행 될 [commandstreams](../../../ado/reference/ado-api/commandstream-property-ado.md) 을 포함 합니다. 예를 들어 XML UpdateGrams은 SQL Server 용 Microsoft OLE DB 공급자에 대해 명령의 원본으로 사용할 수 있습니다.  
  
-   공급자의 결과를 **레코드 집합**이외의 형식으로 수신 하려면 (예: SQL Server에 대 한 Microsoft OLE DB 공급자의 XML 결과). 자세한 내용은 [스트림에 결과 집합 검색](../../../ado/guide/data/retrieving-resultsets-into-streams.md)을 참조 하세요.  
  
-   파일이 나 메시지를 구성 하는 텍스트 또는 바이트를 포함 하려면 일반적으로 Microsoft OLE DB 공급자와 같은 공급자와 함께 인터넷 게시용으로 사용 됩니다. 이러한 **스트림** 개체 사용에 대 한 자세한 내용은 [인터넷 게시에 ADO 사용](../../../ado/guide/data/using-ado-for-internet-publishing.md)을 참조 하세요.  
  
 **Stream** 개체는 다음 위치에서 열 수 있습니다.  
  
-   URL로 지정 된 간단한 파일입니다.  
  
-   **Stream** 개체를 포함 하는 **레코드** 또는 레코드 **집합** 의 필드입니다.  
  
-   디렉터리 또는 복합 파일을 나타내는 **레코드** 또는 레코드 **집합** 개체의 기본 스트림입니다.  
  
-   단순 파일의 URL을 포함 하는 리소스 필드입니다.  
  
-   특정 소스가 없습니다. 이 경우 **Stream** 개체가 메모리에서 열립니다. 데이터를 쓴 다음 다른 **스트림이나** 파일에 저장할 수 있습니다.  
  
-   **레코드 집합**의 BLOB 필드입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [스트림 및 지속성](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [명령 스트림](../../../ado/guide/data/command-streams.md)  
  
-   [스트림으로 결과 집합 검색](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [인터넷 게시용 ADO 사용](../../../ado/guide/data/using-ado-for-internet-publishing.md)
