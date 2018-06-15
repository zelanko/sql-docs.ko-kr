---
title: 인터넷 게시에 대 한 OLE DB Provider | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee7efbcd02903e8bba38ecfa177ed7e095e0f5e9
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273032"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>인터넷 게시에 대 한 OLE DB Provider
ADO [레코드](../../../ado/reference/ado-api/record-object-ado.md) 및 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체가 사용 하 여 Microsoft OLE DB Provider for Internet Publishing (게시 공급자 인터넷) 액세스 하 고 리소스를 조작할 웹 폴더 또는 파일 Microsoft FrontPage 처리합니다. ADO와 원본을 지정할 수 있습니다는 **레코드**, **스트림**, 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) url은 URL 이어야 합니다. 수 다음 업로드, 다운로드, 이동, 복사 및 리소스를 삭제 또는 리소스 속성을 직접 조작 합니다.  
  
 사용 하는 코드 예를 들어 **레코드** 및 **스트림을** 인터넷 Publishing 공급자로 참조는 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md)합니다.  
  
 인터넷 게시 공급자는 Microsoft Windows 2000 함께 설치 됩니다. 이전 버전의 인터넷 게시 공급자 Microsoft Office 2000 및 Microsoft Internet Explorer 5.0 함께 사용할 수도 있습니다.  
  
 ADO 인터넷 게시 공급자에 연결 하는 방법은 세 가지가 있습니다.  
  
-   지정 "URL =" 연결 문자열에 있습니다. 예를 들어:  
  
    ```  
    objConn.Open "URL=http://servername"  
    ```  
  
-   에 대 한 Msdaipp.dso 지정는 *공급자* 의 연결 문자열 키워드입니다. 예를 들어:  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=http://servername"  
    ```  
  
-   에 대 한 Msdaipp.dso 지정는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 예를 들어:  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "http://servername"  
    ```  
  
> [!NOTE]
>  Msdaipp.dso을 사용 하 여 공급자의 값으로 명시적으로 지정 하는 경우는 *공급자* 연결 문자열 키워드 또는 **공급자** 사용할 수 없는 속성을 "URL =" 연결 문자열에 있습니다. 이렇게 하면 오류가 발생 합니다. 대신, URL만 지정 하면 앞에서 보았듯이 합니다.  
  
 인터넷 게시 공급자에 대 한 보다 구체적인 정보를 참조 하십시오. [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)는 소스 응용 프로그램과 함께 제공 되는 공급자 설명서 나 OLE DB Provider에 대 한 Internet Publishing이 설치 된: Windows 2000, Office 2000 또는 Internet Explorer 5.0입니다.
