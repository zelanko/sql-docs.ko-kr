---
title: 날짜 및 시간 기능 향상을 위한 데이터 형식 지원(OLE DB 드라이버) | Microsoft Docs
description: OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], data type support
- OLE DB, date/time improvements
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c4306574aca251ad1f530cfeb3c26ce91e0a48b1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244881"
---
# <a name="data-type-support-for-ole-db-date-and-time-improvements"></a>OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 문서에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 날짜/시간 데이터 형식을 지원하는 OLE DB(OLE DB Driver for SQL Server) 형식에 대한 정보를 제공합니다.  
  
## <a name="data-type-mapping-in-rowsets-and-parameters"></a>행 집합 및 매개 변수의 데이터 형식 매핑  
 OLE DB에는 새로운 서버 유형을 지원하기 위해 DBTYPE_DBTIME2 및 DBTYPE_DBTIMESTAMPOFFSET이라는 새로운 데이터 형식이 제공됩니다. 다음 표에서는 전체 서버 유형 매핑을 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식|OLE DB 데이터 형식|값|  
|-----------------------------------------|----------------------|-----------|  
|Datetime|DBTYPE_DBTIMESTAMP|135(oledb.h)|  
|smalldatetime|DBTYPE_DBTIMESTAMP|135(oledb.h)|  
|date|DBTYPE_DBDATE|133(oledb.h)|  
|time|DBTYPE_DBTIME2|145(msoledbsql.h)|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|146(msoledbsql.h)|  
|datetime2|DBTYPE_DBTIMESTAMP|135(oledb.h)|  
  
## <a name="data-formats-strings-and-literals"></a>데이터 형식: 문자열 및 리터럴  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식|OLE DB 데이터 형식|클라이언트 변환을 위한 문자열 형식|  
|-----------------------------------------|----------------------|------------------------------------------|  
|Datetime|DBTYPE_DBTIMESTAMP|'yyyy-mm-dd hh:mm:ss[.999]'<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 Datetime에 대해 최대 3자리의 소수 자릿수 초를 지원합니다.|  
|smalldatetime|DBTYPE_DBTIMESTAMP|'yyyy-mm-dd hh:mm:ss'<br /><br /> 이 데이터 형식의 정확도는 1분 단위입니다. 초 구성 요소 부분은 출력 시 0이 되고, 입력 시 서버에 의해 반올림됩니다.|  
|date|DBTYPE_DBDATE|'yyyy-mm-dd'|  
|time|DBTYPE_DBTIME2|'hh:mm:ss[.9999999]'<br /><br /> 필요한 경우 소수 자릿수 초를 일곱 자리까지 지정할 수 있습니다.|  
|datetime2|DBTYPE_DBTIMESTAMP|'yyyy-mm-dd hh:mm:ss[.fffffff]'<br /><br /> 필요한 경우 소수 자릿수 초를 일곱 자리까지 지정할 수 있습니다.|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|'yyyy-mm-dd hh:mm:ss[.fffffff] +/-hh:mm'<br /><br /> 필요한 경우 소수 자릿수 초를 일곱 자리까지 지정할 수 있습니다.|  
  
 날짜/시간 리터럴에 대한 이스케이프 시퀀스에는 변경 내용이 없습니다.  
  
 결과의 소수 자릿수 초는 콜론(:)이 아닌 점(.)을 사용합니다.  
  
 애플리케이션에 반환되는 문자열 값은 지정된 열에 대해 길이가 항상 동일합니다. 연도, 월, 일, 시간, 분 및 초 구성 요소에는 최대 너비까지 앞에 0이 채워지고 날짜와 시간 사이 및 시간과 표준 시간대 오프셋 사이에는 공백이 하나씩 있습니다. 표준 시간대 오프셋 앞에는 항상 부호가 나오며 오프셋이 0인 경우에는 더하기(+) 부호가 사용됩니다. 부호와 오프셋 값 사이에는 공백이 없습니다. 필요한 경우 소수 자릿수 초의 뒷부분은 열에 정의된 전체 자릿수까지만 0으로 채워집니다. datetime 열의 경우 소수 자릿수 초는 3자리입니다. smalldatetime 열의 경우 소수 자릿수 초의 자릿수가 정의되지 않으며 초는 항상 0이 됩니다.  
  
 애플리케이션에서 제공하는 문자열 값을 보다 유연하게 변환할 수 있으며 최대 너비보다 작은 구성 요소 값도 허용됩니다. 연도는 1 - 4자리일 수 있고 월, 일, 시간, 분 및 초는 1자리 또는 2자리일 수 있습니다. 날짜/시간 및 시간/표준 시간대 오프셋 사이에 임의의 개수의 공백을 사용할 수 있습니다. 0시간 0분 오프셋의 부호는 더하기 또는 빼기 모두 될 수 있습니다. 소수 자릿수 초의 뒤에는 0을 최대 9자리까지 표시할 수 있습니다. 시간 구성 요소는 소수 자릿수 초의 자릿수 없이 소수점으로 끝날 수 있습니다.  
  
 빈 문자열은 유효한 날짜/시간 리터럴이 아니며 NULL 값을 나타내지 않습니다. 빈 문자열을 날짜/시간 값으로 변환하려고 하면 SQLState 22018 및 "캐스트 사양의 문자 값이 올바르지 않습니다."라는 메시지와 함께 오류가 발생합니다.  
  
## <a name="data-formats-data-structures"></a>데이터 형식: 데이터 구조  
 아래에 설명된 OLE DB별 구조에서 OLE DB는 다음 제약 조건을 준수합니다. 이러한 제약 조건은 일반 달력을 기준으로 합니다.  
  
-   월 범위는 1에서 12까지입니다.  
  
-   일 필드의 범위는 1에서 해당 월의 일 수까지이며, 윤년을 고려하여 연도 및 월 필드와 일관성을 유지해야 합니다.  
  
-   시 범위는 0에서 23까지입니다.  
  
-   분 범위는 0에서 59까지입니다.  
  
-   초 범위는 0에서 59까지입니다. 이는 항성시와의 동기화를 유지하기 위한 최대 2초의 윤초를 허용합니다.  
  
 다음과 같은 기존 OLE DB 구조체의 구현은 새로운 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 날짜 및 시간 데이터 형식을 지원하도록 수정되었습니다. 단, 정의는 변경되지 않았습니다.  
  
-   DBTYPE_DATE. 자동 DATE 형식입니다. 내부적으로 **double**로 표시됩니다. 정수 부분은 1899년 12월 30일 이후의 일 수이고, 소수 부분은 하루를 분수로 표시한 수입니다. 이 형식의 정확도는 1초 단위이므로 소수 자릿수가 0입니다.  
  
-   DBTYPE_DBDATE  
  
-   DBTYPE_DBTIME  
  
-   DBTYPE_DBTIMESTAMP. OLE DB에서 분수 필드는 10억분의 1초(나노초)로 정의되며 범위는 0-999,999,999입니다.  
  
-   DBTYPE_FILETIME  
  
### <a name="dbtype_dbtime2"></a>DBTYPE_DBTIME2  
 이 구조체는 32비트와 64비트 운영 체제 모두에서 12바이트까지 채워집니다.  
  
```  
typedef struct tagDBTIME2 {  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    } DBTIME2;  
```  
  
### <a name="dbtype_-dbtimestampoffset"></a>DBTYPE_ DBTIMESTAMPOFFSET  
  
```  
typedef struct tagDBTIMESTAMPOFFSET {  
    SHORT year;  
    USHORT month;  
    USHORT day;  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    SHORT timezone_hour;  
    SHORT timezone_minute;  
    } DBTIMESTAMPOFFSET;  
```  
  
 `timezone_hour`가 음수인 경우 `timezone_minute`는 음수 또는 0이어야 합니다. `timezone_hour`가 양수인 경우 `timezone minute`는 양수 또는 0이어야 합니다. `timezone_hour`가 0인 경우 `timezone minute`의 값 범위는 -59에서 +59까지입니다.  
  
### <a name="ssvariant"></a>SSVARIANT  
 이 구조체는 이제 새로운 구조인 DBTYPE_DBTIME2와 DBTYPE_DBTIMESTAMPOFFSET을 포함하고 적절한 형식에 소수 자릿수 초의 자릿수를 추가합니다.  
  
```  
struct SSVARIANT {  
   SSVARTYPE vt;  
   DWORD dwReserved1;  
   DWORD dwReserved2;  
   union {  
// ...  
      DBTIMESTAMP tsDateTimeVal;  
      DBDATE dDateVal;  
      struct _Time2Val {  
         DBTIME2 tTime2Val;  
         BYTE bScale;  
      } Time2Val;  
      struct _DateTimeVal {  
         DBTIMESTAMP tsDateTimeVal;  
         BYTE bScale;  
      } DateTimeVal;  
      struct _DateTimeOffsetVal {   
         DBTIMESTAMPOFFSET tsoDateTimeOffsetVal;  
         BYTE bScale;  
      } DateTimeOffsetVal;  
// ...  
   };  
};  
```  
  
 또한 열거형 형식을 결정하는 SSVARIANT 형식 인코딩과 관련된 열거형은 다음과 같이 확장됩니다.  
  
```  
enum SQLVARENUM {  
// ...  
   // Datetime  
   VT_SS_DATETIME      = DBTYPE_DBTIMESTAMP,  
   VT_SS_SMALLDATETIME = 206,  
  
   VT_SS_DATE = DBTYPE_DBDATE,  
   VT_SS_TIME2 = DBTYPE_DBTIME2,  
   VT_SS_DATETIME2 = 212  
   VT_SS_DATETIMEOFFSET = DBTYPE_DBTIMESTAMPOFFSET  
};  
```  
  
 **sql_variant**를 사용하고 **datetime**의 제한된 전체 자릿수를 사용하는 OLE DB Driver for SQL Server로 마이그레이션하는 애플리케이션은 기본 스키마가 **datetime** 대신 **datetime2**를 사용하도록 업데이트되는 경우 마찬가지로 업데이트되어야 합니다.  
  
 SSVARIANT의 액세스 매크로도 다음과 같은 추가를 통해 확장되었습니다.  
  
```  
#define V_SS_DATETIME2(X)       V_SS_UNION(X, DateTimeVal)  
#define V_SS_TIME2(X)           V_SS_UNION(X, Time2Val)  
#define V_SS_DATE(X)            V_SS_UNION(X, dDateVal)  
#define V_SS_DATETIMEOFFSET(X)  V_SS_UNION(X, DateTimeOffsetVal)  
```  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>ITableDefinition::CreateTable의 데이터 형식 매핑  
 다음 형식 매핑은 ITableDefinition::CreateTable에서 사용되는 DBCOLUMNDESC 구조체와 함께 사용됩니다.  
  
|OLE DB 데이터 형식(*wType*)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식|메모|  
|----------------------------------|-----------------------------------------|-----------|  
|DBTYPE_DBDATE|date||  
|DBTYPE_DBTIMESTAMP|**datetime2**(p)|OLE DB Driver for SQL Server는 DBCOLUMDESC *bScale* 멤버를 검사하여 소수 자릿수 초 전체 자릿수를 확인합니다.|  
|DBTYPE_DBTIME2|**time**(p)|OLE DB Driver for SQL Server는 DBCOLUMDESC *bScale* 멤버를 검사하여 소수 자릿수 초 전체 자릿수를 확인합니다.|  
|DBTYPE_DBTIMESTAMPOFFSET|**datetimeoffset**(p)|OLE DB Driver for SQL Server는 DBCOLUMDESC *bScale* 멤버를 검사하여 소수 자릿수 초 전체 자릿수를 확인합니다.|  
  
 애플리케이션은 *wType*에 DBTYPE_DBTIMESTAMP를 지정하면 *pwszTypeName*에 형식 이름을 지정하여 **datetime2**에 대한 매핑을 재정의할 수 있습니다. **datetime**을 지정하는 경우 *bScale*은 3이어야 합니다. **smalldatetime**을 지정하는 경우 *bScale*은 0이어야 합니다. *bScale*이 *wType* 및 *pwszTypeName*과 일치하지 않는 경우 DB_E_BADSCALE이 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
