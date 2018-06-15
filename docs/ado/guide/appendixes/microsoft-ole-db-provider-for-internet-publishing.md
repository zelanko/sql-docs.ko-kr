---
title: Microsoft OLE DB Provider for 인터넷 게시 | Microsoft Docs
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
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c8d3caac3bd857b790372bd6b41fc818090210a0
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271222"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Microsoft OLE DB Provider for 인터넷 게시 개요
Microsoft OLE DB Provider for Internet Publishing Microsoft FrontPage 또는 Microsoft Internet Information Server에 의해 처리 리소스에 액세스 하도록 ADO 수 있습니다. 리소스에는 HTML 파일 또는 Windows 2000 웹 폴더와 같은 웹 원본 파일이 포함 됩니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결할 설정는 *공급자* 의 인수는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성:

```
MSDAIPP.DSO
```

 이 값도 설정 하거나 사용 하 여 읽을 수는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성입니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 -또는-

```
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 이러한 키워드의 문자열 구성 됩니다.

|키워드|Description|
|-------------|-----------------|
|**공급자**|인터넷 게시에 대 한 OLE DB Provider를 지정합니다.|
|**데이터 원본** -또는- **URL**|파일 또는 웹 폴더에 게시 하는 디렉터리의 URL을 지정 합니다.|
|**사용자 ID**|사용자 이름을 지정합니다.|
|**암호**|사용자 암호를 지정합니다.|

> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 또는 **통합 보안 = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.

 설정 하는 경우는 *ResourceURL* 에서 값은 "URL =" 잘못 된 값으로 연결 문자열에서 기본적으로 인터넷 게시 공급자 발생 유효한 값에 대 한 메시지를 표시 하는 대화 상자. 이 동작은 바람직하지 않은 응용 프로그램의 중간 계층의 구성 요소에 대 한 대화 상자를 지우고 클라이언트 구성 요소에서 응답을 받지 않은 때문에 고정 하려면 표시 될 때까지 프로그램 실행이 중단 때문에 합니다.

> [!NOTE]
>  경우 MSDAIPP 합니다. DSO 명시적으로 지정 된 공급자의 값으로는 *공급자* 연결 문자열 키워드 또는 **공급자** 사용할 수 없는 속성을 "URL =" 연결 문자열에 있습니다. 이렇게 하면 오류가 발생 합니다. 대신, URL만 지정 하면 항목에 나와 있는 것 처럼 [OLE DB Provider for Internet Publishing를 사용 하 여 ADO를 사용 하 여](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)합니다.

## <a name="see-also"></a>관련 항목
 [인터넷 게시 시나리오](../../../ado/guide/data/internet-publishing-scenario.md) [인터넷 게시에 대 한 OLE DB Provider](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)
