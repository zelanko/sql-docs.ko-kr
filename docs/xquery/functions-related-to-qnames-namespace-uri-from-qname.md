---
title: "네임 스페이스 uri-에서-QName (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:namespace-uri-from-QName function
- namespace-uri-from-QName function
ms.assetid: 4ab3f003-2a3b-4268-9e88-b615e35701b2
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 11e9a535a3cd2e8af3f6db1533b0cb35312905db
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="functions-related-to-qnames---namespace-uri-from-qname"></a>Qname-QName에서 네임 스페이스 uri와 관련 된 함수
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  지정 된 QName의 네임 스페이스 uri를 나타내는 문자열을 반환 *$arg*합니다. 결과 빈 시퀀스인 경우 *$arg* 빈 시퀀스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 네임스페이스 URI가 반환되는 QName입니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 다양 한 저장 된 XML 인스턴스에 대 한 XQuery 예 **xml** AdventureWorks 데이터베이스의 열을 입력 합니다.  
  
### <a name="a-retrieve-the-namespace-uri-from-a-qname"></a>1. QName에서 네임스페이스 URI 검색  
 작업 예제를 참조 하십시오. [QName의 로컬 이름 &#40; XQuery &#41; ](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   **namespace-uri-from-qname ()** 함수는 xs: anyuri 대신 xs: string의 인스턴스를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Qname &#40; 관련 함수 XQuery &#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
