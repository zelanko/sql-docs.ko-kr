---
title: SET ANSI_PADDING (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ANSI_PADDING_TSQL
- ANSI_PADDING
- SET_ANSI_PADDING_TSQL
- SET ANSI_PADDING
dev_langs: TSQL
helpviewer_keywords:
- data types [SQL Server], short values
- ANSI_PADDING option
- short values [SQL Server]
- SET ANSI_PADDING statement
- trailing blanks
ms.assetid: 92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0
caps.latest.revision: "47"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 532df95a03b15d545c682d30b3b4d68e10ea5913
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="set-ansipadding-transact-sql"></a>SET ANSI_PADDING(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  열이 정의된 열 크기보다 짧은 값을 저장하는 방법과 **char**, **varchar**, **binary**및 **varbinary** 데이터에 후행 공백이 있는 값을 저장하는 방법을 제어합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문
  
```
-- Syntax for SQL Server

SET ANSI_PADDING { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_PADDING ON
```

## <a name="remarks"></a>주의  
 으로 정의 된 열 **char**, **varchar**, **이진**, 및 **varbinary** 데이터 형식에 정의 된 크기는 합니다.  
  
 이 설정은 새 열의 정의에만 영향을 줍니다. 열이 생성된 다음에는 열을 만들 때의 설정에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 값을 저장합니다. 나중에 이 설정을 변경해도 기존의 열은 영향을 받지 않습니다.  
  
> [!NOTE]  
>  ANSI_PADDING은 항상 ON으로 설정하는 것이 좋습니다.  
  
 다음 표에서 값을 가진 열에 삽입할 때 SET ANSI_PADDING 설정의 효과 보여 줍니다 **char**, **varchar**, **이진**, 및  **varbinary** 데이터 형식입니다.  
  
|설정|char (*n*) 하지 NULL 또는 binary (*n*) NOT NULL|char (*n*) NULL 또는 binary (*n*) NULL|varchar (*n*) 또는 varbinary (*n*)|  
|-------------|----------------------------------------------------|--------------------------------------------|----------------------------------------|  
|ON|원래 값 (후행 공백으로 대 한 **char** 열 후행 0에 대 한으로 **이진** 열) 열의 길이입니다.|와 같은 규칙을 따르는 **char (***n***)** 또는 **이진 (**  *n*  **)** NOT SET ANSI_PADDING이 ON 일 때 NULL입니다.|삽입 된 문자 값의 후행 공백과 **varchar** 열이 잘리지 않습니다. 뒤에 오는 0에 삽입 된 이진 값의 **varbinary** 열이 잘리지 않습니다. 값은 열의 크기만큼 오른쪽에 공백으로 채워집니다.|  
|OFF|원래 값 (후행 공백으로 대 한 **char** 열 후행 0에 대 한으로 **이진** 열) 열의 길이입니다.|와 같은 규칙을 따르는 **varchar** 또는 **varbinary** 때 SET ANSI_PADDING이 OFF입니다.|에 삽입 된 문자 값의 후행 공백과 **varchar** 열 잘립니다. 뒤에 오는 0에 삽입 된 이진 값에는 **varbinary** 열 잘립니다.|  
  
> [!NOTE]  
>  채워질 때 **char** 열은 공백으로 및 **이진** 열은 0으로 채워집니다. 잘릴 때 **char** 열에 후행 공백이 잘리고, 있어야 하 고 **이진** 열 뒤에 오는 0 잘리지에 있어야 합니다.  
  
 계산 열이나 인덱싱된 뷰에서 인덱스를 만들거나 변경할 때는 SET ANSI_PADDING을 ON으로 설정해야 합니다. 계산된 열에 인덱스 및 인덱싱된 뷰에 필요한 SET 옵션 설정에 대 한 자세한 내용은 "고려 사항 때 설정 문 사용"의 참조 [SET 문 &#40; Transact SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 SET ANSI_PADDING의 기본값은 ON입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 될 때 자동으로 ANSI_PADDING을 ON으로 설정 합니다. ODBC 데이터 원본과 ODBC 연결 특성 또는, SQL Server에 연결하기 전에 응용 프로그램에 설정된 OLE DB 연결 속성에서 이 옵션을 구성할 수 있습니다. DB-Library 응용 프로그램에서 연결하는 경우 SET ANSI_PADDING의 기본값은 OFF입니다.  
  
 SET ANSI_PADDING 설정에 영향을 주지 않습니다는 **nchar**, **nvarchar**, **ntext**, **텍스트**, **이미지**, **varbinary (max)**, **varchar (max)**, 및 **nvarchar (max)** 데이터 형식입니다. 이 설정은 항상 SET ANSI_PADDING ON 동작을 표시합니다. 즉, 후행 공백과 뒤에 오는 0은 잘리지 않는다는 의미입니다.  
  
 SET ANSI_DEFAULTS가 ON이면 SET ANSI_PADDING이 설정됩니다.  
  
 SET ANSI_PADDING은 실행 시간이나 런타임에 설정되며 구문 분석 시간에는 설정되지 않습니다.  
  
 이 설정에 대한 현재 설정을 보려면 다음 쿼리를 실행합니다.  
  
```  
DECLARE @ANSI_PADDING VARCHAR(3) = 'OFF';  
IF ( (16 & @@OPTIONS) = 16 ) SET @ANSI_PADDING = 'ON';  
SELECT @ANSI_PADDING AS ANSI_PADDING;  
  
```  
  
## <a name="permissions"></a>Permissions  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 설정이 다음과 같은 각 데이터 형식에 영향을 미치는 방법을 보여 줍니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40; Transact SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40; Transact SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  
