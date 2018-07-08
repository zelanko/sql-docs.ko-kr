---
title: 프로그램 변수에서 대량 복사 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], program variables
- bcp_bind function
- mapping data types [ODBC]
- SQL Server Native Client ODBC driver, bulk copy
- data types [ODBC], bulk copying
- ODBC, bulk copy operations
- program variables [ODBC]
ms.assetid: e4284a1b-7534-4b34-8488-b8d05ed67b8c
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 253123cc62751c39c39e9f5ab9282e2b1e6a3c10
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420022"
---
# <a name="bulk-copying-from-program-variables"></a>프로그램 변수에서 대량 복사
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  프로그램 변수에서 직접 대량 복사를 수행할 수 있습니다. 행 및 호출에 대 한 데이터를 저장할 변수를 할당 한 후 [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 대량 복사를 시작 하려면 호출 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 위치와 연결 될 프로그램 변수의 서식을 지정 하기 위해 각 열에 대 한 열이 있습니다. 각 변수에 데이터를 사용 하 여 호출 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) 서버로 데이터 행 하나를 보내려고 합니다. 변수를 채우고 호출 하는 과정을 반복할 **bcp_sendrow** 서버로 보낸 모든 행을 될 때까지 호출 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) 작업이 완료 되도록 합니다.  
  
 **bcp_bind * pData* 매개 변수 열에 바인딩되는 변수의 주소가 포함 되어 있습니다. 각 열의 데이터는 다음 두 가지 방법 중 하나로 저장할 수 있습니다.  
  
-   데이터를 보유할 변수 할당  
  
-   데이터 변수 바로 앞에 표시자 변수 할당  
  
 표시자 변수는 가변 길이 열의 데이터 길이를 나타내고 열이 NULL을 허용하는 경우 NULL 값을 나타내기도 합니다. 데이터 변수만 사용 하는 경우 다음이 변수의 주소가에 저장 됩니다는 **bcp_bind * pData* 매개 변수입니다. 표시기 변수에 대 한 주소에 저장 됩니다 표시기 변수를 사용 하는 경우는 **bcp_bind * pData* 매개 변수입니다. 해 데이터 변수의 위치를 계산 하는 대량 복사 함수는 **bcp_bind * cbIndicator* 하 고 *pData* 매개 변수입니다.  
  
 **bcp_bind** 는 가변 길이 데이터를 처리하는 다음과 같은 세 가지 메서드를 지원합니다.  
  
-   데이터 변수 하나만 있는 *cbData* 사용. 데이터 길이를 *cbData*에 저장합니다. 길이의 데이터를 대량 복사 변경 될 때마다 호출 [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)재설정할 *cbData*합니다. 다른 두 메서드 중 하나를 사용할 경우에는 *cbData*에 SQL_VARLEN_DATA를 지정합니다. 열에 제공할 데이터 값이 모두 NULL인 경우에는 *cbData*에 SQL_NULL_DATA를 지정합니다.  
  
-   표시자 변수 사용. 각각의 새 데이터 값이 데이터 변수로 이동할 때 값 길이를 표시자 변수에 저장합니다. 다른 두 메서드 중 하나를 사용할 경우에는 *cbIndicator*에 0을 지정합니다.  
  
-   종결자 포인터 사용. 부하는 **bcp_bind * pTerm* 데이터를 종료 하는 비트 패턴 주소를 사용 하 여 매개 변수입니다. 다른 두 메서드 중 하나를 사용할 경우에는 *pTerm*에 NULL을 지정합니다.  
  
 동일한 **bcp_bind** 호출에서 이 세 메서드를 모두 사용할 수 있습니다. 그럴 경우 가장 작은 양의 데이터를 복사하는 사양이 사용됩니다.  
  
 **bcp_bind * * * 형식* 매개 변수는 Db-library 데이터 형식 식별자를 ODBC 데이터 형식 식별자가 없습니다. DB-Library 데이터 형식 식별자는 ODBC **bcp_bind** 함수를 사용하여 sqlncli.h에서 정의됩니다.  
  
 대량 복사 함수는 일부 ODBC C 데이터 형식을 지원하지 않습니다. 예를 들어 대량 복사 함수를 지원 하지는 ODBC SQL_C_TYPE_TIMESTAMP 구조체 사용 하므로 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) 또는 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) ODBC SQL_TYPE_TIMESTAMP 데이터를 SQL_C_CHAR 변수로 변환. 다음 사용 하는 경우 **bcp_bind** 사용 하 여를 *형식* 변수를 바인딩할 SQLCHARACTER의 매개 변수를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 열에 대량 복사 함수 변환 합니다 적절 한 날짜/시간 형식으로 문자 변수의 타임 스탬프 이스케이프 절.  
  
 다음 표에서 ODBC SQL 데이터 형식에서 매핑에 대 한 권장된 데이터 형식이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
|ODBC SQL 데이터 형식|ODBC C 데이터 형식|bcp_bind *type* 매개 변수|SQL Server 데이터 형식|  
|-----------------------|----------------------|--------------------------------|--------------------------|  
|SQL_CHAR|SQL_C_CHAR|SQLCHARACTER|**character**<br /><br /> **char**|  
|SQL_VARCHAR|SQL_C_CHAR|SQLCHARACTER|**varchar**<br /><br /> **다양 한 문자**<br /><br /> **char varying**<br /><br /> **sysname**|  
|SQL_LONGVARCHAR|SQL_C_CHAR|SQLCHARACTER|**text**|  
|SQL_WCHAR|SQL_C_WCHAR|SQLNCHAR|**nchar**|  
|SQL_WVARCHAR|SQL_C_WCHAR|SQLNVARCHAR|**nvarchar**|  
|SQL_WLONGVARCHAR|SQL_C_WCHAR|SQLNTEXT|**ntext**|  
|SQL_DECIMAL|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**<br /><br /> **money**<br /><br /> **smallmoney**|  
|SQL_NUMERIC|SQL_C_NUMERIC|SQLNUMERICN|**numeric**|  
|SQL_BIT|SQL_C_BIT|SQLBIT|**bit**|  
|SQL_TINYINT(부호 있음)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_TINYINT(부호 없음)|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT(부호 있음)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_SMALL_INT(부호 없음)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER(부호 있음)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER(부호 없음)|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**|  
|SQL_BIGINT(부호 있음 및 부호 없음)|SQL_C_CHAR|SQLCHARACTER|**bigint**|  
|SQL_REAL|SQL_C_FLOAT|SQLFLT4|**real**|  
|SQL_FLOAT|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_DOUBLE|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_BINARY|SQL_C_BINARY|SQLBINARY|**binary**<br /><br /> **timestamp**|  
|SQL_VARBINARY|SQL_C_BINARY|SQLBINARY|**varbinary**<br /><br /> **binary varying**|  
|SQL_LONGVARBINARY|SQL_C_BINARY|SQLBINARY|**image**|  
|SQL_TYPE_DATE|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIME|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIMESTAMP|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_GUID|SQL_C_GUID|SQLUNIQUEID|**uniqueidentifier**|  
|SQL_INTERVAL_|SQL_C_CHAR|SQLCHARACTER|**char**|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서명 되지 않습니다 **tinyint**부호 없는 **smallint**, 또는 서명 되지 않은 **int** 데이터 형식입니다. 이러한 데이터 형식을 마이그레이션할 때 데이터 값의 손실을 방지 하려면 만들기를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음 가장 큰 정수 데이터 형식 사용 하 여 테이블입니다. 나중에 사용자가 원래 데이터 형식에서 허용되는 범위를 벗어나는 값을 추가하지 못하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열에 원래 원본의 데이터 형식에서 지원하는 범위로 사용 가능한 값을 제한하는 규칙을 적용합니다.  
  
```  
CREATE TABLE Sample_Ints(STinyIntCol   SMALLINT,  
USmallIntCol INT)  
GO  
CREATE RULE STinyInt_Rule  
AS   
@range >= -128 AND @range <= 127  
GO  
CREATE RULE USmallInt_Rule  
AS   
@range >= 0 AND @range <= 65535  
GO  
sp_bindrule STinyInt_Rule, 'Sample_Ints.STinyIntCol'  
GO  
sp_bindrule USmallInt_Rule, 'Sample_Ints.USmallIntCol'  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interval 데이터 형식을 직접 지원 하지 않습니다. 그러나 응용 프로그램에서 문자열로 interval 이스케이프 시퀀스를 저장할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 열입니다. 나중에 응용 프로그램에서 이러한 문자열을 읽을 수 있지만 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에는 해당 문자열을 사용할 수 없습니다.  
  
 대량 복사 함수를 사용 하 여 신속 하 게 데이터를 로드할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 데이터 원본에서 읽은 합니다. 사용 하 여 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) 열의 결과 집합을 프로그램 변수에 바인딩할 사용 **bcp_bind** 대량 복사 작업에 동일한 프로그램 변수를 바인딩할 합니다. 호출 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) 하거나 **SQLFetch** 프로그램 변수 및 호출에 ODBC 데이터 원본에서 데이터 행을 페치합니다 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) 데이터를 대량 복사 프로그램 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
 응용 프로그램이 사용할 수는 [bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md) 변수에 원래 지정 된 데이터 변수의 주소를 변경 해야 할 때마다 함수는 **bcp_bind** *pData* 매개 변수입니다. 응용 프로그램이 사용할 수는 [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) 변수에 원래 지정 된 데이터 길이 변경 해야 할 때마다 함수는 **bcp_bind * * * cbData* 매개 변수입니다.  
  
 데이터를 읽을 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 복사를 사용 하 여 프로그램 변수로 "bcp_readrow" 함수입니다. 응용 프로그램에서 서버로 데이터를 보낼 수만 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 작업 수행 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
