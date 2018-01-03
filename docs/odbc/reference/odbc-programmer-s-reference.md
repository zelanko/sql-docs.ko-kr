---
title: "ODBC 프로그래머 &#39; s 참조 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b934652505039a021d2b08c0fa5314614ce9c609
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-programmer39s-reference"></a>ODBC 프로그래머 &#39; s 참조
*ODBC Programmer's Reference* 다음 섹션이 포함 되어 있습니다.  
  
-   [What's New in ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) Windows 8 SDK에 추가 된 새로운 ODBC 기능을 설명 합니다.  
  
-   [ODBC 프로그램 샘플](../../odbc/reference/sample-odbc-program.md) ODBC 프로그램 예제를 제공 합니다.  
  
-   [ODBC 소개](../../odbc/reference/introduction-to-odbc.md) 구조적 쿼리 언어 및 ODBC 및 ODBC 인터페이스에 대 한 개념 정보 간략 한 시도한 기록을 제공 합니다.  
  
-   [응용 프로그램 개발](../../odbc/reference/develop-app/developing-applications.md) 드라이버는 ODBC 인터페이스와 구현 하는 드라이버를 사용 하는 응용 프로그램을 개발 하는 방법에 대 한 정보를 포함 합니다.  
  
-   [설치 및 구성 ODBC 소프트웨어](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) 설치 및 설정 DLL 함수 참조 하는 방법에 대 한 정보를 제공 합니다.  
  
-   [ODBC 드라이버를 개발](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) 드라이버를 쓰는에 정보를 포함 합니다.  
  
-   [API 참조](../../odbc/reference/syntax/odbc-reference.md) 구문 및 모든 ODBC 함수에 대 한 의미 체계 정보를 포함 합니다.  
  
-   [ODBC 부록](../../odbc/reference/appendixes/odbc-appendixes.md) 기술 세부 정보를 포함 하 고 ODBC 오류 코드, 데이터 형식 및 SQL 문법에 대 한 테이블을 참조 합니다.  
  
## <a name="working-with-the-odbc-documentation"></a>ODBC 설명서 사용  
 ODBC 인터페이스는 C 프로그래밍 언어에 사용 하도록 설계 되었습니다. ODBC 인터페이스를 사용 하 여 세 가지 영역에 걸쳐: SQL 문에서 ODBC 함수 호출 및 C 프로그래밍 합니다. 이 문서에는 다음이 있다고 가정 합니다.  
  
-   C 프로그래밍 언어에 대해 알고 있습니다.  
  
-   일반 DBMS 지식 및 SQL에 익숙해야 합니다.  
  
 에서는 다음 표기법 사용 됩니다.  
  
|형식|사용 대상|  
|------------|--------------|  
|선택 *에서|대문자 문자 SQL 문, 매크로 이름 및 운영 체제 명령 수준에서 사용 되는 용어를 나타냅니다.|  
|`RETCODE SQLFetch(hdbc)`|고정 폭 글꼴은 예제 명령줄 및 프로그램 코드에 사용 됩니다.|  
|*인수*|기울임꼴은은 프로그래밍 방식으로 인수, 사용자 또는 응용 프로그램이를 제공 해야 합니다 또는 강조 단어 정보를 나타냅니다.|  
|**SQLEndTran**|굵은 글꼴을 나타냄 구문은 함수 이름을 포함 하 여 표시 된 대로 정확히 입력 해야 합니다.|  
|&#124;|세로 막대 구문 줄에서 상호 배타적인 선택할 수 있는 두 가지를 구분합니다.|  
|...|가변 인수 수 여러 번 반복할 수를 나타냅니다.|  
|의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다. 이라고도 합니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.|세 개의 점의 열에는 코드의 이전 줄 연속을 나타냅니다.|  
  
## <a name="about-the-code-examples"></a>코드 예제 정보  
 이 가이드의 코드 예제는 이해를 돕기 위해 설계 되었습니다. ODBC 원칙을 설명 하는 데 주로 작성 하기 때문에 효율성 경우가 따로 설정 된 명확성을 위해. 또한 코드의 전체 섹션을 쉽게 구별할 수 있도록 누락 되었습니다 경우도 있습니다. 여기에 비 ODBC 함수 (이름이 "SQL"로 시작 하지 않는 이러한 함수) 및 대부분의 오류 처리의 정의가 포함 됩니다.  
  
 ANSI 문자열 및 동일한 데이터베이스 스키마의 시작 부분에 표시 된 모든 코드 예제에서는 사용 [카탈로그 함수](../../odbc/reference/develop-app/catalog-functions.md)합니다.  
  
## <a name="recommended-reading"></a>권장 참조 항목  
 SQL에 대 한 자세한 내용은 다음 표준을 사용할 수 있습니다.  
  
-   데이터베이스 언어-SQL 무결성 향상 된 기능, ANSI, 1989 ANSI X3.135 1989로 합니다.  
  
-   데이터베이스 언어-SQL: X3H2 ANSI 및 ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL 92).  
  
-   Open Group 데이터 관리: 구조적된 쿼리 언어 (SQL), 버전 2 (Open Group, 1996).  
  
 표준 및 공급 업체 특정 SQL 지침 외에도 다양 한 문서가 설명 SQL을 포함 하 여:  
  
-   날짜, Darwen, Hugh와 C. J.: *SQL 표준에 대 한 지침* (Addison-wesley, 1993).  
  
-   Emerson "," Sandra 범위로 정의 됩니다. "," Darnovsky "," Marcy, "및" 사, Judith S.: *실용적인 SQL 지침 서* (Addison-wesley, 1989).  
  
-   Groff, James 오른쪽 및 Weinberg, Paul 명사: *SQL을 사용 하 여* (Osborne McGraw-언덕, 1990).  
  
-   Gruber Martin: *SQL 이해* (Sybex 1990).  
  
-   Hursch, 잭 범위로 정의 됩니다. 및 진 J.: *SQL, 구조적된 쿼리 언어* (탭 책, 1988).  
  
-   Melton, Jim 및 Simon, Alan 오른쪽: *새 SQL 이해: 완벽 가이드* (Morgan Kaufmann Publishers, 1993).  
  
-   파스칼, Fabian: *SQL 및 관계형 기본 사항* (& T 책, 1990).  
  
-   Trimble, J. Harvey, 님 및 David Chappell,: *SQL에 대 한 시각적 소개* (Wiley, 1989).  
  
-   Van der Lan, Rick F.: *SQL 소개* (Addison-wesley, 1988).  
  
-   Vang, Soren: *SQL 및 관계형 데이터베이스* (Microtrend 책, 1990).  
  
-   Viescas John: *to SQL 빠른 참조 가이드* (Microsoft Corp., 1989).  
  
 트랜잭션 처리에 대 한 자세한 내용은 다음을 참조 하세요.  
  
-   회색 J. n입니다. 및 Reuter, Andreas: *트랜잭션 처리: 개념 및 기술을* (Morgan Kaufmann Publishers, 1993).  
  
-   Hackathorn Richard D.: *엔터프라이즈 데이터베이스 연결* (Wiley & 아들과, 1993).  
  
 호출 수준 인터페이스에 대 한 자세한 내용은 다음 표준을 사용할 수 있습니다.  
  
-   Open Group *데이터 관리: SQL 호출 수준 인터페이스 (CLI) C451* (Open Group, 1995).  
  
-   ISO/IEC 9075-3:1995, 호출 수준 인터페이스 (SQL/CLI).  
  
 ODBC에 대 한 추가 정보에 대 한 다양 한 설명서를 포함 하 여 사용할 수 있습니다:  
  
-   Geiger Kyle: *ODBC 내* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, Shoemaker, Andrew, Jim, 크로스 및 Lilley, Albert W.: *ODBC 2를 사용 하 여* (까지의 1994).  
  
-   Johnston, Tom 및 Osborne, 표시: *ODBC Developers Guide* (Howard W. Sam & 회사, 1994).  
  
-   북쪽, Ken: *Windows 다중 DBMS 프로그래밍: DBMS 프로젝트에 대 한 c + +, Visual Basic, ODBC, OLE 2 및 도구를 사용 하 여* (Wiley John & 아들과, Inc., 1995).  
  
-   Stegman, Michael 15., Signore, Robert 및 Creamer, John: *ODBC 솔루션, Open Database Connectivity에서 분산 환경을* (McGraw-언덕, 1995).  
  
-   Welch Keith: *ODBC 2를 사용 하 여* (까지의 1994).  
  
-   Whiting 청구서: *21 일 이내에 ODBC 학습* (Howard W. Sam & 회사, 1994).
