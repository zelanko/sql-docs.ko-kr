---
title: bcp_gettypename | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_gettypename
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d2752a1708c5727567de470b49d4cbcc63f90923
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73782650"
---
# <a name="bcp_gettypename"></a>bcp_gettypename
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  지정한 BCP 유형 토큰의 SQL 유형 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_gettypename (  
        INT token,  
        DBBOOL fIsMaxType);  
```  
  
## <a name="arguments"></a>인수  
 *토큰*  
 BCP 유형 토큰을 나타내는 값입니다.  
  
 *필드가*  
 요청된 토큰이 max 유형인지 여부를 나타냅니다.  
  
## <a name="returns"></a>반환  
 BCP 유형에 해당하는 SQL 유형 이름이 포함된 문자열입니다. 잘못된 BCP 유형을 지정하면 빈 문자열이 반환됩니다.  
  
## <a name="remarks"></a>설명  
 BCP 유형 토큰은 sqlncli.h 헤더 파일과 sqlncli11.lib 라이브러리에서 정의됩니다.  
  
 다음 표에서는 가능한 BCP 유형, max 유형인지 여부 및 예상 출력을 지정합니다.  
  
|BCP 유형 이름|MaxType|출력|  
|-------------------|-------------|------------|  
|**SQLDECIMAL**|여기서는|**decimal**|  
|**SQLNUMERIC**|여기서는|**numeric**|  
|**SQLINT1**|여기서는|**tinyint**|  
|**SQLINT2**|여기서는|**smallint**|  
|**SQLINT4**|여기서는|**int**|  
|**SQLMONEY**|여기서는|**money**|  
|**SQLFLT8**|여기서는|**float**|  
|**SQLDATETIME**|여기서는|**datetime**|  
|**SQLBITN**|여기서는|**bit-null**|  
|**SQLBIT**|여기서는|**bit**|  
|**SQLBIGCHAR**|아니요|**char**|  
|**SQLCHARACTER**|아니요|**char**|  
|**SQLBIGVARCHAR**|아니요|**varchar**|  
|**SQLVARCHAR**|아니요|**varchar**|  
|**SQLTEXT**|여기서는|**text**|  
|**SQLBIGBINARY**|아니요|**binary**|  
|**SQLBINARY**|아니요|**바이너리**|  
|**SQLBIGVARBINARY**|아니요|**Varbinary**|  
|**SQLVARBINARY**|아니요|**Varbinary**|  
|**SQLIMAGE**|여기서는|**이미지**|  
|**SQLINTN**|여기서는|**int-null**|  
|**SQLDATETIMN**|여기서는|**datetime-null**|  
|**SQLMONEYN**|여기서는|**money-null**|  
|**SQLFLTN**|여기서는|**float-null**|  
|**SQLAOPSUM**|여기서는|**총합**|  
|**SQLAOPAVG**|여기서는|**매출**|  
|**SQLAOPCNT**|여기서는|**Count**|  
|**SQLAOPMIN**|여기서는|**일별**|  
|**SQLAOPMAX**|여기서는|**최대값**|  
|**SQLDATETIM4**|여기서는|**smalldatetime**|  
|**SQLMONEY4**|여기서는|**Smallmoney**|  
|**SQLFLT4**|여기서는|**실제로**|  
|**SQLUNIQUEID**|여기서는|**uniqueidentifier**|  
|**SQLNCHAR**|아니요|**Nchar**|  
|**SQLNVARCHAR**|아니요|**Varchar**|  
|**SQLNTEXT**|여기서는|**N**|  
|**SQLVARIANT**|여기서는|**sql_variant**|  
|**SQLINT8**|여기서는|**Bigint**|  
|**SQLCHARACTER**|예|**varchar(max)**|  
|**SQLBIGCHAR**|예|**varchar(max)**|  
|**SQLBIGVARCHAR**|예|**varchar(max)**|  
|**SQLVARCHAR**|예|**varchar(max)**|  
|**SQLBINARY**|예|**varbinary(max)**|  
|**SQLBIGBINARY**|예|**varbinary(max)**|  
|**SQLBIGVARBINARY**|예|**varbinary(max)**|  
|**SQLVARBINARY**|예|**varbinary(max)**|  
|**SQLNCHAR**|예|**nvarchar(max)**|  
|**SQLNVARCHAR**|예|**nvarchar(max)**|  
|**SQLXML**|예|**Xml**|  
|**SQLUDT**|여기서는|**Udt**|  
  
## <a name="bcp_gettypename-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 bcp_gettypename 지원  
 날짜/시간 형식에 대 한 토큰 매개 변수 값은 [OLE DB 및 ODBC&#41;&#40;향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 내용 ](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)에서 테이블의 "sqlncli 형식" 열에 설명 되어 있습니다. 반환 값은 "파일 스토리지 유형" 열의 해당 행에 있습니다.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
