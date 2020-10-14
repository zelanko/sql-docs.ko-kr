---
title: 네임 스페이스--QName (XQuery) | Microsoft Docs
description: 네임 스페이스--QName 함수를 사용 하 여 QName의 네임 스페이스 URI를 검색 하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 035b92b719431b5a9b74f951f20d51911a41d59c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035782"
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>QNames 관련 함수 - namespace-uri-from-QName
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  *$Arg*로 지정 된 QName의 네임 스페이스 uri를 나타내는 문자열을 반환 합니다. *$Arg* 빈 시퀀스인 경우 결과가 빈 시퀀스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 네임스페이스 URI가 반환되는 QName입니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>A. QName에서 네임스페이스 URI 검색  
 작업 예제는 [로컬 이름-QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md)를 참조 하세요.  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **네임 스페이스--QName ()** 함수는 Xs: anyURI 대신 xs: string의 인스턴스를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Qname &#40;XQuery&#41;와 관련 된 함수 ](./functions-related-to-qnames-expanded-qname.md)  
  
