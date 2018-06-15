---
title: ODBC 대량 복사로 Db-library에서 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- converting DB-Library to ODBC bulk copy
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], DB-Library bulk copy
- ODBC, bulk copy operations
- DB-Library bulk copy
ms.assetid: 0bc15bdb-f19f-4537-ac6c-f249f42cf07f
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bc8072a1bd0f0e3a097a01696c9d034e0acb33c7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32946308"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>DB-Library에서 ODBC 대량 복사로 변환
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Db-library 대량 복사 프로그램을 ODBC로 변환 되므로 쉽게 대량 복사 함수에서 지원 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 Db-library 대량 복사 함수는 다음과 같은 예외가 비슷합니다.  
  
-   DB-Library 응용 프로그램은 DBPROCESS 구조에 대한 포인터를 대량 복사 함수의 첫 번째 매개 변수로 전달합니다. ODBC 응용 프로그램에서는 DBPROCESS 포인터가 ODBC 연결 핸들로 대체됩니다.  
  
-   Db-library 응용 프로그램 호출 **BCP_SETL** 여 DBPROCESS에서 대량 복사 작업을 사용 하도록 설정에 연결 하기 전에. ODBC 응용 프로그램 대신 호출 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 연결 핸들의 대량 작업을 사용 하도록 연결 하기 전에:  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 Db-library 메시지 및 오류 처리기를 지원 하지 않으며 호출 해야 **SQLGetDiagRec** 오류 및 ODBC 대량 복사 함수에 의해 발생 하는 메시지를 가져옵니다. ODBC 버전의 대량 복사 함수는 SQL_SUCCESS 또는 SQL_ERROR와 같은 ODBC 스타일 반환 코드가 아니라 표준 대량 복사 반환 코드인 SUCCEED 또는 FAILED를 반환합니다.  
  
-   DB 라이브러리에 대 한 지정 된 값 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen* 매개 변수는 ODBC 다르게 해석 되는 **bcp_bind * * * cbData* 매개 변수입니다.  
  
    |나타내는 조건|Db-library *varlen* 값|ODBC *cbData* 값|  
    |-------------------------|--------------------------------|-------------------------|  
    |Null 값 제공|0|-1(SQL_NULL_DATA)|  
    |변수 데이터 제공|-1|-10(SQL_VARLEN_DATA)|  
    |길이가 0인 문자 또는 이진 문자열|NA|0|  
  
     Db-library,는 *varlen* 값이-1 이면 가변 길이 데이터가 제공 되는 ODBC의 *cbData* 에 NULL 값만 제공 되 고 의미로 해석 됩니다. 모든 Db-library 변경 *varlen* SQL_VARLEN_DATA로-1과 모든 사양 *varlen* 사양 SQL_NULL_DATA로 0입니다.  
  
-   Db-library  **bcp_colfmt * * * file_collen* 및 ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)* cbUserData * 에서도 같은 문제가로 **bcp_bind * * * varlen*및 *cbData* 위에 설명 된 매개 변수입니다. 모든 Db-library 변경 *file_collen* SQL_VARLEN_DATA로-1과 모든 사양 *file_collen* 사양 SQL_NULL_DATA로 0입니다.  
  
-   *iValue* ODBC의 매개 변수 [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 함수는 void 포인터입니다. Db-library, *iValue* 는 정수 였습니다. ODBC에 대 한 값을 캐스팅 *iValue* void * 합니다.  
  
-   **bcp_control** 옵션 BCPMAXERRS 개별 행의 수는 대량 복사 작업이 실패 하기 전에 오류를 가질 수를 지정 합니다. BCPMAXERRS의 기본값은 0 (첫 번째 오류 발생 시 실패)의 Db-library 버전에서 **bcp_control** 및 ODBC 버전에는 10입니다. 기본값은 대량 복사 작업을 종료 하는 0에 의존 하는 Db-library 응용 프로그램 ODBC 호출을 변경 해야 **bcp_control** BCPMAXERRS를 0으로 설정 합니다.  
  
-   ODBC **bcp_control** 함수는 Db-library 버전에서 지원 되지 않는 다음 옵션을 지원 **bcp_control**:  
  
    -   BCPODBC  
  
         TRUE를 지정 하는로 설정 하면 **datetime** 및 **smalldatetime** ODBC 타임 스탬프 이스케이프 시퀀스 접두사 및 접미사 문자 형식으로 저장 하는 값을 갖습니다. 이 옵션은 BCP_OUT 작업에만 적용됩니다.  
  
         BCPODBC를 FALSE로 설정 된는 **datetime** 문자로 된 문자열로 변환 된 값으로 출력 됩니다.  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         동일한 TRUE로 설정 하는 bcpodbc **datetime** 값으로 출력 됩니다.  
  
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
  
-   ODBC **bcp_colfmt** 함수 지원 하지 않습니다는 *file_type* SQLCHAR의 표시기 ODBC SQLCHAR typedef와 충돌 하기 때문에 있습니다. 에 대 한 대신 SQLCHARACTER를 사용 **bcp_colfmt**합니다.  
  
-   ODBC 버전의 대량 복사 함수를 사용 하기 위한 형식 **datetime** 및 **smalldatetime** 문자열의 값은 yyyy-월-일 ss.sss 이지만의 ODBC 형식입니다. **smalldatetime** ODBC h:mm: ss yyyy-월-일 형식의 값을 사용 합니다.  
  
     대량 복사 함수는 Db-library 버전에서는 사용할 **datetime** 및 **smalldatetime** 여러 형식을 사용 하 여 문자열의 값:  
  
    -   기본 형식은 *mmm dd yyyy hh: mmxx* 여기서 *xx* 는 AM 또는 PM입니다.  
  
    -   **날짜/시간** 및 **smalldatetime** DB 라이브러리에서 지 원하는 모든 형식 문자열 **dbconvert** 함수입니다.  
  
    -   때는 **국가별 설정을 사용 하 여** Db-library에서 확인란이 **옵션** 탭은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 네트워크 유틸리티는 Db-library 대량 복사 함수 날짜도 사용할 지역 클라이언트 컴퓨터 레지스트리의 로캘 설정에 대해 정의 된 날짜 형식입니다.  
  
     Db-library 대량 복사 함수에서는 ODBC를 받아들이지 않습니다 **datetime** 및 **smalldatetime** 형식입니다.  
  
     SQL_SOPT_SS_REGIONALIZE 문 특성을 SQL_RE_ON으로 설정하면 ODBC 대량 복사 함수에서는 클라이언트 컴퓨터 레지스트리의 로캘 설정에 정의된 국가별 날짜 형식의 날짜를 사용할 수 있습니다.  
  
-   출력할 때 **money** 문자 형식, ODBC 대량 복사 함수 공급 4 자리의 전체 자릿수 및 쉼표 구분 기호;의 값 만 Db-library 버전 두 자리의 전체 자릿수를 제공 하 고 쉼표 구분 기호를 포함 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [대량 복사 작업 수행 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
