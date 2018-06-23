---
title: bcp_gettypename | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_gettypename
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: afea684549765bac4c24679cc65d74bb4dfa47df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091504"
---
# <a name="bcpgettypename"></a>bcp_gettypename
  지정한 BCP 유형 토큰의 SQL 유형 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_gettypename (  
INT   
token  
,  
DBBOOL   
fIsMaxType  
);  
  
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
|`SQLDECIMAL`|모두|**decimal**|  
|`SQLNUMERIC`|모두|**numeric**|  
|`SQLINT1`|모두|**tinyint**|  
|`SQLINT2`|모두|**smallint**|  
|`SQLINT4`|모두|**int**|  
|`SQLMONEY`|모두|**money**|  
|`SQLFLT8`|모두|**float**|  
|`SQLDATETIME`|모두|**datetime**|  
|`SQLBITN`|모두|**bit-null**|  
|`SQLBIT`|모두|**bit**|  
|`SQLBIGCHAR`|아니요|**char**|  
|`SQLCHARACTER`|아니요|**char**|  
|`SQLBIGVARCHAR`|아니요|**varchar**|  
|`SQLVARCHAR`|아니요|**varchar**|  
|`SQLTEXT`|모두|**text**|  
|`SQLBIGBINARY`|아니요|**binary**|  
|`SQLBINARY`|아니요|**이진**|  
|`SQLBIGVARBINARY`|아니요|**Varbinary**|  
|`SQLVARBINARY`|아니요|**Varbinary**|  
|`SQLIMAGE`|모두|**이미지**|  
|`SQLINTN`|모두|**int-null**|  
|`SQLDATETIMN`|모두|**datetime-null**|  
|`SQLMONEYN`|모두|**money-null**|  
|`SQLFLTN`|모두|**float-null**|  
|`SQLAOPSUM`|모두|**Sum**|  
|`SQLAOPAVG`|모두|**Avg**|  
|`SQLAOPCNT`|모두|**개수**|  
|`SQLAOPMIN`|모두|**Min**|  
|`SQLAOPMAX`|모두|**Max**|  
|`SQLDATETIM4`|모두|**smalldatetime**|  
|`SQLMONEY4`|모두|**Smallmoney**|  
|`SQLFLT4`|모두|**실제**|  
|`SQLUNIQUEID`|모두|**uniqueidentifier**|  
|`SQLNCHAR`|아니요|**Nchar**|  
|`SQLNVARCHAR`|아니요|**Nvarchar**|  
|`SQLNTEXT`|모두|**ntext**|  
|`SQLVARIANT`|모두|**sql_variant**|  
|`SQLINT8`|모두|**Bigint**|  
|`SQLCHARACTER`|예|**varchar(max)**|  
|`SQLBIGCHAR`|예|**varchar(max)**|  
|`SQLBIGVARCHAR`|예|**varchar(max)**|  
|`SQLVARCHAR`|예|**varchar(max)**|  
|`SQLBINARY`|예|**varbinary(max)**|  
|`SQLBIGBINARY`|예|**varbinary(max)**|  
|`SQLBIGVARBINARY`|예|**varbinary(max)**|  
|`SQLVARBINARY`|예|**varbinary(max)**|  
|`SQLNCHAR`|예|**nvarchar(max)**|  
|`SQLNVARCHAR`|예|**nvarchar(max)**|  
|`SQLXML`|예|**Xml**|  
|`SQLUDT`|모두|**udt**|  
  
## <a name="bcpgettypename-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 bcp_gettypename 지원  
 에 있는 테이블의 "sqlncli.h의 유형" 열에 날짜/시간 형식에 대 한 토큰 매개 변수 값을 설명 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB 및 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)합니다. 반환 값은 "파일 저장소 유형" 열의 해당 행에 있습니다.  
  
 자세한 내용은 참조 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대량 복사 함수](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  