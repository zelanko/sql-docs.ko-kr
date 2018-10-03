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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: de5b4a62dbb86008f686cb0d630386340238f42c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743201"
---
# <a name="bcpgettypename"></a>bcp_gettypename
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  지정한 BCP 유형 토큰의 SQL 유형 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_gettypename (  
        INT token,  
        DBBOOL fIsMaxType);  
```  
  
## <a name="arguments"></a>인수  
 *token*  
 BCP 유형 토큰을 나타내는 값입니다.  
  
 *field*  
 요청된 토큰이 max 유형인지 여부를 나타냅니다.  
  
## <a name="returns"></a>반환 값  
 BCP 유형에 해당하는 SQL 유형 이름이 포함된 문자열입니다. 잘못된 BCP 유형을 지정하면 빈 문자열이 반환됩니다.  
  
## <a name="remarks"></a>Remarks  
 BCP 유형 토큰은 sqlncli.h 헤더 파일과 sqlncli11.lib 라이브러리에서 정의됩니다.  
  
 다음 표에서는 가능한 BCP 유형, max 유형인지 여부 및 예상 출력을 지정합니다.  
  
|BCP 유형 이름|MaxType|출력|  
|-------------------|-------------|------------|  
|**SQLDECIMAL**|모두|**decimal**|  
|**SQLNUMERIC**|모두|**numeric**|  
|**SQLINT1**|모두|**tinyint**|  
|**SQLINT2**|모두|**smallint**|  
|**SQLINT4**|모두|**int**|  
|**SQLMONEY**|모두|**money**|  
|**SQLFLT8**|모두|**float**|  
|**SQLDATETIME**|모두|**datetime**|  
|**SQLBITN**|모두|**bit-null**|  
|**SQLBIT**|모두|**bit**|  
|**SQLBIGCHAR**|아니요|**char**|  
|**SQLCHARACTER**|아니요|**char**|  
|**SQLBIGVARCHAR**|아니요|**varchar**|  
|**SQLVARCHAR**|아니요|**varchar**|  
|**SQLTEXT**|모두|**text**|  
|**SQLBIGBINARY**|아니요|**binary**|  
|**SQLBINARY**|아니요|**이진**|  
|**SQLBIGVARBINARY**|아니요|**Varbinary**|  
|**SQLVARBINARY**|아니요|**Varbinary**|  
|**SQLIMAGE**|모두|**이미지**|  
|**SQLINTN**|모두|**int-null**|  
|**SQLDATETIMN**|모두|**datetime-null**|  
|**SQLMONEYN**|모두|**money-null**|  
|**SQLFLTN**|모두|**float-null**|  
|**SQLAOPSUM**|모두|**Sum**|  
|**SQLAOPAVG**|모두|**Avg**|  
|**SQLAOPCNT**|모두|**개수**|  
|**SQLAOPMIN**|모두|**Min**|  
|**SQLAOPMAX**|모두|**Max**|  
|**SQLDATETIM4**|모두|**smalldatetime**|  
|**SQLMONEY4**|모두|**smallmoney**|  
|**SQLFLT4**|모두|**실제**|  
|**SQLUNIQUEID**|모두|**uniqueidentifier**|  
|**SQLNCHAR**|아니요|**Nchar**|  
|**SQLNVARCHAR**|아니요|**Nvarchar**|  
|**SQLNTEXT**|모두|**ntext**|  
|**SQLVARIANT**|모두|**sql_variant**|  
|**SQLINT8**|모두|**Bigint**|  
|**SQLCHARACTER**|사용자 계정 컨트롤|**varchar(max)**|  
|**SQLBIGCHAR**|사용자 계정 컨트롤|**varchar(max)**|  
|**SQLBIGVARCHAR**|사용자 계정 컨트롤|**varchar(max)**|  
|**SQLVARCHAR**|사용자 계정 컨트롤|**varchar(max)**|  
|**SQLBINARY**|사용자 계정 컨트롤|**varbinary(max)**|  
|**SQLBIGBINARY**|사용자 계정 컨트롤|**varbinary(max)**|  
|**SQLBIGVARBINARY**|사용자 계정 컨트롤|**varbinary(max)**|  
|**SQLVARBINARY**|사용자 계정 컨트롤|**varbinary(max)**|  
|**SQLNCHAR**|사용자 계정 컨트롤|**nvarchar(max)**|  
|**SQLNVARCHAR**|사용자 계정 컨트롤|**nvarchar(max)**|  
|**SQLXML**|사용자 계정 컨트롤|**Xml**|  
|**SQLUDT**|모두|**udt**|  
  
## <a name="bcpgettypename-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 bcp_gettypename 지원  
 날짜/시간 형식에 대 한 토큰 매개 변수 값에서 테이블의 "sqlncli.h의 유형" 열에 나와 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)합니다. 반환 값은 "파일 저장소 유형" 열의 해당 행에 있습니다.  
  
 자세한 내용은 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
