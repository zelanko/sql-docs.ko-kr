---
description: SET ANSI_PADDING(Transact-SQL)
title: SET ANSI_PADDING(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ANSI_PADDING_TSQL
- ANSI_PADDING
- SET_ANSI_PADDING_TSQL
- SET ANSI_PADDING
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], short values
- ANSI_PADDING option
- short values [SQL Server]
- SET ANSI_PADDING statement
- trailing blanks
ms.assetid: 92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f764b11533be2eb6e6e4a71e5b0fe388da9bdcc6
ms.sourcegitcommit: 644223c40af7168f9d618526e9f4cd24e115d1db
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328091"
---
# <a name="set-ansi_padding-transact-sql"></a>SET ANSI_PADDING(Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  열이 정의된 열 크기보다 짧은 값을 저장하는 방법과 **char**, **varchar**, **binary** 및 **varbinary** 데이터에 후행 공백이 있는 값을 저장하는 방법을 제어합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문
 
### <a name="syntax-for-ssnoversion-mdmd-and-sssodfull-mdmd"></a>[!INCLUDE[ssnoversion-md.md](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[sssodfull-md.md](../../includes/sssodfull-md.md)] 구문 
```syntaxsql
SET ANSI_PADDING { ON | OFF }
```

### <a name="syntax-for-sssdw-mdmd-and-sspdw-mdmd"></a>[!INCLUDE[sssdw-md.md](../../includes/sssdw-md.md)] 및 [!INCLUDE[sspdw-md.md](../../includes/sspdw-md.md)] 구문
```syntaxsql
SET ANSI_PADDING ON
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명
 **char**, **varchar**, **binary** 및 **varbinary** 데이터 형식으로 정의된 열에는 정의된 크기가 있습니다.  
  
 이 설정은 새 열의 정의에만 영향을 줍니다. 열이 생성된 다음에는 열을 만들 때의 설정에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 값을 저장합니다. 나중에 이 설정을 변경해도 기존의 열은 영향을 받지 않습니다.  
  
> [!NOTE]  
> ANSI_PADDING은 항상 ON으로 설정해야 합니다.  
  
 다음 표에서는 **char**, **varchar**, **binary** 및 **varbinary** 데이터 형식의 열에 값을 삽입할 때 SET ANSI_PADDING 설정의 결과를 보여 줍니다.  
  
|설정|char(*n*) NOT NULL 또는 binary(*n*) NOT NULL|char(*n*) NULL 또는 binary(*n*) NULL|varchar(*n*) 또는 varbinary(*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|켜기|열의 크기만큼 오른쪽으로 원래 값(**char** 열에 대해서는 후행 공백으로, **binary** 열에 대해서는 후행 0으로)을 채웁니다.|SET ANSI_PADDING이 ON일 때는 **char(** _n_ **)** 또는 **binary(** _n_ **)** NOT NULL과 동일한 규칙을 따릅니다.|**varchar** 열에 삽입된 문자 값의 후행 공백은 잘리지 않습니다. **varbinary** 열에 삽입된 이진 값 뒤에 오는 0은 잘리지 않습니다. 값은 열의 크기만큼 오른쪽에 공백으로 채워집니다.|  
|OFF|열의 크기만큼 오른쪽으로 원래 값(**char** 열에 대해서는 후행 공백으로, **binary** 열에 대해서는 후행 0으로)을 채웁니다.|SET ANSI_PADDING 옵션이 OFF일 때 **varchar** 또는 **varbinary** 의 경우와 같은 규칙을 따릅니다.|**varchar** 열에 삽입된 문자 값의 후행 공백은 잘립니다. **varbinary** 열에 삽입된 이진 값 뒤에 오는 0은 잘립니다.|  
  
> [!NOTE]  
> 채워질 때 **char** 열은 공백으로, **binary** 열은 0으로 채워집니다. 잘릴 때 **char** 열에서는 후행 공백이, **binary** 열에서는 뒤에 오는 0이 잘립니다.  
  
계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때는 ANSI_PADDING을 ON으로 설정해야 합니다. 인덱싱된 뷰 및 계산 열의 인덱스에 사용되는 필수 SET 옵션 설정에 대한 자세한 내용은 [SET Statements &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)에서 "SET 문 사용 시 고려 사항"을 참조하세요.  
  
SET ANSI_PADDING의 기본값은 ON입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 연결될 때 자동으로 ANSI_PADDING을 ON으로 설정합니다. ODBC 데이터 원본과 ODBC 연결 특성 또는, SQL Server에 연결하기 전에 애플리케이션에 설정된 OLE DB 연결 속성에서 이 옵션을 구성할 수 있습니다. DB-Library 애플리케이션에서 연결하는 경우 SET ANSI_PADDING의 기본값은 OFF입니다.  
  
 SET ANSI_PADDING 설정은 **nchar**, **nvarchar**, **ntext**, **text**, **image**, **varbinary(max)**, **varchar(max)** 및 **nvarchar(max)** 데이터 형식에는 영향을 주지 않습니다. 이 설정은 항상 SET ANSI_PADDING ON 동작을 표시합니다. 즉, 후행 공백과 뒤에 오는 0은 잘리지 않는다는 의미입니다.  
  
ANSI_DEFAULTS가 ON이면 ANSI_PADDING이 활성화됩니다.  
  
ANSI_PADDING의 설정은 실행 시 또는 런타임에 정의되며 구문 분석 시에는 정의되지 않습니다.  
  
이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.  
  
```sql  
DECLARE @ANSI_PADDING VARCHAR(3) = 'OFF';  
IF ( (16 & @@OPTIONS) = 16 ) SET @ANSI_PADDING = 'ON';  
SELECT @ANSI_PADDING AS ANSI_PADDING;  
```  
  
## <a name="permissions"></a>사용 권한  
**public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
다음 예에서는 설정이 다음과 같은 각 데이터 형식에 영향을 미치는 방법을 보여 줍니다.  

ANSI_PADDING을 ON으로 설정하고 테스트합니다.

```sql  
PRINT 'Testing with ANSI_PADDING ON'  
SET ANSI_PADDING ON;  
GO  
  
CREATE TABLE t1 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t1 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t1 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '\<',  
   varbinarycol  
FROM t1;  
GO  
```

이제 ANSI_PADDING을 OFF로 설정하고 테스트합니다.

```sql
PRINT 'Testing with ANSI_PADDING OFF';  
SET ANSI_PADDING OFF;  
GO  
  
CREATE TABLE t2 (  
   charcol CHAR(16) NULL,   
   varcharcol VARCHAR(16) NULL,   
   varbinarycol VARBINARY(8)  
);  
GO  
INSERT INTO t2 VALUES ('No blanks', 'No blanks', 0x00ee);  
INSERT INTO t2 VALUES ('Trailing blank ', 'Trailing blank ', 0x00ee00);  
  
SELECT 'CHAR' = '>' + charcol + '\<', 'VARCHAR'='>' + varcharcol + '<',  
   varbinarycol  
FROM t2;  
GO  
  
DROP TABLE t1;  
DROP TABLE t2;  
```  
  
## <a name="see-also"></a>참고 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  
