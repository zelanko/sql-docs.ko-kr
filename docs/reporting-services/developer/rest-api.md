---
title: "Reporting Services에 대 한 REST Api를 사용 하 여 개발 | Microsoft Docs"
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
ms.date: 10/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7c2c34047ac316045387b036cf10ee149175580a
ms.contentlocale: ko-kr
ms.lasthandoff: 10/20/2017

---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>보고 서비스에 대 한 REST Api를 사용 하 여 개발

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 Reporting Services REPRESENTATIONAL State Transfer () Api를 지원 합니다. REST Api는 서비스를 제공 하는 HTTP 작업 (메서드)의 집합을 지 원하는 끝점 만들기, 검색, 업데이트 또는 보고서 서버 내에서 리소스에 대 한 액세스를 삭제 합니다.

REST API는 SQL Server 2017 Reporting Services 보고서 서버 카탈로그에 있는 개체에 대 한 프로그래밍 방식 액세스를 제공합니다. 개체에는 폴더, 보고서, Kpi, 데이터 원본, 데이터 집합, 새로 고침 계획, 구독 및 더 있습니다. REST API를 사용 하 여 있습니다 수, 예를 들어 폴더 계층을 탐색는 폴더의 내용을 검색 또는 보고서 정의 다운로드 합니다. 있습니다 수 또한 만들기, 업데이트 및 개체를 삭제 합니다. 개체를 사용의 예는 보고서를 업로드, 새로 고침 계획을 실행, 폴더를 삭제 및 등입니다.

## <a name="components-of-a-rest-api-requestresponse"></a>REST API 요청/응답의 구성 요소

REST API 요청/응답 쌍 5 개의 구성 요소를 구분할 수 있습니다.

* **요청 URI**, 구성 된: `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`합니다. 요청 URI는 요청 메시지 헤더에 포함 되어 있지만 이름을 여기에서는 별도로 대부분 언어 또는 프레임 워크는 요청 메시지에서 별도로 전달할 수 필요 하기 때문에 있습니다.

    * URI 체계: 요청을 전송 하는 데 사용 되는 프로토콜을 나타냅니다. 예를 들어 `http` 또는 `https`합니다.
    * URI 호스트: 도메인 이름 또는 REST 서비스 끝점 호스팅되와 같은 서버의 IP 주소 지정 `myserver.contoso.com`합니다.
    * 리소스 경로: 리소스 또는 해당 리소스를 선택 하 고 결정 하는 데 서비스에서 사용 되는 여러 세그먼트를 포함할 수 있는 리소스 컬렉션을 지정 합니다. 예를 들어: `CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` 는 CatalogItem에 대 한 지정된 된 속성을 가져오는 데 사용할 수 있습니다.
    * 쿼리 문자열 (선택 사항): API 버전 또는 리소스 선택 조건과 같은 추가 단순 매개 변수를 제공 합니다.

* HTTP 요청 메시지 헤더 필드:

    * 필수 [HTTP 메서드](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) (라고도 연산 또는 동사), 서비스 요청 하는 작업 유형을 지정 합니다. 서비스 REST Api 지원 DELETE 보고 GET, HEAD, PUT, POST, 및 메서드를 패치 합니다.
    * 지정 된 URI와 HTTP 메서드로 필요에 따라 선택적 추가 헤더 필드입니다.

* 선택적 HTTP **요청 메시지 본문** URI 및 HTTP 작업을 지원 하도록 필드입니다. 예를 들어 POST 작업 복잡 한 매개 변수로 전달 되는 MIME 인코딩된 개체를 포함 합니다. POST 또는 PUT 작업에 대 한 본문에 대 한 MIME 인코딩 형식으로 지정 해야는 `Content-type` 도 요청 헤더입니다. 일부 서비스와 같은 특정 MIME 형식을 사용 해야 `application/json`합니다.

* HTTP **응답 메시지 헤더** 필드:

    * [HTTP 상태 코드](http://www.w3.org/Protocols/HTTP/HTRESP.html)2xx 성공 코드 4xx 또는 5xx 오류 코드에 이르기까지, 합니다. 또는 API 설명서에 나와 있는 것 처럼 서비스 정의 된 상태 코드가 반환 될 수 있습니다.
    * 와 같은 요청의 응답을 지 원하는 데 필요한 만큼 선택적 추가 헤더 필드는 `Content-type` 응답 헤더입니다.

* 선택적 HTTP **응답 메시지 본문** 필드:

    * MIME 인코딩된 응답 개체는 HTTP 응답 본문에서 데이터를 반환 하는 GET 메서드에서 응답과 같은 반환 됩니다. 일반적으로 이러한 개체는 반환 된 JSON 또는 XML과 같은 구조적 형식에 표시 된 대로 `Content-type` 응답 헤더입니다.

## <a name="api-documentation"></a>API 설명서

최신 API 설명서에 대 한 최신 REST API를 호출합니다. REST API는 기반으로 OpenAPI 사양 (규칙 하위 swagger 규격) 설명서에서 사용할 수는 및 [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0)합니다. API를 문서화 외 SwaggerHub 선택 – JavaScript, TypeScript, C#, Java, Python, Ruby, 등의 언어로 클라이언트 라이브러리를 생성할 수 있습니다.

## <a name="testing-api-calls"></a>테스트 API 호출

HTTP 요청/응답 메시지를 테스트 하는 도구는 [Fiddler](http://www.telerik.com/fiddler)합니다. Fiddler는 무료 웹 디버깅 프록시 REST 요청을 가로챌 수 있는 HTTP 요청을 진단 하기 쉽게 만들어 / 응답 메시지입니다.

## <a name="next-steps"></a>다음 단계

사용 가능한 Api를 통해 검토 [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0)합니다.

샘플에서 사용할 수 있는 [GitHub](https://github.com/Microsoft/Reporting-Services)합니다. 샘플은 TypeScript, React, 시스템용 PowerShell 예제에 구축 된 HTML5 응용 프로그램에 포함 되어 있습니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
