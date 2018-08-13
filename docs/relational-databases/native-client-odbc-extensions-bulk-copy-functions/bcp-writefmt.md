---
title: bcp_writefmt | Microsoft 문서
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
- bcp_writefmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_writefmt function
ms.assetid: cb4c1d37-667d-4bcd-b13c-eb638bcc9b69
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 5c5dda2f06df80d151ceece7e363643c3e824afe
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39562577"
---
# <a name="bcpwritefmt"></a>bcp_writefmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  현재 대량 복사 데이터 파일의 서식에 대한 설명이 포함된 서식 파일을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_writefmt (  
        HDBC hdbc,  
        LPCTSTR szFormatFile);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *szFormatFile*  
 데이터 파일의 형식 값을 받을 사용자 파일의 경로와 이름입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 서식 파일은 대량 복사를 통해 만들어진 데이터 파일의 데이터 형식을 지정합니다. 에 대 한 호출 [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) 하 고 [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) 데이터 파일의 형식을 정의 합니다. **bcp_writefmt** 이 정의에서 참조 하는 파일에 저장 *szFormatFile*합니다. 자세한 내용은 [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)합니다.  
  
 구조에 대 한 자세한 내용은 **bcp** 데이터 형식으로 파일을 참조 하십시오 [bcp 유틸리티를 사용 하 여 대량 데이터 내보내기 및 가져오기 &#40;SQL Server&#41;](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md).  
  
 저장된 된 서식 파일을 로드 하려면 사용 [bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)합니다.  
  
> [!NOTE]  
>  생성 된 서식 파일 **bcp_writefmt** 의 버전 에서만 지원 됩니다 합니다 **bcp** 유틸리티와 함께 배포 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 이상 버전.  
  
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
   _T("myErrors"),    DB_OUT) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_columns(hdbc, 3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
bcp_colfmt(hdbc, 1, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 1);  
bcp_colfmt(hdbc, 2, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 2);  
bcp_colfmt(hdbc, 3, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 3);  
  
if (bcp_writefmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   printf_s("%ld rows copied from SQL Server\n", nRowsProcessed);  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
