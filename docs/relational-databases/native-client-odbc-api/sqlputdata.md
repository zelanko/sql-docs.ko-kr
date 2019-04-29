---
title: SQLPutData | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8c8755b100fcfbdb8c1ca9e067a79eb09bd37ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014279"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLPutData를 사용 하 여 65,535 바이트 이상의 데이터를 전송 하는 경우 다음 제한 사항이 적용 (에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 4.21a) 또는 400KB sql_longvarchar (SQL Server 버전 6.0 이상)에 대 한 데이터 (**텍스트**), SQL_WLONGVARCHAR (**ntext**) 또는 SQL_LONGVARBINARY (**이미지**) 열:  
  
-   참조 된 매개 변수 수를 *insert_value* 문입니다.  
  
-   참조 된 매개 변수 수를 *식* UPDATE 문의 SET 절에서.  
  
 블록을 실행 하는 서버에서 데이터를 제공 하는 SQLPutData 호출 시퀀스로 취소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 또는 이전 버전을 사용 하는 경우 열 값의 부분 업데이트를 사용 하면 됩니다. 합니다 **텍스트**를 **ntext**, 또는 **이미지** SQLCancel가 호출 될 때 참조 된 열은 중간 자리 표시자 값으로 설정 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전에 대한 연결을 지원하지 않습니다.  
  
## <a name="diagnostics"></a>진단  
 하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 관련 SQLSTATE SQLPutData에 대 한 합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|22026|문자열 데이터, 길이가 일치하지 않음|보낼 바이트에는 데이터의 길이 지정 된 경우 응용 프로그램에 예를 들어 SQL_LEN_DATA_AT_EXEC를 사용 하 여 (*n*) 위치 *n* 를 통해 응용 프로그램에서 지정 된 바이트의 총 수는 0 보다 크면 SQLPutData 지정된 된 길이 일치 해야 합니다.|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData 및 테이블 반환 매개 변수  
 SQLPutData 가변 행 바인딩을 테이블 반환 매개 변수를 사용 하 여 사용 하는 경우 응용 프로그램에서 사용 됩니다. 합니다 *StrLen_Or_Ind* 매개 변수는 행이 더 이상 사용할 수 있는지 또는 드라이버가 다음 행 또는 테이블 반환 매개 변수 데이터의 행 데이터를 수집할 준비가 되었음을 나타냅니다.  
  
-   0보다 큰 값은 다음 행 값의 집합을 사용할 수 있음을 나타냅니다.  
  
-   값이 0이면 보낼 행이 더 이상 없음을 나타냅니다.  
  
-   0보다 작은 값은 오류를 나타내며 SQLState HY090 및 "잘못된 문자열 또는 버퍼 길이입니다."라는 메시지가 포함된 진단 레코드가 기록됩니다.  
  
 합니다 *DataPtr* 매개 변수는 무시 되지만 NULL이 아닌 값으로 설정 해야 합니다. 변수 TVP 행 바인딩에 대 한 자세한 내용은 섹션을 참조 [바인딩 및 Data Transfer of Table-Valued 매개 변수 및 열 값](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)합니다.  
  
 경우 *StrLen_Or_Ind* SQL_DEFAULT_PARAM 또는 0과 SQL_PARAMSET_SIZE 사이의 숫자 이외의 모든 값 (즉, 합니다 *ColumnSize* SQLBindParameter의 매개 변수), 오류가 발생 합니다. 이 오류로 인해 SQLPutData에서 SQL_ERROR를 반환 합니다. SQLSTATE HY090, = "잘못 된 문자열 또는 버퍼 길이"입니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLPutData 지원  
 에 설명 된 대로 날짜/시간 형식의 매개 변수 값을 변환할지 [C에서 SQL로 변환을](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)입니다.  
  
 자세한 내용은 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLPutData 지원  
 **SQLPutData** 큰 CLR 사용자 정의 형식 (Udt)를 지원 합니다. 자세한 내용은 [Large CLR User-Defined 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLPutData Function](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
