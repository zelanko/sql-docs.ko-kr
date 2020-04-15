---
title: SQLPutData | 마이크로 소프트 문서
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
ms.openlocfilehash: e063d1053d8a6e5e10a1234d33893adf27fbc3ad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302367"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  다음 제한 사항은 SQLPutData를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL_LONGVARCHAR(텍스트), SQL_WLONGVARCHAR(ntext) 또는 SQL_LONGVARBINARY(이미지) 열에 대해 65,535바이트 이상의 데이터(버전 4.21a) 또는 400KB**image**이상의 데이터(SQL Server 버전 6.0 이상)를 보낼 때 적용됩니다.**text****ntext**  
  
-   참조된 매개 변수는 INSERT 문의 *insert_value* 될 수 있습니다.  
  
-   참조된 매개 변수는 UPDATE 문의 SET 절에서 *식일* 수 있습니다.  
  
 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버에 블록의 데이터를 제공하는 SQLPutData 호출 시퀀스를 취소하면 버전 6.5 이전을 사용할 때 열 값이 부분적으로 업데이트됩니다. SQLCancel이 호출될 때 참조된 **텍스트,** **ntext**또는 **이미지** 열은 중간 자리 표시자 값으로 설정됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.5 및 이전 버전에 대한 연결을 지원하지 않습니다.  
  
## <a name="diagnostics"></a>진단  
 SQLPutData에 대한 하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 특정 SQLSTATE가 있습니다.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|22026|문자열 데이터, 길이가 일치하지 않음|송신할 바이트의 데이터 길이 응용 프로그램에서 지정한 경우(예: *n이* 0보다 큰*SQL_LEN_DATA_AT_EXEC(n)를*사용하면 SQLPutData를 통해 응용 프로그램에서 제공하는 총 바이트 수가 지정된 길이와 일치해야 합니다.|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData 및 테이블 반환 매개 변수  
 SQLPutData 테이블 값 매개 변수와 변수 행 바인딩을 사용 하는 경우 응용 프로그램에서 사용 됩니다. *StrLen_Or_Ind* 매개 변수는 드라이버가 테이블 값 매개 변수 데이터의 다음 행 또는 행에 대한 데이터를 수집할 준비가 되거나 더 이상 행을 사용할 수 없음을 나타냅니다.  
  
-   0보다 큰 값은 다음 행 값의 집합을 사용할 수 있음을 나타냅니다.  
  
-   값이 0이면 보낼 행이 더 이상 없음을 나타냅니다.  
  
-   0보다 작은 값은 오류를 나타내며 SQLState HY090 및 "잘못된 문자열 또는 버퍼 길이입니다."라는 메시지가 포함된 진단 레코드가 기록됩니다.  
  
 *DataPtr* 매개 변수는 무시되지만 NULL이 아닌 값으로 설정해야 합니다. 자세한 내용은 테이블 값 매개 변수 및 [열 값의 바인딩 및 데이터 전송에서](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)변수 TVP 행 바인딩의 섹션을 참조하십시오.  
  
 *StrLen_Or_Ind* SQL_DEFAULT_PARAM 이외의 값 또는 0과 SQL_PARAMSET_SIZE 사이의 숫자(즉, *COLUMNSize* 매개 변수/SQLBindParameter)가 있는 경우 오류입니다. 이 오류로 인해 SQLPutData SQL_ERROR 반환: SQLSTATE=HY090, "잘못 된 문자열 또는 버퍼 길이".  
  
 테이블 값 매개 변수에 대한 자세한 내용은 ODBC&#41;[&#40;테이블 값 매개 변수를 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)참조하십시오.  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLPutData 지원  
 날짜/시간 형식의 매개 변수 값은 [C에서 SQL로의 변환에](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)설명된 대로 변환됩니다.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLPutData 지원  
 **SQLPutData는** 큰 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLPutData 함수](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
