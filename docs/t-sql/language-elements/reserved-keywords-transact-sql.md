---
title: "예약 된 키워드 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 65ef776b119b40bbeb4bbdddcfe0a4a99379a833
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="reserved-keywords-transact-sql"></a>예약어(Transact-SQL)
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
|DOUBLE|OPTION|USER|  
|DROP|OR|VALUES|  
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
|**ABSOLUTE**|**EXEC**|**OVERLAPS**|  
|**작업**|**EXECUTE**|**PAD**|  
|**ADA**|**EXISTS**|**부분**|  
|**ADD**|**외부**|**PASCAL**|  
|**ALL**|**EXTRACT**|**위치**|  
|**ALLOCATE**|**FALSE**|**전체 자릿수**|  
|**ALTER**|**FETCH**|**준비**|  
|**및**|**FIRST**|**유지**|  
|**ANY**|**FLOAT**|**PRIMARY**|  
|**는**|**에 대 한**|**사전**|  
|**AS**|**외부**|**권한**|  
|**ASC**|**포트란**|**PROCEDURE**|  
|**어설션**|**찾을 수합니다**|**PUBLIC**|  
|**AT**|**FROM**|**READ**|  
|**AUTHORIZATION**|**FULL**|**REAL**|  
|**AVG**|**GET**|**참조**|  
|**BEGIN**|**GLOBAL**|**상대**|  
|**BETWEEN**|**GO**|**제한**|  
|**BIT**|**GOTO**|**REVOKE**|  
|**BIT_LENGTH**|**GRANT**|**RIGHT**|  
|**BOTH**|**GROUP**|**롤백**|  
|**BY**|**HAVING**|**ROWS**|  
|**CASCADE**|**HOUR**|**SCHEMA**|  
|**CASCADED**|**IDENTITY**|**SCROLL**|  
|**CASE**|**IMMEDIATE**|**두 번째**|  
|**CAST**|**IN**|**섹션**|  
|**CATALOG**|**INCLUDE**|**SELECT**|  
|**CHAR**|**INDEX**|**세션**|  
|**CHAR_LENGTH**|**INDICATOR**|**SESSION_USER**|  
|**CHARACTER**|**INITIALLY**|**SET**|  
|**CHARACTER_LENGTH**|**INNER**|**SIZE**|  
|**CHECK**|**INPUT**|**SMALLINT**|  
|**CLOSE**|**구분 안 함**|**SOME**|  
|**COALESCE**|**INSERT**|**SPACE**|  
|**COLLATE**|**INT**|**SQL**|  
|**데이터 정렬**|**INTEGER**|**SQLCA**|  
|**COLUMN**|**INTERSECT**|**SQLCODE**|  
|**COMMIT**|**INTERVAL**|**SQLERROR**|  
|**CONNECT**|**INTO**|**SQLSTATE**|  
|**연결**|**은**|**SQLWARNING**|  
|**CONSTRAINT**|**격리**|**SUBSTRING**|  
|**CONSTRAINTS**|**JOIN**|**SUM**|  
|**CONTINUE**|**KEY**|**SYSTEM_USER**|  
|**CONVERT**|**LANGUAGE**|**TABLE**|  
|**에 해당**|**LAST**|**임시**|  
|**COUNT**|**앞에**|**그런 다음**|  
|**CREATE**|**LEFT**|**TIME**|  
|**CROSS**|**LEVEL**|**타임 스탬프**|  
|**CURRENT**|**LIKE**|**TIMEZONE_HOUR**|  
|**CURRENT_DATE**|**LOCAL**|**TIMEZONE_MINUTE**|  
|**CURRENT_TIME**|**LOWER**|**TO**|  
|**CURRENT_TIMESTAMP**|**MATCH**|**TRAILING**|  
|**CURRENT_USER**|**MAX**|**TRANSACTION**|  
|**CURSOR**|**MIN**|**TRANSLATE**|  
|**DATE**|**MINUTE**|**번역**|  
|**DAY**|**모듈**|**TRIM**|  
|**DEALLOCATE**|**MONTH**|**TRUE**|  
|**DEC**|**NAMES**|**공용 구조체**|  
|**DECIMAL**|**NATIONAL**|**고유**|  
|**선언**|**자연**|**UNKNOWN**|  
|**DEFAULT**|**NCHAR**|**UPDATE**|  
|**연기할 수**|**NEXT**|**UPPER**|  
|**지연**|**NO**|**USAGE**|  
|**DELETE**|**NONE**|**USER**|  
|**DESC**|**NOT**|**USING**|  
|**설명**|**NULL**|**VALUE**|  
|**DESCRIPTOR**|**NULLIF**|**VALUES**|  
|**DIAGNOSTICS**|**NUMERIC**|**VARCHAR**|  
|**연결 끊기**|**OCTET_LENGTH**|**다양 한**|  
|**DISTINCT**|**OF**|**VIEW**|  
|**도메인**|**ON**|**WHEN**|  
|**DOUBLE**|**ONLY**|**WHENEVER**|  
|**DROP**|**OPEN**|**WHERE**|  
|**ELSE**|**옵션**|**WITH**|  
|**END**|**OR**|**작업**|  
|**END-EXEC**|**ORDER**|**WRITE**|  
|**ESCAPE**|**OUTER**|**YEAR**|  
|**EXCEPT**|**OUTPUT**|**ZONE**|  
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
|CUME_DIST|NEW|TIMESTAMP|  
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
|DEFERRED|OUTPUT|VALUE|  
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
  
  
