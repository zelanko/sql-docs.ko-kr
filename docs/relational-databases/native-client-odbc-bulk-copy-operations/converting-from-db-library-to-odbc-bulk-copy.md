---
title: Db-library에서 ODBC 대량 복사로 변환 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 81d44a01e46078599fe601d672211a9d615ce528
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124053"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>DB-Library에서 ODBC 대량 복사로 변환
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Db-library 대량 복사 프로그램을 odbc로 변환 되므로 쉽게 대량 복사 함수에서 지 원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 Db-library 대량 복사 함수에서 다음과 같은 예외가 비슷합니다.  
  
-   DB-Library 응용 프로그램은 DBPROCESS 구조에 대한 포인터를 대량 복사 함수의 첫 번째 매개 변수로 전달합니다. ODBC 응용 프로그램에서는 DBPROCESS 포인터가 ODBC 연결 핸들로 대체됩니다.  
  
-   Db-library 응용 프로그램 호출 **BCP_SETL** 연결 여 DBPROCESS에서 대량 복사 작업을 사용 하도록 설정 하기 전에 합니다. ODBC 응용 프로그램 대신 호출 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 연결 연결 핸들에서 대량 작업을 사용 하도록 설정 하기 전에:  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 호출 해야 합니다; Native Client ODBC 드라이버는 Db-library 메시지 및 오류 처리기를 지원 하지 않습니다 **SQLGetDiagRec** 오류 및 ODBC 대량 복사 함수에서 발생 하는 메시지를 가져오려고 합니다. ODBC 버전의 대량 복사 함수는 SQL_SUCCESS 또는 SQL_ERROR와 같은 ODBC 스타일 반환 코드가 아니라 표준 대량 복사 반환 코드인 SUCCEED 또는 FAILED를 반환합니다.  
  
-   Db-library 지정 된 값 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen* 매개 변수는 ODBC 다르게 해석 됩니다 **bcp_bind**_cbData_매개 변수입니다.  
  
    |나타내는 조건|Db-library *varlen* 값|ODBC *cbData* 값|  
    |-------------------------|--------------------------------|-------------------------|  
    |Null 값 제공|0|-1(SQL_NULL_DATA)|  
    |변수 데이터 제공|-1|-10(SQL_VARLEN_DATA)|  
    |길이가 0인 문자 또는 이진 문자열|NA|0|  
  
     DB-라이브러리에는 *varlen* 값이-1 이면 가변 길이 데이터를 제공 되는 odbc *cbData* NULL 값만 제공 되는 의미로 해석 됩니다. 모든 Db-library 변경 *varlen* SQL_VARLEN_DATA-1과와 사양 *varlen* 사양 0은 모두 SQL_NULL_DATA로 합니다.  
  
-   Db-library **bcp_colfmt**_file_collen_ 및 ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*cbUserData* 으로 동일한 문제가  **bcp_bind**_varlen_ 하 고 *cbData* 위에서 언급 한 매개 변수입니다. 모든 Db-library 변경 *file_collen* SQL_VARLEN_DATA-1과와 사양 *file_collen* 사양 0은 모두 SQL_NULL_DATA로 합니다.  
  
-   합니다 *iValue* ODBC의 매개 변수 [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 함수는 void 포인터입니다. Db-library에서 *iValue* 는 정수 였습니다. ODBC에 대 한 값을 캐스팅 *iValue* void * 합니다.  
  
-   합니다 **bcp_control** BCPMAXERRS 옵션 지정 개별 행의 수가 오류가 있어야 대량 복사 작업이 실패 합니다. BCPMAXERRS의 기본값은 0 (첫 번째 오류 발생 시 실패)의 Db-library 버전 **bcp_control** 및 ODBC 버전에는 10입니다. 대량 복사 작업을 종료 하는 0의 기본값에 의존 하는 Db-library 응용 프로그램을 ODBC 호출을 변경 해야 합니다 **bcp_control** BCPMAXERRS를 0으로 설정 합니다.  
  
-   ODBC **bcp_control** 함수에는 Db-library 버전에서 지원 되지 않습니다 다음 옵션을 지원 합니다 **bcp_control**:  
  
    -   BCPODBC  
  
         지정 TRUE로 설정 하면 **날짜/시간** 하 고 **smalldatetime** 문자 형식으로 저장 하는 값은 ODBC 타임 스탬프 이스케이프 시퀀스 접두사 및 접미사를 갖습니다. 이 옵션은 BCP_OUT 작업에만 적용됩니다.  
  
         Bcpodbc를 FALSE로 설정 된 **날짜/시간** 을 문자열로 변환 된 값으로 출력 됩니다:  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         동일한 TRUE로 설정 하는 bcpodbc **날짜/시간** 값으로 출력 됩니다.  
  
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
  
-   ODBC **bcp_colfmt** 함수를 지원 하지 않습니다는 *file_type* SQLCHAR의 표시기 ODBC SQLCHAR typedef와 충돌 하기 때문에 있습니다. 에 대 한 대신 SQLCHARACTER를 사용 **bcp_colfmt**합니다.  
  
-   대량 복사 함수를 사용 하기 위한 형식은 ODBC 버전에서 **날짜/시간** 하 고 **smalldatetime** 문자열의 값은 yyyy: mm: ss.sss 이지만의 ODBC 형식 **smalldatetime** h:mm: ss yyyy-월-일 형식의 ODBC를 사용 하는 값입니다.  
  
     대량 복사 함수는 Db-library 버전에서는 사용할 **날짜/시간** 하 고 **smalldatetime** 여러 형식을 사용 하 여 문자열의 값:  
  
    -   기본 형식은 *mmm dd yyyy hh: mmxx* 여기서 *xx* 는 AM 또는 PM입니다.  
  
    -   **날짜/시간** 하 고 **smalldatetime** Db-library에서 지 원하는 모든 형식으로 문자열 **dbconvert** 함수입니다.  
  
    -   경우는 **국가별 설정 사용** Db-library에서 확인란 **옵션** 탭을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 네트워크 유틸리티와 Db-library 대량 복사 함수 날짜도 국가 클라이언트 컴퓨터 레지스트리의 로캘 설정에 대해 정의 된 날짜 형식입니다.  
  
     Db-library 대량 복사 함수에서는 ODBC를 허용 하지 않습니다 **날짜/시간** 하 고 **smalldatetime** 형식입니다.  
  
     SQL_SOPT_SS_REGIONALIZE 문 특성을 SQL_RE_ON으로 설정하면 ODBC 대량 복사 함수에서는 클라이언트 컴퓨터 레지스트리의 로캘 설정에 정의된 국가별 날짜 형식의 날짜를 사용할 수 있습니다.  
  
-   출력할 때 **money** 문자 형식, ODBC 대량 복사 함수 공급 4 자리의 전체 자릿수 및 쉼표 구분 기호 없음; 값 만 Db-library 버전 2 자리의 전체 자릿수만 제공 하 고 쉼표 구분 기호를 포함 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 작업 수행 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
