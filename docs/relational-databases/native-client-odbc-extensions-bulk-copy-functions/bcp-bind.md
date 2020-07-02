---
title: bcp_bind | Microsoft Docs
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_bind
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.reviewer: ''
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1716c650a138edd36291e20877faf5da741b92a7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787949"
---
# <a name="bcp_bind"></a>bcp_bind

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 대량 복사를 수행하기 위해 프로그램 변수에서 테이블 열로 데이터를 바인딩합니다.  

## <a name="syntax"></a>구문

```  
  
RETCODE bcp_bind (  
        HDBC hdbc,
        LPCBYTE pData,  
        INT cbIndicator,  
        DBINT cbData,  
        LPCBYTE pTerm,  
        INT cbTerm,  
        INT eDataType,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>인수

 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *pData*  
 복사 대상 데이터에 대한 포인터입니다. *Edatatype* 이 sqltext, SQLTEXT, SQLXML, sqltext, SQLTEXT, sqltext, SQLTEXT, SQLBINARY, sqltext 또는 SQLIMAGE 인 경우 *.pdata* 는 NULL 일 수 있습니다. NULL *.pdata* 는 긴 데이터 값이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)를 사용 하 여 청크로 전송 됨을 나타냅니다. 사용자가 바인딩된 필드에 해당 하는 열이 BLOB 열인 경우에는 사용자가 *.pdata* 만 NULL로 설정 해야 합니다. 그렇지 않으면 **bcp_bind** 이 실패 합니다.  
  
 데이터에 표시자가 있으면 이는 메모리에서 데이터 바로 앞에 표시됩니다. *.Pdata* 매개 변수는이 경우 표시기 변수를 가리키며 표시기의 너비 인 *cbindicator* 매개 변수는 대량 복사에서 사용자 데이터를 올바르게 처리 하는 데 사용 됩니다.  
  
 *cbIndicator*  
 열 데이터의 길이 또는 Null 표시자의 바이트 단위 길이입니다. 올바른 표시기 길이 값은 0(표시기를 사용하지 않을 경우), 1, 2, 4 또는 8입니다. 표시자는 메모리에서 데이터 바로 앞에 표시됩니다. 예를 들어 대량 복사를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 정수 값을 삽입하기 위해 다음 구조 형식 정의를 사용할 수 있습니다.  
  
```
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 예제 사례에서 *.pdata* 매개 변수는 구조체의 선언 된 인스턴스 주소 (BCPBOUNDINT *iindicator* 구조체 멤버의 주소)로 설정 됩니다. *Cbindicator* 매개 변수는 정수 크기 (sizeof (int))로 설정 되 고, *cbindicator* 매개 변수는 다시 정수 크기 (sizeof (int))로 설정 됩니다. 바인딩된 열에 대해 NULL 값을 포함 하는 서버에 행을 대량 복사 하려면 인스턴스의 *Iindicator* 멤버 값을 SQL_NULL_DATA으로 설정 해야 합니다.  
  
 *cbData*  
 프로그램 변수 데이터에서 길이 또는 Null 표시자나 종결자의 길이를 제외한 바이트 수입니다.  
  
 *Cbdata* 를 SQL_NULL_DATA로 설정 하면 서버에 복사 된 모든 행에는 열에 대 한 NULL 값이 포함 되어 있음을 나타냅니다.  
  
 *Cbdata* 를 SQL_VARLEN_DATA로 설정 하면 시스템에서 문자열 종결자 또는 다른 메서드를 사용 하 여 복사 되는 데이터의 길이를 결정 하는 것을 나타냅니다.  
  
 정수와 같은 고정 길이 데이터 형식의 경우 시스템은 데이터 형식으로 데이터의 길이를 확인합니다. 따라서 고정 길이 데이터 형식의 경우 *Cbdata* 를 안전 하 게 SQL_VARLEN_DATA 하거나 데이터 길이에 안전 하 게 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]문자 및 이진 데이터 형식의 경우 *cbdata* 는 SQL_VARLEN_DATA, SQL_NULL_DATA, 양수 값 또는 0 일 수 있습니다. *Cbdata* 가 SQL_VARLEN_DATA 되 면 시스템에서는 길이/null 표시기 (있는 경우) 또는 종결자 시퀀스를 사용 하 여 데이터 길이를 확인 합니다. 두 가지가 모두 제공되면 시스템은 복사할 데이터가 적은 항목을 사용합니다. *Cbdata* 가 SQL_VARLEN_DATA 경우 열의 데이터 형식이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 또는 이진 형식이 며 길이 표시기와 종결자 시퀀스를 모두 지정 하지 않으면 시스템에서 오류 메시지를 반환 합니다.  
  
 *Cbdata* 가 0 이거나 양수 값 이면 시스템은 *cbdata* 를 데이터 길이로 사용 합니다. 그러나 *cbdata* 값이 양수이 고 길이 표시자 또는 종결자 시퀀스가 제공 된 경우 시스템은 복사 되는 데이터의 양이 가장 적은 메서드를 사용 하 여 데이터 길이를 결정 합니다.  
  
 *Cbdata* 매개 변수 값은 데이터의 바이트 수를 나타냅니다. 문자 데이터가 유니코드 와이드 문자로 표현 되는 경우 양의 *Cbdata* 매개 변수 값은 문자 수와 각 문자의 바이트 크기를 곱한 값을 나타냅니다.  
  
 *pTerm*  
 바이트 패턴에 대한 포인터이며 있는 경우 이 프로그램 변수의 끝을 표시합니다. 예를 들어 ANSI 및 MBCS C 문자열은 일반적으로 1바이트 종결자(\0)를 가집니다.  
  
 변수에 종결자가 없는 경우 *Pterm* 을 NULL로 설정 합니다.  
  
 C Null 종결자를 프로그램 변수 종결자로 지정하기 위해 빈 문자열("")을 사용할 수 있습니다. Null로 끝나는 빈 문자열은 단일 바이트 (종결자 바이트 자체)를 구성 하므로 *Cbterm* 을 1로 설정 합니다. 예를 들어 *szName* 의 문자열이 null로 종료 되 고 해당 종결자를 사용 하 여 길이를 나타내야 함을 나타낼 수 있습니다.  
  
```
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```

 이 예제의 종료 되지 않은 형식은 15 자를 *szName* 변수에서 바인딩된 테이블의 두 번째 열로 복사 했음을 나타낼 수 있습니다.  

```
bcp_bind(hdbc, szName, 0, 15,
   NULL, 0, SQLCHARACTER, 2)  
```

 대량 복사 API는 필요한 경우 유니코드에서 MBCS로의 문자 변환을 수행합니다. 종결자 바이트 문자열 및 바이트 문자열 길이를 모두 올바르게 설정해야 합니다. 예를 들어 *szName* 의 문자열이 유니코드 null 종결자 값으로 종료 된 유니코드 와이드 문자열 임을 나타내려면 다음을 수행 합니다.  
  
```  
bcp_bind(hdbc, szName, 0,
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 바인딩된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열이 와이드 문자 이면 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)에서 변환이 수행 되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열이 MBCS 문자 형식이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터를 보내는 동안 와이드 문자가 멀티바이트 문자로 변환됩니다.  
  
 *cbTerm*  
 프로그램 변수에 종결자가 있는 경우 바이트 수입니다. 변수에 종결자가 없는 경우 *Cbterm* 을 0으로 설정 합니다.  

*Edatatype* 프로그램 변수의 C 데이터 형식입니다. 프로그램 변수의 데이터는 데이터베이스 열의 형식으로 변환됩니다. 이 매개 변수가 0이면 변환이 수행되지 않습니다.  

*Edatatype* 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC C 데이터 형식 열거자가 아닌 sqlncli의 데이터 형식 토큰에 의해 열거 됩니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 특정 형식 SQLINT2를 사용하여 2바이트 정수인 ODBC 형식 SQL_C_SHORT를 지정할 수 있습니다.  

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 **_Edatatype_** 매개 변수의 SQLXML 및 sqludt 데이터 형식 토큰에 대 한 지원이 도입 되었습니다.  

다음 표에는 유효한 열거형 데이터 형식 및 해당 ODBC C 데이터 형식이 나열되어 있습니다.

|eDataType|C 형식|
|-----------------------|------------|  
|SQLTEXT|char *|  
|SQLNTEXT|wchar_t *|  
|SQLCHARACTER|char *|  
|SQLBIGCHAR|char *|  
|SQLVARCHAR|char *|  
|SQLBIGVARCHAR|char *|  
|SQLNCHAR|wchar_t *|  
|SQLNVARCHAR|wchar_t *|  
|SQLBINARY|unsigned char *|  
|SQLBIGBINARY|unsigned char *|  
|SQLVARBINARY|unsigned char *|  
|SQLBIGVARBINARY|unsigned char *|  
|SQLBIT|char|  
|SQLBITN|char|  
|SQLINT1|char|  
|SQLINT2|short int|  
|SQLINT4|int|  
|SQLINT8|_int64|  
|SQLINTN|*cbIndicator*<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|  
|SQLFLT4|float|  
|SQLFLT8|float|  
|SQLFLTN|*cbIndicator*<br /> 4: SQLFLT4<br /> 8: SQLFLT8|  
|SQLDECIMALN|SQL_NUMERIC_STRUCT|  
|SQLNUMERICN|SQL_NUMERIC_STRUCT|  
|SQLMONEY|DBMONEY|  
|SQLMONEY4|DBMONEY4|  
|SQLMONEYN|*cbIndicator*<br /> 4: SQLMONEY4<br /> 8: SQLMONEY|  
|SQLTIMEN|SQL_SS_TIME2_STRUCT|  
|SQLDATEN|SQL_DATE_STRUCT|  
|SQLDATETIM4|DBDATETIM4|  
|SQLDATETIME|DBDATETIME|  
|SQLDATETIMN|*cbIndicator*<br /> 4: SQLDATETIM4<br /> 8: SQLDATETIME|  
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|  
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|  
|SQLIMAGE|unsigned char *|  
|SQLUDT|unsigned char *|  
|SQLUNIQUEID|SQLGUID|  
|SQLVARIANT|*다음을 제외한 모든 데이터 형식:*<br />-   text<br />-   ntext<br />-   image<br />-   varchar(max)<br />-   varbinary(max)<br />-   nvarchar(max)<br />-   xml<br />-   timestamp|  
|SQLXML|*지원되는 C 데이터 형식:*<br />-   char*<br />-   wchar_t *<br />-   unsigned char *|  

*Idxservercol* 데이터가 복사 되는 데이터베이스 테이블에서 열의 서 수 위치입니다. 테이블의 첫 번째 열은 열 1입니다. 열의 서수 위치는 [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)를 사용하여 확인할 수 있습니다.  
  
## <a name="returns"></a>반환

 SUCCEED 또는 FAIL

## <a name="remarks"></a>설명

**Bcp_bind** 를 사용 하 여 프로그램 변수에서의 테이블로 데이터를 빠르고 효율적으로 복사할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있습니다.  

이 또는 다른 대량 복사 함수를 호출 하기 전에 [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 를 호출 합니다. **Bcp_init** 를 호출 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 테이블이 대량 복사로 설정 됩니다. **Bcp_bind** 및 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)와 함께 사용 하기 위해 **bcp_init** 를 호출 하는 경우 데이터 파일을 나타내는 **bcp_init** _szdatafile_ 파일 매개 변수가 NULL로 설정 됩니다. **bcp_init**_edirection_ 매개 변수는 DB_IN로 설정 됩니다.  

복사할 테이블의 모든 열에 대해 별도의 **bcp_bind** 호출을 수행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 필요한 **bcp_bind** 호출이 완료 되 면 **bcp_sendrow** 를 호출 하 여 프로그램 변수의 데이터 행을로 보냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 열을 다시 바인딩하는 것은 지원되지 않습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이미 받은 행을 커밋할 때마다 [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)를 호출 합니다. 예를 들어 1000 행이 삽입 될 때마다 또는 다른 간격으로 **bcp_batch** 를 한 번씩 호출 합니다.  

삽입할 행이 더 이상 없는 경우 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)를 호출 합니다. 그렇게 하지 않으면 오류가 반환됩니다.

[Bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)로 지정 된 컨트롤 매개 변수 설정은 **bcp_bind** 행 전송에 영향을 주지 않습니다.  

열에 대 한 *.pdata* 가 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)에 대 한 호출에서 제공 되기 때문에 열에 대해 .pdata가 null로 설정 된 경우 *edatatype* 이 SQLTEXT, SQLTEXT, SQLXML, SQLTEXT, SQLTEXT, SQLTEXT, SQLTEXT, SQLBINARY, sqltext 또는 SQLIMAGE로 설정 된 이후의 모든 열은 null로 설정 된 *.pdata* 와 바인딩되어야 하 고 **bcp_moretext**에 대 한 호출을 통해 해당 값  

**Varchar (max)**, **varbinary (max)** 또는 **nvarchar (max)** 와 같은 새 대량 값 형식의 경우 *EDATATYPE* 매개 변수에서 SQLCHARACTER, SQLCHARACTER, sqlcharacter, SQLBINARY 및 sqlcharacter를 형식 표시기로 사용할 수 있습니다.  

*Cbterm* 이 0이 아니면 접두사 (*cbterm*)에 대 한 값 (1, 2, 4 또는 8)이 유효 합니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 종결자를 검색 하 고, 종결자 (*i*)와 관련 된 데이터 길이를 계산 하 고, *cbdata* 를 i의 작은 값과 접두사 값으로 설정 합니다.  

*Cbterm* 이 0이 고 *cbterm* (접두사)가 0이 아니면 *cbterm* 8 이어야 합니다. 8 바이트 접두사는 다음 값을 사용할 수 있습니다.  

- 0xFFFFFFFFFFFFFFFF는 필드의 Null 값을 의미합니다.  

- 0xFFFFFFFFFFFFFFFE은 서버에 데이터를 청크로 효율적으로 전송 하는 데 사용 되는 특수 접두사 값으로 처리 됩니다. 이 특수한 접두사를 사용한 데이터의 형식은 다음과 같습니다.  

- <SPECIAL_PREFIX> \<0 or more  DATA CHUNKS> <ZERO_CHUNK> 위치:  

- SPECIAL_PREFIX는 0xFFFFFFFFFFFFFFFE입니다.  

- DATA_CHUNK는 청크 길이를 포함 하는 4 바이트 접두사이 고 그 뒤에 4 바이트 접두사에 길이가 지정 된 실제 데이터가 있습니다.  

- ZERO_CHUNK은 데이터의 끝을 나타내는 모든 0 (00000000)을 포함 하는 4 바이트 값입니다.  

- 다른 모든 유효한 8 바이트 길이는 일반 데이터 길이로 처리 됩니다.  

 **Bcp_bind** 를 사용할 때 [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) 를 호출 하면 오류가 발생 합니다.  
  
## <a name="bcp_bind-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능을 위한 bcp_bind 지원

날짜/시간 형식에 대 한 *Edatatype* 매개 변수와 함께 사용 되는 형식에 대 한 자세한 내용은 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 내용 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)를 참조 하세요.  

자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  

## <a name="example"></a>예제
  
```
#include sql.h  
#include sqlext.h  
#include odbcss.h  
// Variables like henv not specified.  
HDBC      hdbc;  
char         szCompanyName[MAXNAME];  
DBINT      idCompany;  
DBINT      nRowsProcessed;  
DBBOOL      bMoreData;  
char*      pTerm = "\t\t";  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source; return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bcp.
if (bcp_init(hdbc, "comdb..accounts_info", NULL, NULL  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.
if (bcp_bind(hdbc, (LPCBYTE) &idCompany, 0, sizeof(DBINT), NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_bind(hdbc, (LPCBYTE) szCompanyName, 0, SQL_VARLEN_DATA,  
   (LPCBYTE) pTerm, strnlen(pTerm, sizeof(pTerm)), SQLCHARACTER, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
while (TRUE)  
   {  
   // Retrieve and process program data.
   if ((bMoreData = getdata(&idCompany, szCompanyName)) == TRUE)  
      {  
      // Send the data.
      if (bcp_sendrow(hdbc) == FAIL)  
         {  
         // Raise error and return.  
         return;  
         }  
      }  
   else  
      {  
      // Break out of loop.  
      break;  
      }  
   }  
  
// Terminate the bulk copy operation.  
if ((nRowsProcessed = bcp_done(hdbc)) == -1)  
   {  
   printf_s("Bulk-copy unsuccessful.\n");  
   return;  
   }  
  
printf_s("%ld rows copied.\n", nRowsProcessed);  
```  
  
## <a name="see-also"></a>참고 항목

 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)
