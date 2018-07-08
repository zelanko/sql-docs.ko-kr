---
title: bcp_bind | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_bind
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
caps.latest.revision: 47
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d956dcbd51d9f62a79012071dd1b1935131edf8f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430262"
---
# <a name="bcpbind"></a>bcp_bind
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
 복사 대상 데이터에 대한 포인터입니다. 하는 경우 *eDataType* SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR 또는 sqlimage 인 경우에 *pData* NULL 일 수 있습니다. NULL *pData* 긴 데이터 값을 보냄을 나타냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 청크로 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)합니다. 사용자만 설정 해야 *pData* 그렇지 않은 경우에 해당 하는 사용자가 바인딩한 필드 열이 BLOB 열인 경우 NULL로 **bcp_bind** 실패 합니다.  
  
 데이터에 표시자가 있으면 이는 메모리에서 데이터 바로 앞에 표시됩니다. 합니다 *pData* 매개 변수가이 경우 표시기의 너비에 표시자 변수를 가리키는 합니다 *cbIndicator* 매개 변수를 올바르게 주소 사용자 데이터를 대량 복사에서 사용 됩니다.  
  
 *cbIndicator*  
 열 데이터의 길이 또는 Null 표시자의 바이트 단위 길이입니다. 올바른 표시기 길이 값은 0(표시기를 사용하지 않을 경우), 1, 2, 4 또는 8입니다. 표시자는 메모리에서 데이터 바로 앞에 표시됩니다. 예를 들어 대량 복사를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 정수 값을 삽입하기 위해 다음 구조 형식 정의를 사용할 수 있습니다.  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 예제에서는 합니다 *pData* 매개 변수는 선언 된 즉 BCPBOUNDINT 주소의 구조 인스턴스의 주소를 설정할 수는 *iIndicator* 구조체 멤버입니다. 합니다 *cbIndicator* 정수 크기로 매개 변수를 설정할 수는 (sizeof (int), 및 *cbData* 매개 변수는 정수 (sizeof (int) 크기 다시 설정 됩니다. 인스턴스의 값에 바인딩된 열에 값 NULL을 포함 하는 서버에 행을 대량 복사할 *iIndicator* 멤버를 sql_null_data로 설정 되어야 합니다.  
  
 *cbData*  
 프로그램 변수 데이터에서 길이 또는 Null 표시자나 종결자의 길이를 제외한 바이트 수입니다.  
  
 설정 *cbData* 를 sql_null_data로 서버에 복사 하는 모든 행의 열에 NULL 값 포함을 의미 합니다.  
  
 설정 *cbData* 를 sql_varlen_data로 시스템에서 문자열 종결자를 사용 하거나 데이터의 길이 확인 하려면 다른 메서드를 복사를 나타냅니다.  
  
 정수와 같은 고정 길이 데이터 형식의 경우 시스템은 데이터 형식으로 데이터의 길이를 확인합니다. 따라서 고정 길이 데이터 형식용 *cbData* SQL_VARLEN_DATA 또는 데이터의 길이 안전 하 게 될 수 있습니다.  
  
 에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 및 이진 데이터 형식의 *cbData* SQL_VARLEN_DATA, SQL_NULL_DATA, 양수 일부 값 또는 0 일 수 있습니다. 하는 경우 *cbData* 가 SQL_VARLEN_DATA 이면 시스템은 데이터의 길이 확인 하는 길이 또는 null 표시기 (있는 경우) 또는 종결자 시퀀스를 사용 합니다. 두 가지가 모두 제공되면 시스템은 복사할 데이터가 적은 항목을 사용합니다. 하는 경우 *cbData* 가 SQL_VARLEN_DATA 이면 열의 데이터 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 또는 이진 형식이 며 길이 표시기 나 종결자 시퀀스 모두를 지정 하면 시스템 오류 메시지를 반환 합니다.  
  
 하는 경우 *cbData* 가 0 이거나 양수 값 이면 시스템은 *cbData* 를 데이터 길이로 합니다. 그러나 양수 이면 *cbData* 최소한의 데이터를 복사 하는 메서드를 사용 하 여 데이터 길이 확인 하는 시스템, 값, 길이 표시기 나 종결자 시퀀스를 제공 합니다.  
  
 합니다 *cbData* 매개 변수 값 데이터의 바이트 수를 나타냅니다. 문자 데이터가 유니코드 와이드 문자로 다음 양수 표현 되는 경우 *cbData* 매개 변수 값에서 각 문자의 바이트 크기를 곱한 문자의 수를 나타냅니다.  
  
 *pTerm*  
 바이트 패턴에 대한 포인터이며 있는 경우 이 프로그램 변수의 끝을 표시합니다. 예를 들어 ANSI 및 MBCS C 문자열은 일반적으로 1바이트 종결자(\0)를 가집니다.  
  
 종결자가 없는 변수를 설정 *pTerm* NULL로 합니다.  
  
 C Null 종결자를 프로그램 변수 종결자로 지정하기 위해 빈 문자열("")을 사용할 수 있습니다. Null로 끝나는 빈 문자열은 단일 바이트 (종결자 바이트 자체), 설정 *cbTerm* 1입니다. 예를 들어 나타내는 문자열 *szName* null로 종료 되는 길이를 나타내는 종결자를 사용 해야 함 및:  
  
```  
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```  
  
 이 예제의 종결된 폼에서 15 자 복사 되어야 함을 나타낼 수 있습니다 합니다 *szName* 바인딩된 테이블의 두 번째 열에 변수:  
  
```  
bcp_bind(hdbc, szName, 0, 15,   
   NULL, 0, SQLCHARACTER, 2)  
```  
  
 대량 복사 API는 필요한 경우 유니코드에서 MBCS로의 문자 변환을 수행합니다. 종결자 바이트 문자열 및 바이트 문자열 길이를 모두 올바르게 설정해야 합니다. 예를 들어 나타내는 문자열 *szName* 유니코드 와이드 문자열이 유니코드 null 종결자 값에 의해 종료 됩니다.  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 경우 바인딩된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열이 와이드 문자 하 변환이 수행 됩니다 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열이 MBCS 문자 형식이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터를 보내는 동안 와이드 문자가 멀티바이트 문자로 변환됩니다.  
  
 *cbTerm*  
 프로그램 변수에 종결자가 있는 경우 바이트 수입니다. 종결자가 없는 변수를 설정 *cbTerm* 0입니다.  
  
 *eDataType*  
 프로그램 변수의 C 데이터 형식입니다. 프로그램 변수의 데이터는 데이터베이스 열의 형식으로 변환됩니다. 이 매개 변수가 0이면 변환이 수행되지 않습니다.  
  
 *eDataType* 의해 열거 된 매개 변수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 토큰 sqlncli.h에는 ODBC C 데이터 형식 열거자가 아닌 합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 특정 형식 SQLINT2를 사용하여 2바이트 정수인 ODBC 형식 SQL_C_SHORT를 지정할 수 있습니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SQLXML 및 SQLUDT 데이터 형식 토큰에 대 한 지원을 도입 합니다 ***eDataType*** 매개 변수입니다.  
 
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
|SQLINT4|ssNoversion|  
|SQLINT8|_int64|  
|SQLINTN|*cbIndicator*<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|  
|SQLFLT4|FLOAT|  
|SQLFLT8|FLOAT|  
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
  
 *idxServerCol*  
 데이터 복사 대상인 데이터베이스 테이블 열의 서수 위치입니다. 테이블의 첫 번째 열은 열 1입니다. 열의 서 수 위치를 보고 [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)합니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 사용 하 여 **bcp_bind** 의 테이블에 프로그램 변수에서 데이터를 복사할 빠르고 효율적인 방법을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 호출 [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 이 또는 다른 대량 복사 함수를 호출 하기 전에 합니다. 호출 **bcp_init** 설정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 복사의 대상 테이블입니다. 호출할 때 **bcp_init** 사용에 대 한 **bcp_bind** 하 고 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)서 **bcp_init** *szDataFile*매개 변수를 데이터 파일을 나타내는 NULL로 설정 됩니다 **bcp_init * eDirection* 매개 변수가 DB_IN으로 설정 됩니다.  
  
 개별적 **bcp_bind** 의 모든 열에 대 한 호출을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복사 하려는 테이블입니다. 필요한 **bcp_bind** 호출을 수행한 다음 호출 **bcp_sendrow** 하 여 프로그램 변수의 데이터 행을 보낼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 열을 다시 바인딩하는 것은 지원되지 않습니다.  
  
 추가할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이미 수신한 행 커밋이 호출 [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)합니다. 예를 들어, 호출 **bcp_batch** 삽입 되는 모든 1000 행 또는 다른 간격으로 한 번입니다.  
  
 더 이상 행을 삽입할 때 호출할 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)합니다. 그렇게 하지 않으면 오류가 반환됩니다.  
  
 에 지정 된 매개 변수 설정을 제어할 [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md), 미치지 **bcp_bind** 행 전송 합니다.  
  
 하는 경우 *pData* 를 호출 하 여 해당 값을 제공 하기 때문에 열을 NULL로 설정 됩니다 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)를 사용 하 여 모든 후속 열 *eDataType* SQLTEXT, SQLNTEXT로 설정 SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR 또는 SQLIMAGE도 바인딩되어야 *pData* NULL로 설정 하 고 호출 하 여 해당 값도 제공 해야 **bcp_moretext**.  
  
 새로운 큰 값 형식의 경우와 같은 **varchar (max)** 를 **varbinary (max)**, 또는 **nvarchar (max)**, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, 사용할 수 있습니다 및 형식으로 SQLNCHAR 합니다 *eDataType* 매개 변수입니다.  
  
 하는 경우 *cbTerm* 는 0이 아닌 모든 값 (1, 2, 4 또는 8)이 접두사에 대 한 유효 (*cbIndicator*). 이런 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 종결자에 대 한 검색, 종결자와 관련 하 여 데이터 길이 계산 (*있습니까*), 설정 및 합니다 *cbData* i의 값을 더 작은 값 접두사입니다.  
  
 하는 경우 *cbTerm* 은 0 및 *cbIndicator* 아닙니다 (접두사) 0 *cbIndicator* 8 이어야 합니다. 8바이트 접두사는 다음과 같은 값을 가질 수 있습니다.  
  
-   0xFFFFFFFFFFFFFFFF는 필드의 Null 값을 의미합니다.  
  
-   0xFFFFFFFFFFFFFFFE는 청크의 데이터를 효과적으로 서버에 보내는 데 사용할 수 있는 특수한 접두사 값입니다. 이 특수한 접두사를 사용한 데이터의 형식은 다음과 같습니다.  
  
-   < SPECIAL_PREFIX > \<0 또는 데이터 청크를 더 >< ZERO_CHUNK > 여기서:  
  
-   SPECIAL_PREFIX는 0xFFFFFFFFFFFFFFFE입니다.  
  
-   DATA_CHUNK는 청크의 길이를 포함하는 4바이트 접두사이며, 이 뒤에는 4바이트 접두사에 길이가 지정된 실제 데이터가 옵니다.  
  
-   ZERO_CHUNK는 데이터의 끝을 나타내는 모든 0(00000000)을 포함하는 4바이트 값입니다.  
  
-   다른 모든 유효한 8바이트 길이는 일반적인 데이터 길이로 처리됩니다.  
  
 호출 [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) 사용 하는 경우 **bcp_bind** 오류가 발생 합니다.  
  
## <a name="bcpbind-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능을 위한 bcp_bind 지원  
 사용 유형에 대 한 정보에 대 한 합니다 *eDataType* 날짜/시간 형식에 대 한 매개 변수 참조 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 자세한 내용은 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
