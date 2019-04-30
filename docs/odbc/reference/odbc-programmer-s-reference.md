---
title: ODBC 프로그래머&#39;참조 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c83a7de609d200da2957a65b9325d031eda49780
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273038"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 프로그래머&#39;참조
합니다 *ODBC 프로그래머 참조* 다음 섹션이 포함 되어 있습니다.  
  
-   [ODBC 3.8의 새로운](../../odbc/reference/what-s-new-in-odbc-3-8.md) Windows 8 SDK에 추가 된 새 ODBC 기능을 나열 합니다.  
  
-   [샘플 ODBC 프로그램](../../odbc/reference/sample-odbc-program.md) 샘플 ODBC 프로그램을 제시 합니다.  
  
-   [ODBC 소개](../../odbc/reference/introduction-to-odbc.md) 간략 한 역사 구조적 쿼리 언어 및 ODBC, ODBC 인터페이스에 대 한 개념 정보를 제공 합니다.  
  
-   [응용 프로그램을 개발](../../odbc/reference/develop-app/developing-applications.md) ODBC 인터페이스와 구현 하는 드라이버를 사용 하는 응용 프로그램을 개발 하는 방법에 대 한 정보를 포함 합니다.  
  
-   [ODBC 소프트웨어 설치 및 구성](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) 설치 및 DLL 함수 참조를 설정 하는 방법에 대 한 정보를 제공 합니다.  
  
-   [ODBC 드라이버 개발](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) 드라이버 작성에 대 한 정보를 포함 합니다.  
  
-   [API 참조](../../odbc/reference/syntax/odbc-reference.md) 구문 및 의미 체계 정보에 대 한 모든 ODBC 함수가 포함 되어 있습니다.  
  
-   [ODBC 부록](../../odbc/reference/appendixes/odbc-appendixes.md) 기술 세부 정보를 포함 하 고 ODBC 오류 코드, 데이터 형식 및 SQL 문법에 대 한 테이블을 참조 합니다.  
  
## <a name="working-with-the-odbc-documentation"></a>ODBC 설명서를 사용 하 여 작업  
 ODBC 인터페이스는 C 프로그래밍 언어를 사용 하 여 사용 하도록 설계 되었습니다. 세 가지 영역에 걸쳐 ODBC 인터페이스 사용: SQL 문, ODBC 함수 호출 및 C 프로그래밍 합니다. 이 설명서는 다음을 가정합니다.  
  
-   C 프로그래밍 언어에 대해 잘 알고 있습니다.  
  
-   일반 DBMS 지식 및 SQL에 익숙해야 합니다.  
  
 에서는 다음 표기법 사용 됩니다.  
  
|형식|사용 대상|  
|------------|--------------|  
|SELECT * FROM|대문자는 SQL 문, 매크로 이름 및 운영 체제 명령 수준에서 사용 되는 용어를 나타냅니다.|  
|`RETCODE SQLFetch(hdbc)`|고정 폭 글꼴 샘플 명령줄 및 프로그램 코드에 사용 됩니다.|  
|*argument*|기울임꼴은은 프로그래밍 방식으로 인수, 사용자 또는 응용 프로그램을 제공 해야 합니다 또는 강조 단어는 정보를 나타냅니다.|  
|**SQLEndTran**|굵은 나타냅니다 구문은 함수 이름을 포함 하 여 표시 된 대로 정확히 입력 해야 합니다.|  
|&#124;|세로 막대 구분 구문 줄의 두 가지 상호 배타적인 선택 합니다.|  
|...|줄임표는 인수 여러 번 반복할 수를 나타냅니다.|  
|. 이라고도 합니다. .|점 세 개 열의 이전 코드 줄의 연속 작업을 나타냅니다.|  
  
## <a name="about-the-code-examples"></a>코드 예제 정보  
 이 가이드의 코드 예제는 설명 목적 으로만 설계 되었습니다. ODBC 원칙을 설명 하는 데 주로 기록 되므로, 효율성 때로는 따로 설정 된 명확성을 위해. 또한 코드의 전체 섹션 명확성을 위해 생략 되었습니다 경우도 있습니다. 여기에 비 ODBC 함수 (이름이 "SQL"로 시작 하지 않는 해당 함수) 및 대부분의 오류 처리의 정의가 포함 됩니다.  
  
 모든 코드 예제에서는 ANSI 문자열 및의 시작 부분에 나와 있는 동일한 데이터베이스 스키마를 사용 [카탈로그 함수](../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
## <a name="recommended-reading"></a>권장 참조 항목  
 SQL에 대 한 자세한 내용은 다음 표준을 사용할 수 있습니다.  
  
-   언어-무결성 향상 된 기능, ANSI, 1989 ANSI X3.135 1989를 사용 하 여 SQL 데이터베이스입니다.  
  
-   Database Language - SQL: X3H2 ANSI 및 ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Open Group 데이터 관리: 구조적된 쿼리 언어 (SQL), 버전 2 (Open Group, 1996).  
  
 표준 및 공급 업체별 SQL 지침 외에도 많은 책 설명 SQL을 포함 합니다.  
  
-   날짜, C. J., Darwen, Hugh 사용 하 여: *SQL 표준에 대 한 지침* (Addison-wesley, 1993).  
  
-   Emerson, Sandra L., Darnovsky, Marcy, 및 사, Judith S.: *실제 SQL Handbook* (Addison-wesley, 1989).  
  
-   Groff, James R. 및 Weinberg, Paul 명사. *SQL을 사용 하 여* (Osborne Mcgraw-hill, 1990).  
  
-   Gruber, Martin: *SQL 이해* (Sybex, 1990).  
  
-   Jack L. 및 진 J. Hursch: *SQL, 구조적된 쿼리 언어* (탭 책, 1988).  
  
-   Melton, Jim 및 Simon, Alan R.: *새 SQL 이해: 완전 한 가이드* (Morgan Kaufmann 게시자, 1993).  
  
-   Fabian Pascal: *SQL 및 관계형 기본 사항* (& T 책, 1990).  
  
-   Trimble, J. Harvey, 박사 및 David Chappell 합니다. *SQL에 대 한 시각적 소개* (Wiley, 1989).  
  
-   Van der Lan, Rick 6.: *SQL 소개* (Addison-wesley, 1988).  
  
-   Vang Soren: *SQL 및 관계형 데이터베이스* (Microtrend 책, 1990).  
  
-   Viescas, John: *SQL 빠른 참조 가이드* (Microsoft Corp., 1989).  
  
 트랜잭션 처리에 대 한 자세한 내용은 다음을 참조 하세요.  
  
-   회색, J. 명사. 및 Reuter, Andreas: *트랜잭션 처리: 개념 및 기술을* (Morgan Kaufmann 게시자, 1993).  
  
-   Hackathorn, Richard 4.: *엔터프라이즈 데이터베이스 연결* (Wiley & 아들과, 1993).  
  
 호출 수준 인터페이스에 대 한 자세한 내용은 다음 표준을 사용할 수 있습니다.  
  
-   Open Group *데이터 관리: SQL 호출 수준 인터페이스 (CLI), C451* (Open Group, 1995).  
  
-   ISO/IEC 9075-3:1995, 호출 수준 인터페이스 (SQL/CLI).  
  
 ODBC에 대 한 추가 정보에 대 한 다양 한 온라인 설명서를 비롯 하 여:  
  
-   Geiger Kyle: *ODBC 내* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, l u c, Oelschlager, Jon, Shoemaker, Andrew, Jim, 간 및 Lilley, Albert W.: *ODBC 2를 사용 하 여* (Que, 1994).  
  
-   Johnston, Tom 및 Osborne를 표시 합니다. *ODBC 개발자 가이드* (Howard W. Sams & 1994 회사인).  
  
-   박 단은 북부: *Windows 다중 DBMS 프로그래밍: 사용 하 여 C++, Visual Basic, ODBC, OLE 2 및 DBMS 프로젝트의 도구* (Wiley John 및 아들과, Inc., 1995).  
  
-   Stegman, Michael O., Signore, Robert, 및 Creamer, John: *분산 환경에서 Open Database Connectivity을 ODBC 솔루션* (Mcgraw-hill, 1995).  
  
-   Welch, Keith. *ODBC 2를 사용 하 여* (Que, 1994).  
  
-   Whiting를 청구 합니다. *ODBC 21 개의 일 teach Yourself* (Howard W. Sams & 1994 회사인).
