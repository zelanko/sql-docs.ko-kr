---
title: "예약 된 키워드 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- ODBC function calls
- keywords [SQL Server], reserved
- reserved words [SQL Server]
- keywords [SQL Server]
ms.assetid: ed8b3e27-6796-40f0-aef3-0cac5e0e2418
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: efaa21099f422ae812168561351a359fc89f8e0d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="reserved-keywords-transact-sql"></a>예약 된 키워드-TRANSACT-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 데이터베이스를 정의, 조작 및 액세스할 때 예약된 키워드를 사용합니다. 예약된 키워드는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문과 일괄 처리를 구문 분석하고 이해하는 데 사용하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 문법의 일부입니다. 구문상으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예약된 키워드를 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트에서 식별자와 개체 이름으로 사용할 수 있지만 구분 기호로 분리된 식별자를 사용한 경우에만 가능합니다.  
  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예약된 키워드를 나열합니다.  
  
||||  
|-|-|-|  
|ADD|EXTERNAL|PROCEDURE|  
|ALL|FETCH|PUBLIC|  
|ALTER|FILE|RAISERROR|  
|및|FILLFACTOR|READ|  
|ANY|FOR|READTEXT|  
|AS|FOREIGN|RECONFIGURE|  
|ASC|FREETEXT|REFERENCES|  
|AUTHORIZATION|FREETEXTTABLE|복제|  
|BACKUP|FROM|RESTORE|  
|BEGIN|FULL|RESTRICT|  
|BETWEEN|FUNCTION|RETURN|  
|BREAK|GOTO|REVERT|  
|BROWSE|GRANT|REVOKE|  
|BULK|GROUP|RIGHT|  
|BY|HAVING|ROLLBACK|  
|CASCADE|HOLDLOCK|ROWCOUNT|  
|CASE|IDENTITY|ROWGUIDCOL|  
|CHECK|IDENTITY_INSERT|RULE|  
|CHECKPOINT|IDENTITYCOL|SAVE|  
|CLOSE|IF|SCHEMA|  
|CLUSTERED|IN|SECURITYAUDIT|  
|COALESCE|INDEX|SELECT|  
|COLLATE|INNER|SEMANTICKEYPHRASETABLE|  
|COLUMN|INSERT|SEMANTICSIMILARITYDETAILSTABLE|  
|COMMIT|INTERSECT|SEMANTICSIMILARITYTABLE|  
|COMPUTE|INTO|SESSION_USER|  
|CONSTRAINT|IS|SET|  
|CONTAINS|JOIN|SETUSER|  
|CONTAINSTABLE|KEY|SHUTDOWN|  
|CONTINUE|KILL|SOME|  
|CONVERT|LEFT|STATISTICS|  
|CREATE|LIKE|SYSTEM_USER|  
|CROSS|LINENO|TABLE|  
|CURRENT|LOAD|TABLESAMPLE|  
|CURRENT_DATE|MERGE|TEXTSIZE|  
|CURRENT_TIME|NATIONAL|THEN|  
|CURRENT_TIMESTAMP|NOCHECK|TO|  
|CURRENT_USER|NONCLUSTERED|맨 위로 이동|  
|CURSOR|NOT|TRAN|  
|DATABASE|NULL|TRANSACTION|  
|DBCC|NULLIF|TRIGGER|  
|DEALLOCATE|OF|TRUNCATE|  
|DECLARE|OFF|TRY_CONVERT|  
|DEFAULT|OFFSETS|TSEQUAL|  
|DELETE|ON|UNION|  
|DENY|OPEN|UNIQUE|  
|DESC|OPENDATASOURCE|UNPIVOT|  
|DISK|OPENQUERY|UPDATE|  
|DISTINCT|OPENROWSET|UPDATETEXT|  
|DISTRIBUTED|OPENXML|USE|  
|DOUBLE|OPTION|User|  
|DROP|또는|VALUES|  
|DUMP|ORDER|VARYING|  
|ELSE|OUTER|VIEW|  
|END|OVER|WAITFOR|  
|ERRLVL|PERCENT|WHEN|  
|ESCAPE|PIVOT|WHERE|  
|EXCEPT|PLAN|WHILE|  
|EXEC|PRECISION|의 모든 멘션을|  
|CREATE 문을 실행하기 전에|PRIMARY|WITHIN GROUP|  
|EXISTS|PRINT|WRITETEXT|  
|EXIT|PROC||  
  
 또한 ISO 표준에서도 예약된 키워드 목록을 정의합니다. ISO 예약된 키워드를 개체 이름과 식별자에 사용하지 마십시오. 다음 표에 있는 ODBC 예약된 키워드 목록은 ISO 예약된 키워드 목록과 같습니다.  
  
> [!NOTE]  
>  ISO 표준 예약된 키워드 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]보다 더 제한적인 경우도 있고 덜 제한적인 경우도 있습니다. 예를 들어 ISO 예약 된 키워드 목록에 **INT**합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이것을 예약된 키워드로 구분할 필요가 없습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 예약된 키워드는 데이터베이스의 식별자나 이름 또는 데이터베이스 개체(예: 테이블, 열, 뷰 등)로 사용될 수 있습니다. 따옴표로 묶인 식별자나 구분 기호로 분리된 식별자를 사용합니다. 예약된 키워드를 변수 이름과 저장 프로시저 매개 변수로 사용하는 것은 제한되지 않습니다.  
  
## <a name="odbc-reserved-keywords"></a>ODBC 예약된 키워드  
 다음은 ODBC 함수 호출에 사용하기 위해 예약된 단어입니다. 예약된 키워드는 최소 SQL 문법을 강요하지 않지만 핵심 SQL 문법을 지원하는 드라이버와의 호환성을 위해 응용 프로그램에 이 키워드를 사용하지 마십시오.  
  
 다음은 ODBC 예약된 키워드의 현재 목록입니다.  
  
||||  
|-|-|-|  
|**절대**|**EXEC**|**겹치는 항목이 있습니다**|  
|**작업**|**EXECUTE**|**채움**|  
|**ADA**|**존재**|**부분**|  
|**추가**|**외부**|**파스칼**|  
|**ALL**|**추출**|**위치**|  
|**할당**|**FALSE**|**전체 자릿수**|  
|**ALTER**|**FETCH**|**준비**|  
|**AND**|**첫 번째**|**유지**|  
|**모든**|**FLOAT**|**PRIMARY**|  
|**는**|**에 대 한**|**사전**|  
|**AS**|**외부**|**권한**|  
|**ASC**|**포트란**|**프로시저**|  
|**어설션**|**찾을 수합니다**|**공개**|  
|**AT**|**FROM**|**읽기**|  
|**권한 부여**|**FULL**|**실제**|  
|**AVG**|**가져오기**|**참조**|  
|**BEGIN**|**전역**|**상대**|  
|**BETWEEN**|**이동**|**제한**|  
|**비트**|**GOTO**|**REVOKE**|  
|**BIT_LENGTH**|**GRANT**|**RIGHT**|  
|**둘 다**|**그룹**|**롤백**|  
|**에서**|**필요**|**행**|  
|**계단식 배열**|**1 시간**|**스키마**|  
|**캐스케이드**|**IDENTITY**|**스크롤**|  
|**대/소문자**|**직접 실행**|**두 번째**|  
|**캐스트**|**IN**|**섹션**|  
|**카탈로그**|**포함**|**SELECT**|  
|**CHAR**|**인덱스**|**세션**|  
|**CHAR_LENGTH**|**표시기**|**SESSION_USER**|  
|**문자**|**처음**|**설정**|  
|**CHARACTER_LENGTH**|**내부**|**크기**|  
|**확인**|**입력**|**SMALLINT**|  
|**닫기**|**구분 안 함**|**일부**|  
|**COALESCE**|**INSERT**|**공간**|  
|**한 부씩 인쇄**|**INT**|**SQL**|  
|**데이터 정렬**|**정수**|**SQLCA**|  
|**열**|**교차**|**SQLCODE**|  
|**커밋**|**간격**|**SQLERROR**|  
|**연결**|**에**|**SQLSTATE**|  
|**연결**|**IS**|**SQLWARNING**|  
|**제약 조건**|**격리**|**SUBSTRING**|  
|**제약 조건**|**조인**|**합계**|  
|**계속**|**키**|**SYSTEM_USER**|  
|**변환**|**LANGUAGE**|**테이블**|  
|**에 해당**|**마지막**|**임시**|  
|**개수**|**앞에**|**그런 다음**|  
|**만들기**|**LEFT**|**시간**|  
|**크로스**|**수준**|**타임 스탬프**|  
|**현재**|**LIKE**|**TIMEZONE_HOUR**|  
|**CURRENT_DATE**|**로컬**|**TIMEZONE_MINUTE**|  
|**CURRENT_TIME**|**더 낮은**|**받는 사람**|  
|**CURRENT_TIMESTAMP**|**MATCH**|**후행**|  
|**CURRENT_USER**|**최대**|**트랜잭션**|  
|**커서**|**MIN**|**번역하기**|  
|**날짜**|**분**|**번역**|  
|**일**|**모듈**|**TRIM**|  
|**할당 취소**|**월**|**TRUE**|  
|**년 12 월**|**이름**|**공용 구조체**|  
|**10 진수**|**NATIONAL**|**고유**|  
|**선언**|**자연**|**알 수 없음**|  
|**기본값**|**NCHAR**|**UPDATE**|  
|**연기할 수**|**다음**|**위쪽**|  
|**지연**|**아니요**|**사용**|  
|**DELETE**|**NONE**|**사용자**|  
|**DESC**|**NOT**|**사용 하 여**|  
|**설명**|**NULL**|**VALUE**|  
|**설명자**|**NULLIF**|**값**|  
|**진단**|**숫자**|**VARCHAR**|  
|**연결 끊기**|**OCTET_LENGTH**|**다양 한**|  
|**DISTINCT**|**의**|**보기**|  
|**도메인**|**ON**|**시기**|  
|**DOUBLE**|**만**|**때마다**|  
|**DROP**|**열기**|**WHERE**|  
|**ELSE**|**옵션**|**사용**|  
|**END**|**OR**|**작업**|  
|**EXEC 끝**|**순서**|**쓰기**|  
|**이스케이프**|**외부**|**연도**|  
|**제외 하**|**출력**|**영역**|  
|**예외**|||  
  
## <a name="future-keywords"></a>앞으로 사용될 키워드  
 다음은 앞으로 출시될 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 새 기능이 구현될 때 예약될 수 있는 키워드입니다. 다음 단어를 식별자로 사용하지 않는 것이 좋습니다.  
  
||||  
|-|-|-|  
|ABSOLUTE|HOST|RELATIVE|  
|ACTION|HOUR|RELEASE|  
|ADMIN|IGNORE|RESULT|  
|AFTER|IMMEDIATE|RETURNS|  
|AGGREGATE|INDICATOR|ROLE|  
|ALIAS|INITIALIZE|ROLLUP|  
|ALLOCATE|INITIALLY|ROUTINE|  
|ARE|INOUT|ROW|  
|ARRAY|INPUT|ROWS|  
|ASENSITIVE|INT|SAVEPOINT|  
|ASSERTION|INTEGER|SCROLL|  
|ASYMMETRIC|INTERSECTION|SCOPE|  
|AT|INTERVAL|SEARCH|  
|ATOMIC|ISOLATION|SECOND|  
|BEFORE|ITERATE|SECTION|  
|BINARY|LANGUAGE|SENSITIVE|  
|BIT|LARGE|SEQUENCE|  
|BLOB|LAST|SESSION|  
|BOOLEAN|LATERAL|SETS|  
|BOTH|LEADING|SIMILAR|  
|BREADTH|LESS|SIZE|  
|CALL|LEVEL|SMALLINT|  
|CALLED|LIKE_REGEX|SPACE|  
|CARDINALITY|LIMIT|SPECIFIC|  
|CASCADED|LN|SPECIFICTYPE|  
|CAST|LOCAL|SQL|  
|CATALOG|LOCALTIME|SQLEXCEPTION|  
|CHAR|LOCALTIMESTAMP|SQLSTATE|  
|CHARACTER|LOCATOR|SQLWARNING|  
|CLASS|MAP|START|  
|CLOB|MATCH|STATE|  
|COLLATION|MEMBER|STATEMENT|  
|COLLECT|METHOD|STATIC|  
|COMPLETION|MINUTE|STDDEV_POP|  
|CONDITION|MOD|STDDEV_SAMP|  
|CONNECT|MODIFIES|STRUCTURE|  
|CONNECTION|MODIFY|SUBMULTISET|  
|CONSTRAINTS|MODULE|SUBSTRING_REGEX|  
|CONSTRUCTOR|MONTH|SYMMETRIC|  
|CORR|MULTISET|SYSTEM|  
|CORRESPONDING|NAMES|TEMPORARY|  
|COVAR_POP|NATURAL|TERMINATE|  
|COVAR_SAMP|NCHAR|THAN|  
|CUBE|NCLOB|TIME|  
|CUME_DIST|NEW|timestamp|  
|CURRENT_CATALOG|NEXT|TIMEZONE_HOUR|  
|CURRENT_DEFAULT_TRANSFORM_GROUP|아니요|TIMEZONE_MINUTE|  
|CURRENT_PATH|없음|TRAILING|  
|CURRENT_ROLE|NORMALIZE|TRANSLATE_REGEX|  
|CURRENT_SCHEMA|NUMERIC|TRANSLATION|  
|CURRENT_TRANSFORM_GROUP_FOR_TYPE|OBJECT|TREAT|  
|CYCLE|OCCURRENCES_REGEX|TRUE|  
|DATA|OLD|UESCAPE|  
|DATE|ONLY|UNDER|  
|DAY|OPERATION|UNKNOWN|  
|DEC|ORDINALITY|UNNEST|  
|DECIMAL|OUT|USAGE|  
|DEFERRABLE|OVERLAY|USING|  
|DEFERRED|OUTPUT|Value|  
|DEPTH|PAD|VAR_POP|  
|DEREF|매개 변수|VAR_SAMP|  
|DESCRIBE|PARAMETERS|VARCHAR|  
|DESCRIPTOR|PARTIAL|VARIABLE|  
|DESTROY|PARTITION|WHENEVER|  
|DESTRUCTOR|PATH|WIDTH_BUCKET|  
|DETERMINISTIC|POSTFIX|WITHOUT|  
|DICTIONARY|PREFIX|WINDOW|  
|DIAGNOSTICS|PREORDER|WITHIN|  
|DISCONNECT|PREPARE|WORK|  
|DOMAIN|PERCENT_RANK|WRITE|  
|DYNAMIC|PERCENTILE_CONT|XMLAGG|  
|EACH|PERCENTILE_DISC|XMLATTRIBUTES|  
|ELEMENT|POSITION_REGEX|XMLBINARY|  
|END-EXEC|PRESERVE|XMLCAST|  
|EQUALS|PRIOR|XMLCOMMENT|  
|EVERY|PRIVILEGES|XMLCONCAT|  
|EXCEPTION|RANGE|XMLDOCUMENT|  
|FALSE|READS|XMLELEMENT|  
|FILTER|REAL|XMLEXISTS|  
|FIRST|RECURSIVE|XMLFOREST|  
|FLOAT|REF|XMLITERATE|  
|FOUND|REFERENCING|XMLNAMESPACES|  
|FREE|REGR_AVGX|XMLPARSE|  
|FULLTEXTTABLE|REGR_AVGY|XMLPI|  
|FUSION|REGR_COUNT|XMLQUERY|  
|GENERAL|REGR_INTERCEPT|XMLSERIALIZE|  
|GET|REGR_R2|XMLTABLE|  
|GLOBAL|REGR_SLOPE|XMLTEXT|  
|GO|REGR_SXX|XMLVALIDATE|  
|GROUPING|REGR_SXY|YEAR|  
|HOLD|REGR_SYY|ZONE|  
  
## <a name="see-also"></a>관련 항목:  
 [SET quoted_identifier&#40; Transact SQL &#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
