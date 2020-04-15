---
title: 데이터 원본 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b7e464963471b0cad41c5b93d50507d0fa9bf96
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306514"
---
# <a name="data-sources"></a>솔루션 탐색기
*데이터 원본은* 단순히 데이터의 원본입니다. 파일, DBMS의 특정 데이터베이스 또는 라이브 데이터 피드일 수 있습니다. 데이터는 프로그램과 동일한 컴퓨터에 있거나 네트워크의 다른 컴퓨터에 있을 수 있습니다. 예를 들어 데이터 원본은 Novell® Netware에서 액세스하는 OS/2® 운영 체제에서 실행되는 Oracle DBMS일 수 있습니다. 게이트웨이를 통해 액세스하는 IBM DB2 DBMS; 서버 디렉터리에서 Xbase 파일의 컬렉션; 또는 로컬 Microsoft® 액세스 데이터베이스 파일입니다.  
  
 데이터 원본의 목적은 드라이버 이름, 네트워크 주소, 네트워크 소프트웨어 등 데이터에 액세스하는 데 필요한 모든 기술 정보를 한 곳에 수집하고 사용자로부터 숨기는 것입니다. 사용자는 급여, 인벤토리 및 인력이 포함된 목록을 보고, 목록에서 급여를 선택하고, 급여 데이터가 어디에 있는지 또는 응용 프로그램이 어떻게 도착했는지 알지 못하고 급여 데이터에 응용 프로그램을 연결하도록 할 수 있어야 합니다.  
  
 데이터 *원본이라는* 용어는 유사한 용어와 혼동해서는 안 됩니다. 이 설명서에서 *DBMS* 또는 *데이터베이스는* 데이터베이스 프로그램 또는 엔진을 참조합니다. 개인용 컴퓨터에서 실행되도록 설계되고 전체 SQL 및 트랜잭션 지원이 부족한 *데스크톱 데이터베이스와* 클라이언트/서버 상황에서 실행되도록 설계되었으며 독립 실행형 데이터베이스 엔진과 풍부한 SQL 및 트랜잭션 지원이 특징인 *서버 데이터베이스* 간에는 추가적인 차이가 있습니다. *데이터베이스는* 디렉터리또는 SQL Server의 데이터베이스와 같은 특정 데이터 컬렉션을 참조합니다. 일반적으로 이 설명서의 다른 곳에서 사용되는 *카탈로그* 라는 용어 또는 ODBC의 이전 버전에서 *한정자라는* 용어와 동일합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 원본 유형](../../odbc/reference/types-of-data-sources.md)  
  
-   [데이터 원본 사용](../../odbc/reference/using-data-sources.md)  
  
-   [데이터 원본 예제](../../odbc/reference/data-source-example.md)
