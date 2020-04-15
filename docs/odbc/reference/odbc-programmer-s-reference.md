---
title: ODBC 프로그래머&#39;레퍼런스 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a9ca32627b9703465dcfca554fdc32ae01442e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280513"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 프로그래머&#39;참조
*ODBC 프로그래머의 참조에는* 다음 섹션이 포함되어 있습니다.  
  
-   [ODBC 3.8의 새로운 기능은](../../odbc/reference/what-s-new-in-odbc-3-8.md) Windows 8 SDK에 추가된 새로운 ODBC 기능을 나열합니다.  
  
-   [샘플 ODBC 프로그램은](../../odbc/reference/sample-odbc-program.md) 샘플 ODBC 프로그램을 제공합니다.  
  
-   [ODBC 소개는](../../odbc/reference/introduction-to-odbc.md) 구조화 된 쿼리 언어 및 ODBC에 대한 간략한 기록과 ODBC 인터페이스에 대한 개념 정보를 제공합니다.  
  
-   [응용 프로그램 개발에는](../../odbc/reference/develop-app/developing-applications.md) ODBC 인터페이스를 사용하는 응용 프로그램 개발 및 응용 프로그램을 구현하는 드라이버에 대한 정보가 포함되어 있습니다.  
  
-   [ODBC 소프트웨어를 설치하고 구성하면](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) 설치 및 설치 DLL 기능 참조에 대한 정보를 제공합니다.  
  
-   [ODBC 드라이버를 개발하는](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) 방법에는 드라이버 작성에 대한 정보가 포함되어 있습니다.  
  
-   [API 참조는](../../odbc/reference/syntax/odbc-reference.md) 모든 ODBC 함수에 대한 구문 및 의미 체계 정보를 포함합니다.  
  
-   [ODBC 부록에는 ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) 오류 코드, 데이터 형식 및 SQL 문법에 대한 기술 세부 정보 및 참조 테이블이 포함되어 있습니다.  
  
## <a name="working-with-the-odbc-documentation"></a>ODBC 문서 작업  
 ODBC 인터페이스는 C 프로그래밍 언어와 함께 사용하도록 설계되었습니다. ODBC 인터페이스는 SQL 문, ODBC 함수 호출 및 C 프로그래밍의 세 가지 영역에서 사용됩니다. 이 설명서에는 다음이 있습니다.  
  
-   C 프로그래밍 언어에 대한 실무 지식입니다.  
  
-   일반적인 DBMS 지식과 SQL에 대한 친숙함.  
  
 다음 타이포그래피 규칙이 사용됩니다.  
  
|형식|사용 대상|  
|------------|--------------|  
|* 선택 중|대문자는 SQL 문, 매크로 이름 및 운영 체제 명령 수준에서 사용되는 용어를 나타냅니다.|  
|`RETCODE SQLFetch(hdbc)`|모노스페이스 글꼴은 샘플 명령줄 및 프로그램 코드에 사용됩니다.|  
|*argument*|기울임꼴 단어는 프로그래밍 방식의 인수, 사용자 또는 응용 프로그램에서 제공해야 하는 정보 또는 단어 강조를 나타냅니다.|  
|**SQLEndTran**|굵은 형식은 함수 이름을 포함하여 구문을 그림과 정확히 정확하게 입력해야 함을 나타냅니다.|  
|&#124;|세로 막대는 구문 줄에서 두 개의 상호 배타적인 선택 을 구분합니다.|  
|...|타원은 인수를 여러 번 반복할 수 있음을 나타냅니다.|  
|. . .|세 점의 열은 이전 코드 줄의 연속을 나타냅니다.|  
  
## <a name="about-the-code-examples"></a>코드 예제 소개  
 이 가이드의 코드 예제는 설명용으로만 설계되었습니다. 주로 ODBC 원칙을 보여주기 위해 작성되었기 때문에 명확성을 위해 효율성이 따로 설정되기도 합니다. 또한 명확성을 위해 코드의 전체 섹션이 생략된 경우도 있습니다. 여기에는 ODBC가 아닌 함수(이름이 "SQL"로 시작하지 않는 함수) 및 대부분의 오류 처리에 대한 정의가 포함됩니다.  
  
 모든 코드 예제에서는 ANSI 문자열과 동일한 데이터베이스 스키마를 사용하며, 이 스키마는 [카탈로그 함수의](../../odbc/reference/develop-app/catalog-functions.md)시작 부분에 표시됩니다.  
  
## <a name="recommended-reading"></a>권장 참조 항목  
 SQL에 대한 자세한 내용은 다음 표준을 사용할 수 있습니다.  
  
-   데이터베이스 언어 - 무결성 향상을 가진 SQL, ANSI, 1989 ANSI X3.135-1989.  
  
-   데이터베이스 언어 - SQL : ANSI X3H2 및 ISO / IEC JTC1 / SC21 / WG3 9075 : 1992 (SQL-92).  
  
-   오픈 그룹, 데이터 관리: 구조화 된 쿼리 언어 (SQL), 버전 2 (오픈 그룹, 1996).  
  
 표준 및 공급업체별 SQL 가이드 외에도 많은 책에서는 다음과 같은 SQL을 설명합니다.  
  
-   날짜, C. J., 다웬, 휴: *SQL 표준에 대한 가이드* (애디슨 웨슬리, 1993).  
  
-   에머슨, 산드라 엘, 다노프스키, 마시, 보우먼, 주디스 S.: *실용적인 SQL 핸드북* (애디슨 웨슬리, 1989).  
  
-   그로프, 제임스 R. 및 웨인버그, 폴 N.: *SQL 사용* (오스본 맥그로 힐, 1990).  
  
-   그루버, 마틴: *SQL 이해* (Sybex, 1990).  
  
-   허쉬, 잭 L. 및 캐롤린 J.: *SQL, 구조화 된 쿼리 언어* (TAB 책, 1988).  
  
-   멜튼, 짐, 사이먼, 앨런 R.: *새로운 SQL 이해: 완전한 가이드* (모건 카우프만 출판사, 1993).  
  
-   파스칼, 파비안: *SQL 및 관계기본사항* (M & T 북, 1990).  
  
-   트림블, 제이 하비 주니어, 샤펠, 데이비드: *SQL에 대한 시각적 소개* (와일리, 1989).  
  
-   반 데르 랜스, 릭 F.: *SQL 소개* (애디슨 웨슬리, 1988).  
  
-   방, 소렌: *SQL 및 관계형 데이터베이스* (마이크로 트렌드 도서, 1990).  
  
-   비에스카스, 존: *SQL에 대한 빠른 참조 가이드* (Microsoft Corp., 1989).  
  
 트랜잭션 처리에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   회색, J. N. 그리고 로이터, 안드레아스: *트랜잭션 처리: 개념 과 기술* (모건 카우프만 출판사, 1993).  
  
-   해커쏜, 리처드 D.: *엔터프라이즈 데이터베이스 연결* (와일리 & 아들, 1993).  
  
 통화 수준 인터페이스에 대한 자세한 내용은 다음 표준을 사용할 수 있습니다.  
  
-   오픈 그룹, *데이터 관리: SQL 통화 수준 인터페이스(CLI), C451(오픈* 그룹, 1995).  
  
-   ISO/IEC 9075-3:1995, 통화 수준 인터페이스(SQL/CLI).  
  
 ODBC에 대한 자세한 내용은 다음을 포함한 여러 책을 사용할 수 있습니다.  
  
-   가이거, 카일: *내부 ODBC* (마이크로 소프트 프레스®, 1995).  
  
-   그리폰, 로버트, 샤르펜티에, 루크, 올슐라거, 존, 구두 제작자, 앤드류, 크로스, 짐, 릴리, 앨버트 더블유: *ODBC 2 사용* (퀘, 1994).  
  
-   존스턴, 톰과 오스본, 마크: *ODBC 개발자 가이드* (하워드 W. 샘스 & 회사, 1994).  
  
-   북쪽, 켄: *윈도우 멀티 DBMS 프로그래밍: 사용 C ++, 비주얼 기본, ODBC, OLE 2 및 DBMS 프로젝트에 대 한 도구* (존 와일리 & 아들, Inc., 1995).  
  
-   스테그먼, 마이클 O., 무시, 로버트, 크리머, 존: *ODBC 솔루션, 분산 환경에서 개방형 데이터베이스 연결* (맥그로 힐, 1995).  
  
-   웰치, 키스: *ODBC 2 사용* (Que, 1994).  
  
-   휘팅, 빌: *21일 만에 ODBC를 가르쳐주세요(하워드* 더블유 샘스 & 컴퍼니, 1994년).
