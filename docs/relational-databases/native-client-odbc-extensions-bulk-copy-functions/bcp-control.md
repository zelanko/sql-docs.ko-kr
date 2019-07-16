---
title: bcp_control | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_control
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_control function
ms.assetid: 32187282-1385-4c52-9134-09f061eb44f5
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0909a94ea49f2a4deee20cd29b26b0e1e2aaf6e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895680"
---
# <a name="bcpcontrol"></a>bcp_control
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  파일과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간의 대량 복사에 대한 다양한 제어 매개 변수의 기본 설정을 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_control (  
        HDBC hdbc,  
        INT eOption,  
        void* iValue);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *eOption*  
 다음 중 하나일 수 있습니다.  
  
 BCPABORT  
 이미 진행 중인 대량 복사 작업을 중지합니다. 호출 **bcp_control** 사용 하 여는 *eOption* 실행을 중지 하려면 다른 스레드에서 BCPABORT의 대량 복사 작업입니다. 합니다 *iValue* 매개 변수가 무시 됩니다.  
  
 BCPBATCH  
 일괄 처리당 행 수입니다. 기본값은 0으로, 데이터를 추출할 때 테이블에 있는 모든 행 수를 나타내거나 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 복사할 때 사용자 데이터 파일에 있는 모든 행 수를 나타냅니다. 1보다 작은 값을 지정하면 BCPBATCH가 기본값으로 다시 설정됩니다.  
  
 BCPDELAYREADFMT  
 경우에는 부울을 true로 설정 하면 [bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) 실행 시 읽습니다. False (기본값) 이면 bcp_readfmt 즉시는 경우 서식 파일을 읽습니다. BCPDELAYREADFMT가 true이 고 bcp_columns 또는 bcp_setcolfmt를 호출 하는 경우 시퀀스 오류가 발생 합니다.  
  
 호출 하는 경우에 시퀀스 오류가 발생 `bcp_control(hdbc,` BCPDELAYREADFMT`, (void *)FALSE)` 호출한 후 `bcp_control(hdbc,` BCPDELAYREADFMT`, (void *)TRUE)` 및 bcp_writefmt 합니다.  
  
 자세한 내용은 [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)을 참조하세요.  
  
 BCPFILECP  
 *iValue* 데이터 파일에 대 한 코드 페이지 번호를 포함 합니다. 1252나 850과 같은 코드 페이지 번호를 지정하거나 다음 값 중 하나를 지정할 수 있습니다.  
  
 BCPFILE_ACP: 파일의 데이터가 클라이언트의 Microsoft Windows  코드 페이지에 있습니다.  
  
 BCPFILE_OEMCP: 파일의 데이터가 클라이언트의 OEM 코드 페이지에 있습니다(기본값).  
  
 BCPFILE_RAW: 파일의 데이터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 코드 페이지에 있습니다.  
  
 BCPFILEFMT  
 데이터 파일 형식의 버전 번호입니다. 80 일 수 있습니다 ( [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]), 90 ( [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]), 100 ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 하거나 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]), 110 ( [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), 또는 120 ( [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). 120 기본값입니다. 이 옵션은 이전 버전 서버에서 지원하는 형식으로 데이터를 가져오고 내보내는 데 유용합니다. 예를 들어 텍스트 열에서 가져온 데이터를 가져오기에는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서버를를 **varchar (max)** 열에는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 서버의 80을 지정 해야 합니다. 마찬가지로,에서 데이터를 내보낼 때 80을 지정 하는 경우는 **varchar (max)** 열에 저장 되는 것 같이 텍스트 열에 저장 되어 합니다 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서식을 지정 하 고 텍스트 열으로 가져올 수 있습니다를 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서버.  
  
 BCPFIRST  
 복사할 파일이나 테이블의 첫 번째 데이터 행입니다. 기본값은 1입니다. 1보다 작은 값을 지정하면 이 옵션은 기본값으로 다시 설정됩니다.  
  
 BCPFIRSTEX  
 BCP out 작업의 경우 데이터 파일에 복사할 데이터베이스 테이블의 첫 번째 행을 지정합니다.  
  
 BCP in 작업의 경우 데이터베이스 테이블에 복사할 데이터 파일의 첫 번째 행을 지정합니다.  
  
 합니다 *iValue* 값이 포함 된 부호 있는 64 비트 정수 주소 여야 매개 변수가 필요 합니다. BCPFIRSTEX에 전달할 수 있는 최대값은 2^63-1입니다.  
  
 BCPFMTXML  
 생성되는 서식 파일이 XML 형식이 되도록 지정합니다. 기본적으로 해제되어 있습니다.  
  
 XML 서식 파일은 더 높은 유연성을 제공하지만 몇 가지 제약 조건이 있습니다. 예를 들어 이전 서식 파일에서는 가능했던 작업인 필드의 접두사와 종결자를 동시에 지정할 수 없습니다.  
  
> [!NOTE]  
>  XML 서식 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client와 함께 설치된 경우에만 지원됩니다.  
  
 BCPHINTS  
 *iValue* 는 SQLTCHAR 문자열 포인터가 포함 되어 있습니다. 주소가 지정된 문자열에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 복사 처리 힌트나 결과 집합을 반환하는 Transact-SQL 문을 지정합니다. Transact-SQL 문이 둘 이상의 결과 집합을 반환하도록 지정된 경우 첫 번째 결과 집합 다음에 오는 결과 집합은 모두 무시됩니다. 대량 복사 처리 힌트에 대 한 자세한 내용은 참조 하세요. [bcp 유틸리티](../../tools/bcp-utility.md)합니다.  
  
 BCPKEEPIDENTITY  
 때 *iValue* 가 TRUE 이면 대량 복사 함수에 대 한 제공 된 데이터 값을 삽입 하도록 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identity 제약 조건을 사용 하 여 정의 된 열입니다. 입력 파일은 ID 열에 해당하는 값을 제공해야 합니다. 설정되지 않은 경우 삽입된 행에 대해 새 ID 값이 생성됩니다. 파일에서 ID 열에 대한 데이터는 모두 무시됩니다.  
  
 BCPKEEPNULLS  
 파일의 빈 데이터 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 NULL 값으로 변환할지 여부를 지정합니다. 때 *iValue* 가 TRUE 이면 빈 값에서 NULL로 변환 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 기본적으로 빈 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 열의 기본값(있는 경우)으로 변환됩니다.  
  
 BCPLAST  
 복사할 마지막 행입니다. 기본값은 모든 행 복사입니다. 1보다 작은 값을 지정하면 이 옵션은 기본값으로 다시 설정됩니다.  
  
 BCPLASTEX  
 BCP out 작업의 경우 데이터 파일에 복사할 데이터베이스 테이블의 마지막 행을 지정합니다.  
  
 BCP in 작업의 경우 데이터베이스 테이블에 복사할 데이터 파일의 마지막 행을 지정합니다.  
  
 합니다 *iValue* 값이 포함 된 부호 있는 64 비트 정수 주소 여야 매개 변수가 필요 합니다. BCPLASTEX에 전달할 수 있는 최대값은 2^63-1입니다.  
  
 BCPMAXERRS  
 대량 복사 작업이 실패하기 전에 허용되는 오류 수입니다. 기본값은 10입니다. 1 보다 작은 값이이 옵션을 기본값으로 다시 설정 합니다. 대량 복사에는 최대 65,535개의 오류가 허용됩니다. 이 옵션을 65,535보다 큰 값으로 설정하려고 하는 경우 이 옵션은 65,535로 설정됩니다.  
  
 BCPODBC  
 TRUE 인 경우 지정 **날짜/시간** 하 고 **smalldatetime** 문자 형식으로 저장 하는 값에 ODBC 타임 스탬프 이스케이프 시퀀스 접두사 및 접미사 사용 합니다. BCPODBC 옵션 DB_OUT에만 적용 됩니다.  
  
 FALSE 인 경우는 **날짜/시간** 1997 년 1 월 1 일을 나타내는 값을 문자열로 변환 됩니다. 1997-01-01 00:00:00.000. TRUE 이면 동일한 **날짜/시간** 값으로 표현 됩니다. {ts ' 1997-01-01 00:00:00.000'}.  
  
 BCPROWCOUNT  
 현재(또는 마지막) BCP 작업에 의해 영향을 받는 행의 수를 반환합니다.  
  
 BCPTEXTFILE  
 TRUE이면 데이터 파일이 이진 파일 대신 텍스트 파일이 되도록 지정합니다. 파일이 텍스트 파일이면 BCP에서 데이터 파일의 처음 2바이트에서 유니코드 바이트 표식을 검사하여 텍스트 파일이 유니코드인지 여부를 확인합니다.  
  
 BCPUNICODEFILE  
 TRUE이면 입력 파일이 유니코드 파일이 되도록 지정합니다.  
  
 *iValue*  
 지정 된 값인 *eOption*합니다. *iValue* 는 64 비트 값으로 추가로 확장할 수 있도록 void 포인터로 캐스팅 되는 정수 (LONGLONG) 값입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>설명  
 이 함수는 대량 복사를 취소하기 전에 허용되는 오류 수, 데이터 파일에서 복사할 첫 번째 행과 마지막 행의 번호 및 일괄 처리 크기를 비롯하여 대량 복사 작업에 대한 여러 가지 제어 매개 변수를 설정합니다.  
  
 또한 이 함수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 SELECT의 결과 집합을 대량 복사할 때 SELECT 문을 지정하는 데 사용됩니다. 설정 *eOption* 을 설정 하 고 BCPHINTS *iValue* SELECT 문을 포함 하는 SQLTCHAR 문자열에 대 한 포인터입니다.  
  
 이러한 제어 매개 변수는 사용자 파일과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 간에 복사하는 경우에만 의미가 있습니다. 컨트롤 매개 변수 설정을 복사 하는 행에 영향을 주지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)합니다.  
  
## <a name="example"></a>예제  
  
```  
// Variables like henv not specified.  
SQLHDBC      hdbc;  
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
if (bcp_init(hdbc, _T("address"), _T("address.add"), _T("addr.err"),  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the number of rows per batch.   
if (bcp_control(hdbc, BCPBATCH, (void*) 1000) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set file column count.   
if (bcp_columns(hdbc, 1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the file format.   
if (bcp_colfmt(hdbc, 1, 0, 0, SQL_VARLEN_DATA, '\n', 1, 1)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
printf_s("%ld rows processed by bulk copy.", nRowsProcessed);  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
