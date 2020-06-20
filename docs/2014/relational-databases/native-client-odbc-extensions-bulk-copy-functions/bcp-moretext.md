---
title: bcp_moretext | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_moretext
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
author: rothja
ms.author: jroth
ms.openlocfilehash: ec121d057183bb1076a5c540976bd234bc46fecb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019546"
---
# <a name="bcp_moretext"></a>bcp_moretext
  긴 가변 길이 데이터 형식 값의 일부를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 보냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_moretext (  
HDBC   
hdbc  
,  
DBINT   
cbData  
,  
LPCBYTE   
pData  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *cbData*  
 *.Pdata*에서 참조 하는 데이터 SQL Server에 복사 되는 데이터의 바이트 수입니다. SQL_NULL_DATA 값은 NULL을 나타냅니다.  
  
 *pData*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 보낼 지원되는 긴 가변 길이 데이터 청크에 대한 포인터입니다.  
  
## <a name="returns"></a>반환  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>설명  
 이 함수는 [bcp_bind](bcp-bind.md) 및 [bcp_sendrow](bcp-sendrow.md) 와 함께 사용 하 여 긴 가변 길이 데이터 값을 여러 개의 작은 청크로 SQL Server 복사할 수 있습니다. **bcp_moretext** 는 `text` , `ntext` ,,,, `image` `varchar(max)` `nvarchar(max)` `varbinary(max)` , UDT (사용자 정의 형식) 및 XML과 같은 SQL Server 데이터 형식이 있는 열과 함께 사용할 수 있습니다. **bcp_moretext** 데이터 변환을 지원 하지 않으므로 제공 된 데이터가 대상 열의 데이터 형식과 일치 해야 합니다.  
  
 **Bcp_moretext**에서 지원 되는 데이터 형식에 대해 Null이 아닌 *.pdata* 매개 변수를 사용 하 여 **bcp_bind** 를 호출 하는 경우는 `bcp_sendrow` 길이에 관계 없이 전체 데이터 값을 보냅니다. 그러나 **bcp_bind** 지원 되는 데이터 형식에 대 한 NULL *.pdata* 매개 변수를 포함 하는 경우 데이터가 있는 **bcp_moretext** `bcp_sendrow` 바인딩된 모든 열이 처리 되었음을 나타내는에서 성공적으로 반환 된 후 즉시 데이터를 복사 하는 데 bcp_moretext 사용할 수 있습니다.  
  
 **Bcp_moretext** 를 사용 하 여 지원 되는 데이터 형식 열을 하나의 행에 보내려면이 열을 사용 하 여 행에서 지원 되는 다른 데이터 형식 열을 모두 전송 해야 합니다. 열을 건너뛸 수 없습니다. 지원되는 데이터 형식은 SQLTEXT, SQLNTEXT, SQLIMAGE, SQLUDT 및 SQLXML입니다. 열이 각각 varchar(max), nvarchar(max) 또는 varbinary(max)인 경우 SQLCHARACTER, SQLVARCHAR, SQNCHAR, SQLBINARY 및 SQLVARBINARY도 이 범주에 해당합니다.  
  
 **Bcp_bind** 또는 [bcp_collen](bcp-collen.md) 를 호출 하면 SQL Server 열에 복사 되는 모든 데이터 부분의 총 길이가 설정 됩니다. **Bcp_bind** 에 대 한 호출에 지정 된 것 보다 더 많은 바이트 SQL Server 보내려는 시도는 `bcp_collen` 오류를 생성 합니다. 예를 들어이 오류는 `bcp_collen` SQL Server 열에 사용 가능한 데이터의 길이를 4500로 설정 하는 데 사용 되는 응용 프로그램에서 `text` 데이터 버퍼 길이가 1000 바이트 였는 각 호출을 나타내는 동안 **bcp_moretext** 를 5 번 호출 하는 경우에 발생 합니다.  
  
 복사 된 행에 두 개 이상의 long 가변 길이 열이 포함 된 경우 **bcp_moretext** 는 먼저 가장 낮은 서 수로 번호 열에 데이터를 보내고 그 다음에 가장 낮은 서 수로 번호 열을 입력 합니다. 필요한 데이터의 총 길이를 올바르게 설정하는 것이 중요합니다. 길이 설정 외에는 대량 복사에서 열의 모든 데이터가 수신되었음을 나타낼 방법이 없습니다.  
  
 `var(max)`Bcp_sendrow 및 bcp_moretext를 사용 하 여 값을 서버로 보내는 경우에는 bcp_collen를 호출 하 여 열 길이를 설정할 필요가 없습니다. 대신 이러한 형식에 대해서만 값이 0 인 bcp_sendrow를 호출 하 여 종료 됩니다.  
  
 응용 프로그램은 일반적으로 `bcp_sendrow` 루프 내에서를 호출 하 고 **bcp_moretext** 하 여 많은 데이터 행을 보냅니다. 다음은 두 개의 열이 포함 된 테이블에 대해이 작업을 수행 하는 방법에 대 한 개요입니다 `text` .  
  
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
 이 예제에서는 **bcp_bind** 와 함께 **bcp_moretext** 를 사용 하는 방법을 보여 줍니다 `bcp_sendrow` .  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
