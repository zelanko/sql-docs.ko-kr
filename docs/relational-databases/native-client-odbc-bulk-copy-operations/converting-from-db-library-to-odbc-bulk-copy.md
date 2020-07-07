---
title: DB-LIBRARY에서 ODBC 대량 복사로 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- converting DB-Library to ODBC bulk copy
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], DB-Library bulk copy
- ODBC, bulk copy operations
- DB-Library bulk copy
ms.assetid: 0bc15bdb-f19f-4537-ac6c-f249f42cf07f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09726fbbbb1ba1ecd1516dc56ae084897aafff5c
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006607"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>DB-Library에서 ODBC 대량 복사로 변환
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Native Client ODBC 드라이버에서 지 원하는 대량 복사 함수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] db-library 대량 복사 함수와 비슷하며, 다음과 같은 경우를 제외 하 고 db-library 대량 복사 프로그램을 ODBC로 쉽게 변환할 수 있습니다.  
  
-   DB-Library 애플리케이션은 DBPROCESS 구조에 대한 포인터를 대량 복사 함수의 첫 번째 매개 변수로 전달합니다. ODBC 애플리케이션에서는 DBPROCESS 포인터가 ODBC 연결 핸들로 대체됩니다.  
  
-   DB-LIBRARY 응용 프로그램은 DBPROCESS에서 대량 복사 작업을 사용할 수 있도록 연결 하기 전에 **BCP_SETL** 호출 합니다. ODBC 응용 프로그램은 연결 하기 전에 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 를 호출 하 여 연결 핸들에서 대량 작업을 사용 하도록 설정 합니다.  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT odbc 드라이버는 db-library 메시지 및 오류 처리기를 지원 하지 않습니다. odbc 대량 복사 함수에 의해 발생 한 오류 및 메시지를 얻으려면 **SQLGetDiagRec** 를 호출 해야 합니다. ODBC 버전의 대량 복사 함수는 SQL_SUCCESS 또는 SQL_ERROR와 같은 ODBC 스타일 반환 코드가 아니라 표준 대량 복사 반환 코드인 SUCCEED 또는 FAILED를 반환합니다.  
  
-   DB-LIBRARY [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen* 매개 변수에 대해 지정 된 값은 ODBC **bcp_bind**_cbdata_ 매개 변수와 다르게 해석 됩니다.  
  
    |나타내는 조건|DB-LIBRARY *varlen* 값|ODBC *Cbdata* 값|  
    |-------------------------|--------------------------------|-------------------------|  
    |Null 값 제공|0|-1(SQL_NULL_DATA)|  
    |변수 데이터 제공|-1|-10(SQL_VARLEN_DATA)|  
    |길이가 0인 문자 또는 이진 문자열|해당 없음|0|  
  
     DB-LIBRARY에서 *varlen* 값-1은 가변 길이 데이터를 제공 하 고 있음을 나타냅니다 .이는 ODBC *CBDATA* 에서 NULL 값만 제공 됨을 의미 하는 것으로 해석 됩니다. -1의 DB-LIBRARY *varlen* 사양을 SQL_VARLEN_DATA로 변경 하 고 0의 *varlen* 사양을 SQL_NULL_DATA으로 변경 합니다.  
  
-   DB-LIBRARY **bcp_colfmt**_file_collen_ 와 ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*cbuserdata* 는 위에서 언급 한 **bcp_bind**_varlen_ 및 *cbdata* 매개 변수와 동일한 문제를 가집니다. -1의 DB-LIBRARY *file_collen* 사양을 SQL_VARLEN_DATA으로 변경 하 고 *file_collen* 지정을 0에서 SQL_NULL_DATA로 변경 합니다.  
  
-   ODBC [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 함수의 *ivalue* 매개 변수는 void 포인터입니다. DB-LIBRARY에서 *Ivalue* 는 정수입니다. ODBC *Ivalue* 의 값을 void *로 캐스팅 합니다.  
  
-   **Bcp_control** 옵션 BCPMAXERRS는 대량 복사 작업이 실패 하기 전까지 오류가 발생할 수 있는 개별 행의 수를 지정 합니다. BCPMAXERRS의 기본값은 ODBC 버전의 **bcp_control** 및 10의 db-library 버전에서 0 (첫 번째 오류가 발생 한 경우 실패)입니다. 대량 복사 작업을 종료 하기 위해 기본값 0에 의존 하는 DB-LIBRARY 응용 프로그램은 ODBC **bcp_control** 를 호출 하 여 BCPMAXERRS를 0으로 설정 해야 합니다.  
  
-   ODBC **bcp_control** 함수는 **bcp_control**의 db-library 버전에서 지원 되지 않는 다음 옵션을 지원 합니다.  
  
    -   BCPODBC  
  
         TRUE로 설정 하면 문자 형식으로 저장 된 **datetime** 및 **SMALLDATETIME** 값에 ODBC 타임 스탬프 이스케이프 시퀀스 접두사 및 접미사가 포함 되도록 지정 합니다. 이 옵션은 BCP_OUT 작업에만 적용됩니다.  
  
         BCPODBC.BCP를 FALSE로 설정 하면 문자열로 변환 된 **datetime** 값이 다음과 같이 출력 됩니다.  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         BCPODBC.BCP를 TRUE로 설정 하면 동일한 **datetime** 값이 다음과 같이 출력 됩니다.  
  
        ```  
        {ts '1997-01-01 00:00:00.000' }  
        ```  
  
    -   BCPKEEPIDENTITY  
  
         TRUE로 설정하면 대량 복사 함수에서 제공된 데이터 값을 ID 제약 조건이 있는 열에 삽입하도록 지정합니다. 설정되지 않은 경우 삽입된 행에 대해 새 ID 값이 생성됩니다.  
  
    -   BCPHINTS  
  
         다양한 대량 복사 최적화를 지정합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 이하 버전에서 사용할 수 없습니다.  
  
    -   BCPFILECP  
  
         대량 복사 파일의 코드 페이지를 지정합니다.  
  
    -   BCPUNICODEFILE  
  
         문자 모드 대량 복사 파일이 유니코드 파일이 되도록 지정합니다.  
  
-   Odbc **bcp_colfmt** 함수는 odbc SQLCHAR typedef와 충돌 하기 때문에 SQLCHAR의 *file_type* 표시기를 지원 하지 않습니다. **Bcp_colfmt**대신 sqlcharacter를 사용 합니다.  
  
-   ODBC 버전의 대량 복사 함수에서 문자열의 **datetime** 및 **smalldatetime** 값을 사용 하는 형식은 yyyy-mm-dd hh: mm: ss;의 odbc 형식입니다. **smalldatetime** 값은 yyyy-mm-dd hh: mm: SS의 ODBC 형식을 사용 합니다.  
  
     DB-LIBRARY 버전의 대량 복사 함수는 여러 형식을 사용 하 여 문자열에 **datetime** 및 **smalldatetime** 값을 허용 합니다.  
  
    -   기본 형식은 *mmm dd yyyy hh: mmxx* 여기서 *xx* 는 AM 또는 PM입니다.  
  
    -   DB-LIBRARY **dbconvert** 함수에서 지 원하는 모든 형식의 **datetime** 및 **smalldatetime** 문자열  
  
    -   클라이언트 네트워크 유틸리티의 DB-LIBRARY **옵션** 탭에서 **국가별 설정 사용** 확인란을 선택 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] db-library 대량 복사 함수도 클라이언트 컴퓨터 레지스트리의 로캘 설정에 대해 정의 된 국가별 날짜 형식으로 날짜를 적용 합니다.  
  
     DB-LIBRARY 대량 복사 함수는 ODBC **datetime** 및 **smalldatetime** 형식을 허용 하지 않습니다.  
  
     SQL_SOPT_SS_REGIONALIZE 문 특성을 SQL_RE_ON으로 설정하면 ODBC 대량 복사 함수에서는 클라이언트 컴퓨터 레지스트리의 로캘 설정에 정의된 국가별 날짜 형식의 날짜를 사용할 수 있습니다.  
  
-   문자 형식으로 **money** 값을 출력 하는 경우 ODBC 대량 복사 함수는 네 자리 전체 자릿수를 제공 하 고 쉼표 구분 기호는 제공 하지 않습니다. DB-LIBRARY 버전은 두 자릿수의 전체 자릿수를 제공 하 고 쉼표 구분 기호를 포함 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;대량 복사 작업 수행](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
