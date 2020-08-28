---
description: 인터넷 게시용 Microsoft OLE DB 공급자 개요
title: 인터넷 게시용 Microsoft OLE DB 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: rothja
ms.author: jroth
ms.openlocfilehash: f924e1bec97ed399f4d6d3351c8d18b1d8dad5b1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991064"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>인터넷 게시용 Microsoft OLE DB 공급자 개요
Microsoft OLE DB Provider for Internet 게시용을 사용 하면 ADO에서 Microsoft FrontPage 또는 Microsoft Internet Information Server가 제공 하는 리소스에 액세스할 수 있습니다. 리소스에는 HTML 파일, Windows 2000 웹 폴더 등의 웹 원본 파일이 포함 됩니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결 하려면 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) 속성의 *공급자* 인수를로 설정 합니다.

```vb
MSDAIPP.DSO
```

 이 값은 [공급자](../../reference/ado-api/provider-property-ado.md) 속성을 사용 하 여 설정 하거나 읽을 수도 있습니다.

## <a name="typical-connection-string"></a>일반 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은 다음과 같습니다.

```vb
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 또는

```vb
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 문자열은 다음과 같은 키워드로 구성 됩니다.

|키워드|설명|
|-------------|-----------------|
|**공급 기업**|인터넷 게시용 OLE DB 공급자를 지정 합니다.|
|**데이터 원본** 또는 **URL**|웹 폴더에 게시 된 파일 또는 디렉터리의 URL을 지정 합니다.|
|**사용자 ID**|사용자 이름을 지정합니다.|
|**암호**|사용자 암호를 지정 합니다.|

> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.

 연결 문자열의 "URL ="에서 *Resourceurl* 값을 잘못 된 값으로 설정 하는 경우 기본적으로 인터넷 게시 공급자는 유효한 값을 요청 하는 대화 상자를 발생 시킵니다. 이는 응용 프로그램의 중간 계층에 있는 구성 요소에 대해 바람직하지 않은 동작입니다 .이는 대화 상자를 지우고 클라이언트에서 구성 요소 로부터 응답을 받지 못해 중지 된 것 처럼 보일 때까지 프로그램 실행을 일시 중단 하기 때문입니다.

> [!NOTE]
>  MSDAIPP.DLL 인 경우 DSO는 공급자 연결 문자열 키워드 또는 **공급자** 속성을 사용 하 *여 공급자의* 값으로 명시적으로 지정 됩니다. 연결 문자열에는 "URL ="을 사용할 수 없습니다. 그러면 오류가 발생 합니다. 대신 [인터넷 게시용 OLE DB 공급자와 함께 ADO 사용](../data/the-ole-db-provider-for-internet-publishing.md)항목에 표시 된 대로 URL을 지정 하면 됩니다.

## <a name="see-also"></a>참고 항목
 인터넷 게시 [시나리오](../data/internet-publishing-scenario.md) [인터넷 게시를 위한 OLE DB 공급자](../data/the-ole-db-provider-for-internet-publishing.md)