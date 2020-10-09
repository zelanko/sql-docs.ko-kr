---
description: SQLPutData
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42323e6fbf35ddb6093ac4e764e81e7f0274cbb2
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867479"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SQLPutData를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL_LONGVARCHAR (**텍스트**), SQL_WLONGVARCHAR (**ntext**) 또는 SQL_LONGVARBINARY (**이미지**) 열에 대해 65535 바이트 이상의 데이터 (버전 4.21 a) 또는 400 KB의 데이터 (SQL Server 버전 6.0 이상)를 전송 하는 경우 다음과 같은 제한 사항이 적용 됩니다.  
  
-   참조 된 매개 변수는 INSERT 문에서 *insert_value* 수 있습니다.  
  
-   참조 된 매개 변수는 UPDATE 문의 SET 절에 있는 *식일* 수 있습니다.  
  
 을 실행 하는 서버에 블록의 데이터를 제공 하는 SQLPutData 호출의 시퀀스를 취소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하면 버전 6.5 또는 이전 버전을 사용할 때 열의 값이 부분적으로 업데이트 됩니다. SQLCancel이 호출 될 때 참조 된 **text**, **ntext**또는 **image** 열이 중간 자리 표시자 값으로 설정 되어 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전에 대한 연결을 지원하지 않습니다.  
  
## <a name="diagnostics"></a>진단  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQLPutData에 대해 하나의 Native Client 특정 SQLSTATE가 있습니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|22026|문자열 데이터, 길이가 일치하지 않음|전송할 데이터 길이 (바이트)를 응용 프로그램에서 지정 하는*경우 (예*SQL_LEN_DATA_AT_EXEC: *n* 이 0 보다 큰 경우)에는 sqlputdata를 통해 응용 프로그램에서 제공 하는 총 바이트 수가 지정 된 길이와 일치 해야 합니다.|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData 및 테이블 반환 매개 변수  
 SQLPutData는 테이블 반환 매개 변수와 함께 가변 행 바인딩을 사용할 때 응용 프로그램에서 사용 됩니다. *StrLen_Or_Ind* 매개 변수는 드라이버가 다음 행 또는 테이블 반환 매개 변수 데이터의 행에 대 한 데이터를 수집할 준비가 되었거나 더 이상 행을 사용할 수 없음을 나타냅니다.  
  
-   0보다 큰 값은 다음 행 값의 집합을 사용할 수 있음을 나타냅니다.  
  
-   값이 0이면 보낼 행이 더 이상 없음을 나타냅니다.  
  
-   0보다 작은 값은 오류를 나타내며 SQLState HY090 및 "잘못된 문자열 또는 버퍼 길이입니다."라는 메시지가 포함된 진단 레코드가 기록됩니다.  
  
 *Dataptr* 매개 변수는 무시 되지만 NULL이 아닌 값으로 설정 해야 합니다. 자세한 내용은 Binding의 Variable TVP row binding의 [및 데이터 전송 Table-Valued 매개 변수 및 열 값](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)에 대 한 섹션을 참조 하세요.  
  
 *StrLen_Or_Ind* 의 값이 SQL_DEFAULT_PARAM 또는 0과 SQL_PARAMSET_SIZE 사이의 숫자 (즉, SQLBindParameter의 *columnsize* 매개 변수) 인 경우에는 오류가 발생 합니다. 이 오류가 발생 하면 SQLPutData에서 SQLSTATE = HY090, "잘못 된 문자열 또는 버퍼 길이" SQL_ERROR 반환 됩니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLPutData 지원  
 날짜/시간 형식의 매개 변수 값은 [C에서 SQL로 변환](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)에 설명 된 대로 변환 됩니다.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLPutData 지원  
 **Sqlputdata** 는 크기가 높은 CLR udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC&#41;&#40;대량 CLR User-Defined 형식 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLPutData 함수](../../odbc/reference/syntax/sqlputdata-function.md)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
