---
title: HASHBYTES (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HASHBYTES_TSQL
- HASHBYTES
dev_langs: TSQL
helpviewer_keywords:
- hash input
- HASHBYTES
ms.assetid: 0ea6a4d1-313e-4f70-b939-dd2cd570f6d6
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 63552f4b6fb61b3b24d4d670b9ea255d8e417699
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="hashbytes-transact-sql"></a>HASHBYTES(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 해당 입력의 MD2, MD4, MD5, SHA, SHA1 또는 SHA2 해시를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
HASHBYTES ( '<algorithm>', { @input | 'input' } )  
  
<algorithm>::= MD2 | MD4 | MD5 | SHA | SHA1 | SHA2_256 | SHA2_512   
```  
  
## <a name="arguments"></a>인수  
 **'**\<알고리즘 >**'**  
 입력 해시에 사용할 해싱 알고리즘을 나타냅니다. 필수 인수이며 기본값은 없습니다. 작은따옴표가 필요합니다. 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], SHA2_256, 및 SHA2_512 이외의 모든 알고리즘에 사용 되지 않습니다. (권장 하지 않음) 하는 오래 된 알고리즘 작동을 계속할 수 있지만 이러한 deprecation 이벤트가 발생 합니다.  
  
 **@input**  
 해시할 데이터를 포함하는 변수를 지정합니다. **@input****varchar**, **nvarchar**, 또는 **varbinary**합니다.  
  
 **'** *입력* **'**  
 해시할 문자 또는 이진 문자열로 계산되는 식을 지정합니다.  
  
 출력 알고리즘 표준을 준수: MD2, MD4 및 m d 5에 대 한 128 비트 (16 바이트) SHA 및 SHA1; 160 비트 (20 바이트) SHA2_256, 256 비트 (32 바이트) 및 SHA2_512 512 비트 (64 바이트)입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 에 대 한 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 이전 버전에서 허용 되는 입력된 값은 8000 바이트로 제한 됩니다.  
  
## <a name="return-value"></a>반환 값  
 **varbinary** (최대 8000 바이트)  
  
## <a name="examples"></a>예  
  
### <a name="a-return-the-hash-of-a-variable"></a>A: 변수의 해시 반환  
 다음 예제에서는 반환 된 `SHA1` 의 해시는 **nvarchar** 변수에 저장 된 데이터 `@HashThis`합니다.  
  
```  
DECLARE @HashThis nvarchar(4000);  
SET @HashThis = CONVERT(nvarchar(4000),'dslfdkjLK85kldhnv$n000#knf');  
SELECT HASHBYTES('SHA1', @HashThis);  
  
```  
  
### <a name="b-return-the-hash-of-a-table-column"></a>B:에는 테이블 열의 해시 반환  
 다음 예에서는 `c1` 테이블의 `Test1` 열에 있는 값의 SHA1 해시를 반환합니다.  
  
```  
CREATE TABLE dbo.Test1 (c1 nvarchar(50));  
INSERT dbo.Test1 VALUES ('This is a test.');  
INSERT dbo.Test1 VALUES ('This is test 2.');  
SELECT HASHBYTES('SHA1', c1) FROM dbo.Test1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
-------------------------------------------  
0x0E7AAB0B4FF0FD2DFB4F0233E2EE7A26CD08F173  
0xF643A82F948DEFB922B12E50B950CEE130A934D6  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
