---
title: 잘못된 문자 및 이스케이프 규칙 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, invalid characters
- FOR XML clause, escape rules
ms.assetid: f2e9b997-f400-4963-b225-59d46c6b93e8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3203b5ce4ec033abaa008f8fca0cdc7021678e05
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735641"
---
# <a name="invalid-characters-and-escape-rules"></a>잘못된 문자 및 이스케이프 규칙
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 FOR XML 절에서 잘못된 XML 문자를 처리하는 방법에 대해 설명하고 XML 이름의 잘못된 문자에 대한 이스케이프 규칙을 나열합니다.  
  
## <a name="for-xml-and-invalid-characters"></a>XML 및 잘못된 문자의 경우  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 TYPE 지시어를 사용하지 않는 FOR XML 쿼리 내에서 잘못된 XML 문자가 반환되는 경우 해당 문자를 엔터티화합니다.  
  
 이러한 문자는 엔터티화되었는지 여부에 관계없이 XML 1.0 호환 파서에서 구문 분석 오류를 발생시키지만 엔터티화된 형식은 XML 1.1에 보다 적합합니다. 엔터티화된 형식은 이후 버전의 XML 표준에도 적합할 가능성이 높습니다. 또한 잘못된 문자의 코드 지점이 가시적으로 표시되기 때문에 보다 쉽게 디버깅을 수행할 수 있습니다.  
  
 XML 도구 사용자의 경우에는 데이터 스트림에 잘못된 문자가 있으면 어떤 방식으로든 XML 파서가 실패하기 때문에 해결 방법이 필요하지 않습니다. 비-XML 도구를 사용하는 경우 이러한 변경 내용을 적용하려면 엔터티화된 값으로 이러한 문자를 검색할 수 있도록 프로그래밍 논리를 업데이트해야 합니다.  
  
 다음 공백 문자는 왕복 중에 해당 문자를 보존할 수 있도록 FOR XML 쿼리에서 다르게 엔터티화됩니다.  
  
-   요소 내용 및 특성의 경우: **hex(0D)** (캐리지 리턴)  
  
-   특성 내용의 경우: **hex(09)** (탭), **hex(0A)** (줄 바꿈)  
  
 이러한 문자는 출력에 유지되며 파서에서 문자를 정규화하지 않습니다.  
  
## <a name="escape-rules"></a>이스케이프 규칙  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이름은 유효하지 않은 문자가 이스케이프 숫자 엔터티 인코딩으로 변환되는 방식으로 XML 이름으로 변환됩니다.  
  
 XML 이름에 사용할 수 있는 알파벳이 아닌 문자는 콜론(:)과 밑줄(_)뿐입니다. 콜론은 네임스페이스용으로 이미 예약된 문자이므로 이스케이프 문자로는 밑줄이 선택되었습니다. 다음은 인코딩에 사용되는 이스케이프 규칙입니다.  
  
-   XML 1.0 사양에 따라 유효한 XML 이름 문자가 아닌 모든 UCS-2 문자는 _xHHHH\_로 이스케이프됩니다. HHHH는 해당 문자에 대한 최상위 비트 우선 순서의 4자리 16진수 UCS-2 코드를 나타냅니다. 예를 들어 테이블 이름 **Order Details** 는 Order_x0020_Details로 인코딩됩니다.  
  
-   UCS-2 영역(U+0010FFFF에 U+00010000 범위의 USC-4 추가)은 _xHHHHHHHH\_로 인코딩됩니다. HHHHHHHH는 SQL Server 2000 이전 버전과의 호환성 모드인 경우 해당 문자에 대한 8자리 16진수 UCS-4 인코딩을 나타냅니다. 그렇지 않으면 ISO 표준에 맞도록 문자가 _xHHHHHH\_로 인코딩됩니다.  
  
-   문자 x가 뒤에 이어지지 않는 경우에는 밑줄 문자를 이스케이프 처리하지 않아도 됩니다. 예를 들어 테이블 이름 **Order_Details** 는 인코딩되지 않습니다.  
  
-   식별자에서 콜론은 이스케이프 처리되지 않으므로 네임스페이스 요소와 특성 이름이 FOR XML 쿼리에 의해 생성될 수 있습니다. 예를 들어 다음 쿼리는 이름에 콜론이 있는 네임스페이스 특성을 생성합니다.  
  
    ```  
    SELECT 'namespace-urn' as 'xmlns:namespace',   
     1 as 'namespace:a'   
    FOR XML RAW  
    ```  
  
     쿼리 결과는 다음과 같습니다.  
  
    ```  
    <row xmlns:namespace="namespace-urn" namespace:a="1"/>  
    ```  
  
     XML 네임스페이스를 추가할 때는 WITH XMLNAMESPACES를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML&#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
