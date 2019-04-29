---
title: 프로그램 변수에서 대량 복사 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7c3a0eee5477b249bcde144aa6933851b2f61d5e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014045"
---
# <a name="bulk-copying-from-program-variables"></a>프로그램 변수에서 대량 복사
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  프로그램 변수에서 직접 대량 복사를 수행할 수 있습니다. 행의 데이터를 보유할 변수를 할당하고 [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 를 호출하여 대량 복사를 시작한 후 각 열에 대해 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 를 호출하여 열과 연결될 프로그램 변수의 위치와 서식을 지정합니다. 각 변수에 데이터를 채운 다음 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) 를 호출하여 데이터 행 하나를 서버에 전송합니다. 모든 행을 서버에 전송할 때까지 변수에 데이터를 채우고 **bcp_sendrow** 를 호출하는 과정을 반복한 후 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) 을 호출하여 작업이 완료되었음을 지정합니다.  
  
 **bcp_bind**_pData_ 매개 변수에는 열에 바인딩되는 변수의 주소가 포함됩니다. 각 열의 데이터는 다음 두 가지 방법 중 하나로 저장할 수 있습니다.  
  
-   데이터를 보유할 변수 할당  
  
-   데이터 변수 바로 앞에 표시자 변수 할당  
  
 표시자 변수는 가변 길이 열의 데이터 길이를 나타내고 열이 NULL을 허용하는 경우 NULL 값을 나타내기도 합니다. 데이터 변수만 사용하는 경우에는 이 변수의 주소가 **bcp_bind**_pData_ 매개 변수에 저장됩니다. 표시자 변수를 사용하는 경우에는 표시자 변수의 주소가 **bcp_bind**_pData_ 매개 변수에 저장됩니다. 대량 복사 함수는 **bcp_bind**_cbIndicator_ 및 *pData* 매개 변수를 더해 데이터 변수의 위치를 계산합니다.  
  
 **bcp_bind** 는 가변 길이 데이터를 처리하는 다음과 같은 세 가지 메서드를 지원합니다.  
  
-   데이터 변수 하나만 있는 *cbData* 사용. 데이터 길이를 *cbData*에 저장합니다. 길이의 데이터를 대량 복사 변경 될 때마다 호출 [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)재설정할 *cbData*합니다. 다른 두 메서드 중 하나를 사용할 경우에는 *cbData*에 SQL_VARLEN_DATA를 지정합니다. 열에 제공할 데이터 값이 모두 NULL인 경우에는 *cbData*에 SQL_NULL_DATA를 지정합니다.  
  
-   표시자 변수 사용. 각각의 새 데이터 값이 데이터 변수로 이동할 때 값 길이를 표시자 변수에 저장합니다. 다른 두 메서드 중 하나를 사용할 경우에는 *cbIndicator*에 0을 지정합니다.  
  
-   종결자 포인터 사용. 데이터를 종료하는 비트 패턴 주소를 사용하여 **bcp_bind**_pTerm_ 매개 변수를 로드합니다. 다른 두 메서드 중 하나를 사용할 경우에는 *pTerm*에 NULL을 지정합니다.  
  
 동일한 **bcp_bind** 호출에서 이 세 메서드를 모두 사용할 수 있습니다. 그럴 경우 가장 작은 양의 데이터를 복사하는 사양이 사용됩니다.  
  
 **bcp_bind**_type_ 매개 변수는 ODBC 데이터 형식 식별자가 아니라 DB-Library 데이터 형식 식별자를 사용합니다. DB-Library 데이터 형식 식별자는 ODBC **bcp_bind** 함수를 사용하여 sqlncli.h에서 정의됩니다.  
  
 대량 복사 함수는 일부 ODBC C 데이터 형식을 지원하지 않습니다. 예를 들어 대량 복사 함수는 ODBC SQL_C_TYPE_TIMESTAMP 구조체를 지원하지 않으므로 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) 또는 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 를 사용하여 ODBC SQL_TYPE_TIMESTAMP 데이터를 SQL_C_CHAR 변수로 변환해야 합니다. 그런 다음 SQLCHARACTER의 **bcp_bind** 매개 변수와 함께 *bcp_bind* 를 사용하여 변수를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 열에 바인딩하면 대량 복사 함수가 문자 변수의 타임스탬프 이스케이프 절을 적절한 날짜 시간 형식으로 변환합니다.  
  
 다음 표에는 ODBC SQL 데이터 형식과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 간의 매핑에 대한 권장 데이터 형식이 정리되어 있습니다.  
  
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
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서명 되지 않습니다 **tinyint**부호 없는 **smallint**, 또는 서명 되지 않은 **int** 데이터 형식입니다. 이러한 데이터 형식을 마이그레이션할 때 데이터 값이 손실되지 않게 하려면 다음으로 큰 정수 데이터 형식을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만드십시오. 나중에 사용자가 원래 데이터 형식에서 허용되는 범위를 벗어나는 값을 추가하지 못하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열에 원래 원본의 데이터 형식에서 지원하는 범위로 사용 가능한 값을 제한하는 규칙을 적용합니다.  
  
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
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 interval 데이터 형식을 직접 지원하지 않습니다. 하지만 애플리케이션에서 interval 이스케이프 시퀀스를 문자열로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 열에 저장할 수 있습니다. 나중에 애플리케이션에서 이러한 문자열을 읽을 수 있지만 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에는 해당 문자열을 사용할 수 없습니다.  
  
 대량 복사 함수를 사용하면 ODBC 데이터 원본에서 읽은 데이터를 빠르게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 로드할 수 있습니다. 데이터 변수 하나만 있는 [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) 의 지침에 따라 결과 집합의 열을 프로그램 변수에 바인딩한 후 **bcp_bind** 를 사용하여 동일한 프로그램 변수를 대량 복사 작업에 바인딩합니다. 호출 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) 하거나 **SQLFetch** 프로그램 변수 및 호출에 ODBC 데이터 원본에서 데이터 행을 페치합니다 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) 데이터를 대량 복사 프로그램 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
 응용 프로그램이 사용할 수는 [bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md) 변수에 원래 지정 된 데이터 변수의 주소를 변경 해야 할 때마다 함수는 **bcp_bind** _pData_ 매개 변수입니다. 또한 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) cbData **매개 변수에 원래 지정된 데이터 길이를 변경해야 할 경우에는**_bcp_collen_ 함수를 사용할 수 있습니다.  
  
 "bcp_readrow" 함수에 해당하는 기능이 없기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 대량 복사를 사용하여 프로그램 변수로 데이터를 읽어들일 수는 없으며 애플리케이션에서 서버로 데이터를 보낼 수만 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 작업 수행 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
