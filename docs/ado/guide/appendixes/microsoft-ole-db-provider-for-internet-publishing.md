---
title: 인터넷 게시용 Microsoft OLE DB Provider | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 939cc21d8f89d93dca9249efcad82a85874a00c4
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350034"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Microsoft OLE DB Provider for Internet 게시 개요
Microsoft OLE DB Provider for Internet Publishing는 ADO를 Microsoft FrontPage 또는 Microsoft Internet Information Server 제공한 리소스에 액세스할 수 있습니다. 리소스에는 HTML 파일, Windows 2000 웹 폴더 등 웹 원본 파일이 포함 됩니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결을 설정 합니다 *공급자* 인수를 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을:

```vb
MSDAIPP.DSO
```

 이 값을 설정 하거나 사용 하 여 읽을 수도 있습니다는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성입니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```vb
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 -또는-

```vb
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 문자열을 이러한 키워드 이루어져 있습니다.

|키워드|설명|
|-------------|-----------------|
|**공급자**|인터넷 게시용 OLE DB Provider를 지정합니다.|
|**데이터 원본** -또는- **URL**|파일 또는 웹 폴더에 게시 하는 디렉터리의 URL을 지정 합니다.|
|**사용자 ID**|사용자 이름을 지정합니다.|
|**암호**|사용자 암호를 지정 합니다.|

> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 하거나 **Integrated Security = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.

 설정 하는 경우는 *ResourceURL* 에서 값을 "URL =" 잘못 된 값으로 연결 문자열에서 기본적으로 인터넷 게시 공급자를 발생 시킵니다를 올바른 값을 묻는 대화 상자. 이 동작은 바람직하지 않은 응용 프로그램의 중간 계층의 구성 요소에 대 한 대화 상자를 지우고 클라이언트 구성 요소에서 응답을 받지 못했기 때문에 고정 하려면 표시 될 때까지 프로그램 실행을 일시 중단 하기 때문에 합니다.

> [!NOTE]
>  경우 MSDAIPP 합니다. DSO을 사용 하 여 공급자의 값으로 명시적으로 지정 합니다 *공급자* 연결 문자열 키워드 또는 **공급자** 속성을 사용할 수 없습니다 "URL =" 연결 문자열에 있습니다. 이렇게 하면 오류가 발생 합니다. 대신, URL만 지정 하면 항목에 표시 된 대로 [OLE DB provider for Internet Publishing ADO를 사용 하 여](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)입니다.

## <a name="see-also"></a>관련 항목
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md) [인터넷 게시용 OLE DB Provider](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
