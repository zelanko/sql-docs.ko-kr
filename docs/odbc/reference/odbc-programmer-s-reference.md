---
title: ODBC 프로그래머&#39;s 참조 | Microsoft Docs
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
ms.openlocfilehash: fd729956ee7bb1fccf7a8fceb7a435042df4df7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111189"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 프로그래머&#39;s 참조
*ODBC 프로그래머 참조* 에는 다음과 같은 섹션이 포함 되어 있습니다.  
  
-   [Odbc 3.8의 새로운](../../odbc/reference/what-s-new-in-odbc-3-8.md) 기능에는 WINDOWS 8 SDK에 추가 된 새로운 odbc 기능이 나열 되어 있습니다.  
  
-   샘플 [Odbc 프로그램](../../odbc/reference/sample-odbc-program.md) 은 샘플 odbc 프로그램을 제공 합니다.  
  
-   [Odbc 소개](../../odbc/reference/introduction-to-odbc.md) 에서는 구조적 쿼리 언어 및 odbc에 대 한 간략 한 기록과 odbc 인터페이스에 대 한 개념 정보를 제공 합니다.  
  
-   [응용 프로그램 개발](../../odbc/reference/develop-app/developing-applications.md) 에는 ODBC 인터페이스와이를 구현 하는 드라이버를 사용 하는 응용 프로그램 개발에 대 한 정보가 포함 됩니다.  
  
-   [ODBC 소프트웨어 설치 및 구성](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) 에서는 설치에 대 한 정보와 설치 DLL 함수 참조를 제공 합니다.  
  
-   [ODBC 드라이버를 개발](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) 하려면 드라이버 작성에 대 한 정보가 포함 되어 있습니다.  
  
-   [API 참조](../../odbc/reference/syntax/odbc-reference.md) 에는 모든 ODBC 함수에 대 한 구문 및 의미 체계 정보가 포함 되어 있습니다.  
  
-   Odbc [부록](../../odbc/reference/appendixes/odbc-appendixes.md) 에는 odbc 오류 코드, 데이터 형식 및 SQL 문법에 대 한 기술 정보 및 참조 테이블이 포함 되어 있습니다.  
  
## <a name="working-with-the-odbc-documentation"></a>ODBC 설명서 사용  
 ODBC 인터페이스는 C 프로그래밍 언어와 함께 사용 하도록 설계 되었습니다. ODBC 인터페이스의 사용은 SQL 문, ODBC 함수 호출 및 C 프로그래밍의 세 가지 영역으로 확장 됩니다. 이 문서에서는 다음을 가정 합니다.  
  
-   C 프로그래밍 언어에 대 한 작업 정보입니다.  
  
-   일반 DBMS 기술 자료 및 SQL에 대 한 지식이 있습니다.  
  
 다음과 같은 모양 표기 규칙이 사용 됩니다.  
  
|형식|사용 대상|  
|------------|--------------|  
|SELECT * FROM|대문자는 운영 체제 명령 수준에서 사용 되는 SQL 문, 매크로 이름 및 용어를 의미 합니다.|  
|`RETCODE SQLFetch(hdbc)`|고정 폭 글꼴은 샘플 명령줄 및 프로그램 코드에 사용 됩니다.|  
|*t*|기울임꼴 단어는 프로그래밍 인수, 사용자 또는 응용 프로그램에서 제공 해야 하는 정보 또는 단어 강조 표시를 의미 합니다.|  
|**SQLEndTran**|굵은 형식은 함수 이름을 포함 하 여 구문이 표시 된 대로 정확 하 게 입력 되어야 함을 나타냅니다.|  
|&#124;|세로 막대는 함께 사용할 수 없는 두 가지 옵션을 구문 줄에서 구분 합니다.|  
|...|줄임표는 인수가 여러 번 반복 될 수 있음을 나타냅니다.|  
|. . .|세 점의 열은 이전 코드 줄의 연속을 나타냅니다.|  
  
## <a name="about-the-code-examples"></a>코드 예제 정보  
 이 가이드의 코드 예제는 설명을 위해 작성 되었습니다. 주로 ODBC 원칙을 보여 주기 위해 작성 되었기 때문에 명확 하 게 이해 하기 위해 효율성을 따로 설정 해야 합니다. 또한 명확 하 게 하기 위해 코드의 전체 섹션을 생략 하는 경우도 있습니다. 여기에는 비 ODBC 함수 (이름이 "SQL"로 시작 하지 않는 함수)와 대부분의 오류 처리에 대 한 정의가 포함 됩니다.  
  
 모든 코드 예제는 [카탈로그 함수](../../odbc/reference/develop-app/catalog-functions.md)시작 부분에 표시 되는 ANSI 문자열과 동일한 데이터베이스 스키마를 사용 합니다.  
  
## <a name="recommended-reading"></a>권장 참조 항목  
 SQL에 대 한 자세한 내용은 다음 표준을 사용할 수 있습니다.  
  
-   데이터베이스 언어-무결성 향상 기능이 포함 된 SQL, ANSI, 1989 ANSI X 3.135-1989 년.  
  
-   데이터베이스 언어-SQL: ANSI X3H2 and ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   그룹 데이터 관리: 구조적 쿼리 언어 (SQL), 버전 2 (개방형 그룹, 1996)를 엽니다.  
  
 표준 및 공급 업체별 SQL 가이드 외에도 많은 서적에서 다음과 같은 SQL을 설명 합니다.  
  
-   Date, Darwen, Hugh: SQL 표준 (addison-Wesley, 1993) *에 대 한 가이드* 입니다.  
  
-   곳인 emerson, Sandra L., Darnovsky, Judith, Bowman, Wesley S.: *실용적인 SQL 안내서* (addison-, 1989).  
  
-   Groff, James R. 및 Weinberg, Paul N.: *SQL 사용* (Osborne McGraw-언덕, 1990).  
  
-   Gruber, Martin: *SQL 이해* (sybex, 1990).  
  
-   Hursch, 및 Carolyn J.: *SQL, 구조적 쿼리 언어* (탭 서적, 1988).  
  
-   Melton, 승, Simon, Alan R.: *새 SQL: A 전체 가이드* (Morgan Kaufmann 게시자, 1993)를 이해 합니다.  
  
-   파스칼, Fabian: *SQL 및 관계형 기본 사항* (M & T 서적, 1990).  
  
-   Trimble, Harvey, Jr 및 Chappell, David: SQL (Wiley, 1989) *을 시각적으로 소개* 합니다.  
  
-   Van der Lan, Rick F.: *SQL 소개* (addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL 및 관계형 데이터베이스* (마이크로 추세 서적, 1990).  
  
-   Viescas, John: *SQL에 대 한 빠른 참조 가이드* (Microsoft Corp., 1989).  
  
 트랜잭션 처리에 대 한 자세한 내용은 다음을 참조 하세요.  
  
-   회색, J. N. 및 Reuter, Andreas: *트랜잭션 처리: 개념 및 기술* (Morgan Kaufmann 게시자, 1993).  
  
-   Hackathorn, Richard D.: *Enterprise Database Connectivity* (Wiley & Sons, 1993).  
  
 호출 수준 인터페이스에 대 한 자세한 내용은 다음 표준을 사용할 수 있습니다.  
  
-   그룹 열기, *데이터 관리: SQL 호출 수준 인터페이스 (CLI), C451* (open group, 1995).  
  
-   ISO/IEC 9075-3:1995, 호출 수준 인터페이스 (SQL/CLI)  
  
 ODBC에 대 한 추가 정보를 보려면 다음을 비롯 한 많은 책을 사용할 수 있습니다.  
  
-   Geiger, Kyle: *ODBC* (Microsoft Press®, 1995)를 포함 합니다.  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, Shoemaker, Andrew, Cross, 승, Lilley, Albert W.: *ODBC 2* (쿼리, 1994)를 사용 합니다.  
  
-   Johnston, Tom 및 Osborne, Mark: *ODBC 개발자 가이드* (Howard W. Sams teach yourself & Company, 1994).  
  
-   북부, 켄은: *Windows 다중 Dbms 프로그래밍: Dbms 프로젝트용 c + +, Visual Basic, ODBC, OLE 2 및 도구 사용* (John Wiley & Sons, inc., 1995).  
  
-   Stegman, Michael O., Signore, Creamer, John: *ODBC 솔루션, 분산 환경에서 오픈 데이터베이스 연결* (McGraw-언덕, 1995).  
  
-   Welch, Keith: *ODBC 2* (쿼리, 1994)를 사용 합니다.  
  
-   한 번, 청구서: *ODBC를 21 일* (Howard Sams teach yourself & 회사, 1994)으로 알려 보세요.
