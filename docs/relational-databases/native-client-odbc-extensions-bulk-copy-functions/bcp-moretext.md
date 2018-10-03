---
title: bcp_moretext | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_moretext
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 262280be894eb446d5a097f53f96306e4de410e8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665455"
---
# <a name="bcpmoretext"></a>bcp_moretext
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  긴 가변 길이 데이터 형식 값의 일부를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 보냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_moretext (  
        HDBC hdbc,  
        DBINT cbData,  
        LPCBYTE pData);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *cbData*  
 참조 하는 데이터에서 SQL Server로 복사 되는 데이터의 바이트 수가 *pData*합니다. SQL_NULL_DATA 값은 NULL을 나타냅니다.  
  
 *pData*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 보낼 지원되는 긴 가변 길이 데이터 청크에 대한 포인터입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 이 함수를 함께에서 사용할 수 있습니다 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 하 고 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) 값을 복사 긴 가변 길이 데이터를 보다 작은 많은 청크로 SQL server입니다. **bcp_moretext** 다음 SQL Server 데이터 형식의 열에 사용할 수 있습니다: **텍스트**를 **ntext**를 **이미지**, **varchar (max)** 하십시오 **nvarchar (max)**, **varbinary (max)**, 사용자 정의 형식 (UDT) 및 XML입니다. **bcp_moretext** 데이터 변환을 지원 하지 않습니다, 제공 된 데이터가 대상 열의 데이터 형식과 일치 해야 합니다.  
  
 하는 경우 **bcp_bind** 가 null이 아닌 호출 *pData* 에서 지원 되는 데이터 형식에 대 한 매개 변수 **bcp_moretext**를 **bcp_sendrow** 보냅니다 길이 관계 없이 전체 데이터 값입니다. 그러나 If, **bcp_bind** NULL이 포함 되어 *pData* 지원 되는 데이터 형식에 대 한 매개 변수 **bcp_moretext** 에서성공적인반환후에즉시데이터를복사할수**bcp_sendrow** 나타내는 데이터가 있는 바인딩된 모든 열이 처리 되었습니다.  
  
 사용 하는 경우 **bcp_moretext** 행에서 지원 되는 데이터 형식 열이 하나을 보낼 사용 해야 합니다도 행의 다른 모든 지원 되는 데이터 형식 열을 보내도록 합니다. 열을 건너뛸 수 없습니다. 지원되는 데이터 형식은 SQLTEXT, SQLNTEXT, SQLIMAGE, SQLUDT 및 SQLXML입니다. 열이 각각 varchar(max), nvarchar(max) 또는 varbinary(max)인 경우 SQLCHARACTER, SQLVARCHAR, SQNCHAR, SQLBINARY 및 SQLVARBINARY도 이 범주에 해당합니다.  
  
 호출 **bcp_bind** 하거나 [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) SQL Server 열에 복사할 모든 데이터 부분의 총 길이 설정 합니다. SQL Server에 대 한 호출에 지정 된 것 보다 많은 바이트를 전송 하려고 **bcp_bind** 하거나 **bcp_collen** 오류를 생성 합니다. 이 오류 발생, 예를 들어 하는 응용 프로그램에서 **bcp_collen** 는 SQL Server에 대 한 사용 가능한 데이터의 길이 설정 하려면 **텍스트** 4500으로 열 호출한 **bcp_moretext** 5 시간 동안 데이터 버퍼 길이 각 호출에서 1000 바이트입니다.  
  
 복사한 행에는 둘 이상의 긴 가변 길이 열을 포함 하는 경우 **bcp_moretext** 가장 낮은 데이터에 다음 열 서 수로 번호 첫 번째 보냅니다 가장 낮은 서 수로 번호가 매겨진된 열 및 등입니다. 필요한 데이터의 총 길이를 올바르게 설정하는 것이 중요합니다. 길이 설정 외에는 대량 복사에서 열의 모든 데이터가 수신되었음을 나타낼 방법이 없습니다.  
  
 때 **var(max)** 값 보내집니다 bcp_sendrow 및 bcp_moretext를 사용 하 여 서버에 필요 없는 열 길이 설정 하는 bcp_collen를 호출 합니다. 대신 이러한 형식에 대 한 값이 길이가 0 인 bcp_sendrow를 호출 하 여 종료 됩니다.  
  
 응용 프로그램이 정상적으로 호출 **bcp_sendrow** 하 고 **bcp_moretext** 데이터 행의 수를 보내도록 루프 내에서. 두 개를 포함 하는 테이블에 대 한이 작업을 수행 하는 방법의 개요는 다음과 같습니다 **텍스트** 열:  
  
```  
while (there are still rows to send)  
{  
bcp_sendrow(...);  
  
for (all the data in the first varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
for (all the data in the second varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
}  
  
```  
  
## <a name="example"></a>예제  
 이 예제에 사용 하는 방법을 보여 줍니다 **bcp_moretext** 사용 하 여 **bcp_bind** 하 고 **bcp_sendrow**:  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
DBINT      idRow = 5;  
char*      pPart1 = "This text value isn't very long,";  
char*      pPart2 = " but it's broken into three parts";  
char*      pPart3 = " anyhow.";  
DBINT      cbAllParts;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, "comdb..articles", NULL, NULL, DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idRow, 0, SQL_VARLEN_DATA, NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
cbAllParts = (DBINT) (strnlen(pPart1, sizeof(pPart1) + 1) + strnlen(pPart2, sizeof(pPart2) + 1) + strnlen(pPart3, sizeof(pPart3) + 1));  
if (bcp_bind(hdbc, NULL, 0, cbAllParts, NULL, 0, SQLTEXT, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Send this row, with the text value broken into three chunks.   
if (bcp_sendrow(hdbc) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart1, sizeof(pPart1) + 1), pPart1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart2, sizeof(pPart2) + 1), pPart2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart3, sizeof(pPart3) + 1), pPart3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// All done. Get the number of rows processed (should be one).  
nRowsProcessed = bcp_done(hdbc);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
