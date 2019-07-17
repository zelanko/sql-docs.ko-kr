---
title: 인터넷 게시용 OLE DB Provider | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923901"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>인터넷 게시용 OLE DB 공급자
ADO [레코드](../../../ado/reference/ado-api/record-object-ado.md) 하 고 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체 수 Microsoft OLE DB provider for Internet Publishing (게시 공급자 인터넷) 액세스 하 고 리소스를 조작 웹 폴더 또는 파일 등 Microsoft FrontPage에서 제공 합니다. ADO의 원본을 지정할 수 있습니다는 **레코드**, **Stream**, 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 한 URL 이어야 합니다. 수 다음 업로드, 다운로드, 이동, 복사 및 리소스를 삭제 또는 직접 리소스 속성을 조작 합니다.  
  
 사용 하는 코드 예를 들어 **레코드** 및 **스트림을** 인터넷 게시 공급자를 사용 하 여 참조를 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)합니다.  
  
 인터넷 게시 공급자는 Microsoft Windows 2000을 사용 하 여 설치 됩니다. 이전 버전의 인터넷 게시 공급자 Microsoft Office 2000 및 Microsoft Internet Explorer 5.0을 사용 하 여 사용할 수도 있습니다.  
  
 인터넷 게시 공급자에 ADO를 연결 하는 방법은 세 가지가 있습니다.  
  
-   지정 "URL =" 연결 문자열에 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   Msdaipp.dso에 대 한 지정 된 *공급자* 연결 문자열 키워드입니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   Msdaipp.dso에 대 한 지정 합니다 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 의 속성을 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  Msdaipp.dso을 사용 하 여 공급자의 값으로 명시적으로 지정 하는 경우는 *공급자* 연결 문자열 키워드 또는 **공급자** 속성을 사용할 수 없습니다 "URL =" 연결 문자열에 있습니다. 이렇게 하면 오류가 발생 합니다. 대신, URL만 지정 하면 앞서 설명한 대로 합니다.  
  
 인터넷 게시 공급자에 대 한 자세한 내용은 참조 하세요. [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), 또는 있는 원본 응용 프로그램과 함께 제공 되는 공급자 설명서의 OLE DB 공급자 인터넷 게시 설치 됨: Windows 2000, Office 2000 또는 Internet Explorer 5.0입니다.
