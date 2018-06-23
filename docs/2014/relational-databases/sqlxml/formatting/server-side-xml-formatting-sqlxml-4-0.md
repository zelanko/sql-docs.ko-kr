---
title: 서버 쪽 XML 서식 지정 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f7e8db71e82f25bb31afbe5a7a789df0af0a98ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180798"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>서버 쪽 XML 서식 지정(SQLXML 4.0)
  이 항목에서는 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 대해 실행한 쿼리로 생성된 행 집합의 XML 문서 서식을 서버 쪽에서 지정하는 방법을 설명합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 데이터베이스 테이블에 XML 문서를 저장하거나 데이터베이스 테이블에서 XML 문서를 검색할 수 있습니다. XML 문서를 검색하려면 SELECT 쿼리에서 FOR XML 쿼리 확장을 사용합니다.  
  
 예를 들어, 클라이언트 응용 프로그램에 대해 명령을 실행 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다음으로 구성 된 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML AUTO  
```  
  
 서버에서는 이 쿼리를 두 단계로 나누어 실행합니다. 서버에서는 먼저 다음 SELECT 문을 실행합니다.  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 그런 다음 생성된 행 집합에 FOR XML 변환을 적용합니다. 그러면 결과적으로 생성된 XML이 한 개의 열로 구성된 행 집합으로 클라이언트로 전송됩니다. 이 프로세스가 바로 이 설명서에서 말하는 서버 쪽 XML 서식 지정입니다.  
  
 서버 쪽에서는 FOR XML 절을 사용하여 다음 모드를 지정할 수 있습니다.  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
 FOR XML 절에 대 한 자세한 내용은 참조 [For를 사용 하 여 XML](../../xml/for-xml-sql-server.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [클라이언트 쪽 및 서버 쪽 XML 서식 지정 아키텍처 &#40;SQLXML 4.0&#41;](architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [클라이언트 쪽 XML 서식을 &#40;SQLXML 4.0&#41;](client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML&#40;SQL Server&#41;](../../xml/for-xml-sql-server.md)  
  
  