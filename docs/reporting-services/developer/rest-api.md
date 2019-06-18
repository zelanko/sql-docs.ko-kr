---
title: Reporting Services에 대한 REST API를 사용하여 개발 | Microsoft Docs
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: developer
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/12/2018
ms.openlocfilehash: d4f4af8dc03713046915f61effc684003303aaa9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65502739"
---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>Reporting Services에 대한 REST API를 사용하여 개발

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 Reporting Services는 REST(Representational State Transfer) API를 지원합니다. REST API는 HTTP 작업(메서드)의 집합을 지원하는 서비스 엔드포인트로, 보고서 서버 내에서 리소스에 대한 액세스의 생성, 검색, 업데이트 또는 삭제를 제공합니다.

REST API는 SQL Server 2017 Reporting Services 보고서 서버 카탈로그에 있는 개체에 대한 프로그래밍 방식 액세스를 제공합니다. 개체의 예로는 폴더, 보고서, KPI, 데이터 원본, 데이터 세트, 새로 고침 계획, 구독 등이 있습니다. REST API를 사용하면 폴더 계층 탐색, 폴더의 내용 검색 또는 보고서 정의 다운로드와 같은 작업을 수행할 수 있습니다. 또한 개체를 만들고, 업데이트하고 삭제할 수 있습니다. 개체를 사용한 작업의 예에는 보고서 업로드, 새로 고침 계획 실행, 폴더 삭제 등이 있습니다.

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-hybrid-note.md)]

## <a name="components-of-a-rest-api-requestresponse"></a>REST API 요청/응답의 구성 요소

REST API 요청/응답 쌍은 5개의 구성 요소로 구분할 수 있습니다.

* `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`으로 구성되는 **요청 URI**. 요청 URI는 요청 메시지 헤더에 포함되어 있지만, 대부분 언어 또는 프레임워크는 요청 메시지에서 이를 별도로 전달해야 하기 때문에 여기에서는 별도로 분류합니다.

    * URI 체계: 요청을 전송하는 데 사용되는 프로토콜을 나타냅니다. 예를 들어 `http` 또는 `https`입니다.
    * URI 호스트: `myserver.contoso.com`과 같이 REST 서비스 엔드포인트가 호스팅되는 서버의 도메인 이름 또는 IP 주소를 지정합니다.
    * 리소스 경로: 리소스 또는 해당 리소스 선택을 결정하는 데 서비스에서 사용되는 여러 세그먼트를 포함할 수 있는 리소스 컬렉션을 지정합니다. 예를 들어: `CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties`는 CatalogItem에 대한 지정된 속성을 가져오는 데 사용할 수 있습니다.
    * 쿼리 문자열(선택 사항): API 버전 또는 리소스 선택 조건과 같은 추가적인 단순 매개 변수를 제공합니다.

* HTTP 요청 메시지 헤더 필드:

    * 요청하는 작업의 유형이 무엇인지를 서비스에 알리는 필수 [HTTP 메서드](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)(작업 또는 동사로 알려지기도 함)입니다. Reporting Services REST API는 DELETE, GET, HEAD, PUT, POST 및 PATCH 메서드를 지원합니다.
    * 지정된 URI 및 HTTP 메서드에서 필요로 하는 선택적 추가 헤더 필드입니다.

* URI 및 HTTP 작업을 지원하는 선택적 HTTP **요청 메시지 본문** 필드입니다. 예를 들어 POST 작업은 복잡한 매개 변수로 전달되는 MIME 인코딩된 개체를 포함합니다. POST 또는 PUT 작업의 경우 `Content-type` 요청 헤더에서도 본문에 대한 MIME 인코딩 형식을 지정해야 합니다. 일부 서비스에서는 `application/json`과 같은 특정 MIME 형식을 사용해야 합니다.

* HTTP **응답 메시지 헤더** 필드:

    * 범위가 2xx 성공 코드부터 4xx 또는 5xx 오류 코드인 [HTTP 상태 코드](http://www.w3.org/Protocols/HTTP/HTRESP.html)입니다. 또는 API 설명서에 나와 있는 것처럼 서비스 정의된 상태 코드가 반환될 수 있습니다.
    * `Content-type` 응답 헤더와 같은 요청의 응답을 지원하는 데 필요한 선택적 추가 헤더 필드입니다.

* 선택적 HTTP **응답 메시지 본문** 필드:

    * MIME 인코딩된 응답 개체는 데이터를 반환하는 GET 메서드의 응답과 같은 HTTP 응답 본문에서 반환됩니다. 일반적으로 이러한 개체는 `Content-type` 응답 헤더로 표시된 것처럼 JSON 또는 XML과 같은 구조적 형식으로 반환됩니다.

## <a name="api-documentation"></a>API 설명서

최신 REST API에는 최신 API 설명서가 필요합니다. REST API는 OpenAPI 사양(Swagger 사양이라고도 함)을 기반으로 하며, [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0)에서 문서를 확인할 수 있습니다. API 설명서 이외에도 SwaggerHub에서 클라이언트 라이브러리를 JavaScript, TypeScript, C#, Java, Python, Ruby 등의 언어로 생성하는 데 도움을 받을 수 있습니다.

## <a name="testing-api-calls"></a>API 호출 테스트

HTTP 요청/응답 메시지를 테스트하는 도구는 [Fiddler](https://www.telerik.com/fiddler)입니다. Fiddler는 REST 요청을 가로챌 수 있는 무료 웹 디버깅 프록시로, HTTP 요청/응답 메시지를 쉽게 진단할 수 있도록 합니다.

## <a name="next-steps"></a>다음 단계

[SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0)에서 사용 가능한 API를 검토합니다.

예제는 [GitHub](https://github.com/Microsoft/Reporting-Services)에서 찾아볼 수 있습니다. 샘플에는 PowerShell 예제와 함께 TypeScript, React 및 웹팩을 기반으로 하는 HTML5 앱이 포함되어 있습니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
