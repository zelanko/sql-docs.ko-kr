---
title: bcp_readfmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_readfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_readfmt function
ms.assetid: 654001c8-ae9f-425c-b820-f0191bf89367
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76ccc4271877b81ae103a89b5df727b74017d9ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62688666"
---
# <a name="bcpreadfmt"></a>bcp_readfmt
  지정한 형식 파일에서 데이터 파일 형식 정의를 읽어 옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_readfmt (  
HDBC   
hdbc  
,  
LPCTSTR   
szFormatFile  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *szFormatFile*  
 데이터 파일에 대한 서식 값이 포함된 파일의 경로 및 파일 이름입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 이후에 `bcp_readfmt` 형식 값을 읽고을 적절 하 게 호출 [bcp_columns](bcp-columns.md) 하 고 [bcp_colfmt](bcp-colfmt.md)합니다. 형식 파일의 구문을 분석하여 이러한 호출을 수행할 필요가 없습니다.  
  
 형식 파일을 저장하려면 [bcp_writefmt](bcp-writefmt.md)를 호출합니다. 에 대 한 호출 `bcp_readfmt` 저장 된 서식을 참조할 수 있습니다. 자세한 내용은 [bcp_init](bcp-init.md)를 참조하십시오.  
  
 또는 대량 복사 유틸리티 (**bcp**)에서 참조할 수 있는 파일에서 사용자 정의 데이터 형식을 저장할 수 `bcp_readfmt`입니다. 에 대 한 자세한 내용은 **bcp** 의 구조 및 유틸리티 **bcp** 데이터 서식 파일을 참조 하십시오. [대량 데이터 가져오기 및 내보내기의 &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 `BCPDELAYREADFMT` 의 값을 *eOption* 의 매개 변수 [bcp_control](bcp-control.md) bcp_readfmt의 동작을 수정 합니다.  
  
> [!NOTE]  
>  형식 파일은 **bcp** 유틸리티 4.2 이상 버전에서 생성된 파일이어야 합니다.  
  
## <a name="example"></a>예제  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
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
if (bcp_init(hdbc, _T("myTable"), _T("myData.csv"),  
   _T("myErrors"),    DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_readfmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   cout << nRowsProcessed << " rows copied to SQL Server\n";  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
