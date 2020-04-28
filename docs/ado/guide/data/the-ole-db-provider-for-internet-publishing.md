---
title: 인터넷 게시용 OLE DB 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80a373196f98a964bc3e522cc9329907a3392b95
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923901"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>인터넷 게시용 OLE DB 공급자
Microsoft OLE DB Provider for Internet publishing (internet Publishing Provider)를 사용 하 여 Microsoft FrontPage에서 [제공 하는](../../../ado/reference/ado-api/stream-object-ado.md) 웹 폴더 또는 파일과 같은 리소스에 액세스 [하 고 조작할](../../../ado/reference/ado-api/record-object-ado.md) 수 있습니다. ADO를 사용 하 여 **레코드**, **스트림**또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 원본을 URL로 지정할 수 있습니다. 그런 다음 리소스를 업로드, 다운로드, 이동, 복사 및 삭제 하거나 리소스 속성을 직접 조작할 수 있습니다.  
  
 인터넷 게시 공급자에서 **레코드** 와 **스트림을** 사용 하는 예제 코드는 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)를 참조 하십시오.  
  
 인터넷 게시 공급자는 Microsoft Windows 2000와 함께 설치 됩니다. 이전 버전의 인터넷 게시 공급자는 Microsoft Office 2000 및 Microsoft Internet Explorer 5.0 에서도 사용할 수 있습니다.  
  
 ADO를 인터넷 게시 공급자에 연결 하는 방법에는 다음 세 가지가 있습니다.  
  
-   연결 문자열에서 "URL ="을 지정 합니다. 예를 들면 다음과 같습니다.  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   연결 문자열의 *Provider* 키워드에 대해 msdaipp.dll를 지정 합니다. 예를 들면 다음과 같습니다.  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [Provider](../../../ado/reference/ado-api/provider-property-ado.md) 속성에 대해 msdaipp.dll를 지정 합니다. 예를 들면 다음과 같습니다.  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  *공급자 연결 문자열* 키워드 또는 **공급자** 속성을 사용 하 여 msdaipp.dll를 공급자 값으로 명시적으로 지정 하면 연결 문자열에 "URL ="을 사용할 수 없습니다. 그러면 오류가 발생 합니다. 대신 앞에서 설명한 것 처럼 URL을 지정 하면 됩니다.  
  
 인터넷 게시 공급자에 대 한 자세한 내용은 internet publishing [용 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)또는 인터넷 게시용 OLE DB 공급자가 설치 된 원본 응용 프로그램에서 제공 하는 공급자 설명서 (Windows 2000, Office 2000 또는 internet Explorer 5.0)를 참조 하십시오.
