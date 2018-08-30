---
title: 향상된 날짜 및 시간 형식에 대한 대량 복사 변경 사항(OLE DB) | Microsoft Docs
description: 향상된 날짜 및 시간 형식에 대한 대량 복사 변경 사항(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, bulk copy operations
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 16ab7dd1f4a083c51108ef86ff9c9428df1649da
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029562"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db"></a>향상된 날짜 및 시간 형식에 대한 대량 복사 변경 사항(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 문서에서는 SQL Server 용 OLE DB 드라이버에서 대량 복사 기능을 지원 하기 위해 향상 된 날짜/시간 기능을 설명 합니다.  
  
## <a name="format-files"></a>서식 파일  
 서식 파일을 대화형으로 빌드할 경우 다음 표에서는 날짜/시간 형식을 지정하는 데 사용되는 입력 및 해당되는 호스트 파일 데이터 형식 이름을 보여 줍니다.  
  
|파일 저장 유형|호스트 파일 데이터 형식|메시지: "< field_name > 필드의 파일 저장 유형 입력 [\<기본 >]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|DATETIME|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|d|  
|date|SQLDATE|de|  
|Time|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 XML 서식 파일 XSD에는 다음과 같은 내용이 추가됩니다.  
  
```  
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>문자 데이터 파일  
 문자 데이터 파일의 날짜 및 시간 값의 "데이터 형식:: 문자열 및 리터럴" 섹션에 설명 된 대로 표시 됩니다 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) OLE DB에 대 한 합니다.  
  
 네이티브 데이터 파일의 경우 네 가지 새로운 형식의 날짜 및 시간 값은 해당되는 TDS 표현으로 표시되며 소수 자릿수는 7입니다. 소수 자릿수가 7인 이유는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 지원하는 최댓값이 7이고 bcp 데이터 파일에는 이러한 열의 소수 자릿수가 저장되지 않기 때문입니다. 기존의 **datetime** 및 **smalldatetime** 형식의 저장 방식 또는 이러한 형식의 TDS(Tabular Data Stream) 표현에는 변경 사항이 없습니다.  
  
 OLE DB의 경우 파일 저장 유형에 따른 저장 크기는 다음과 같습니다.  
  
|파일 저장 유형|저장 크기(바이트)|  
|-----------------------|---------------------------|  
|DATETIME|8|  
|smalldatetime|4|  
|날짜|3|  
|Time|6|  
|Datetime2|9|  
|Datetimeoffset|11|  
 
  
## <a name="bcp-types-in-msoledbsqlh"></a>Msoledbsql.h의 BCP 형식  
 형식은은 msoledbsql.h에 정의 됩니다. 이러한 형식을 사용 하 여 전달 되는 *eUserDataType* ibcpsession:: Bcpcolfmt OLE DB에서의 매개 변수입니다.  
  
|파일 저장 유형|호스트 파일 데이터 형식|Ibcpsession:: Bcpcolfmt 사용 msoledbsql.h 입력|값|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|DATETIME|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIM4|0x3a|  
|date|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Time|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>BCP 데이터 형식 변환  
 다음 표에서는 변환 정보를 보여 줍니다.  
  
 **OLE DB 참고 사항** 다음 변환은 IBCPSession에 의해 수행됩니다. IRowsetFastLoad에 정의 된 대로 OLE DB 변환을 사용 하 여 [변환은 클라이언트에서 서버로 수행](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md)합니다. datetime 값은 1/300초로 반올림되며 smalldatetime 값은 아래에 설명된 클라이언트 변환이 수행된 후 0초로 설정됩니다. datetime 반올림은 시간 및 분까지만 전파되고 날짜에는 전파되지 않습니다.  
  
|To --><br /><br /> 보낸 사람|날짜|Time|Smalldatetime|Datetime|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|date|@shouldalert|-|1, 6|1, 6|1, 6|1, 5, 6|1, 3|1, 3|  
|Time|해당 사항 없음|1, 10|1, 7, 10|1, 7, 10|1, 7, 10|1, 5, 7, 10|1, 3|1, 3|  
|Smalldatetime|1, 2|1, 4, 10|@shouldalert|@shouldalert|1, 10|1, 5, 10|1, 11|1, 11|  
|DATETIME|1, 2|1, 4, 10|1, 12|@shouldalert|1, 10|1, 5, 10|1, 11|1, 11|  
|Datetime2|1, 2|1, 4, 10|1, 12|1, 10|1, 10|1, 5, 10|1, 3|1, 3|  
|Datetimeoffset|1, 2, 8|1, 4, 8, 10|1, 8, 10|1, 8, 10|1, 8, 10|1, 10|1, 3|1, 3|  
|Char/wchar(date)|9|-|9, 6, 12|9, 6, 12|9, 6|9, 5, 6|해당 사항 없음|해당 사항 없음|  
|Char/wchar(time)|-|9, 10|9, 7, 10, 12|9, 7, 10, 12|9, 7, 10|9, 5, 7, 10|해당 사항 없음|해당 사항 없음|  
|Char/wchar(datetime)|9, 2|9, 4, 10|9, 10, 12|9, 10, 12|9, 10|9, 5, 10|해당 사항 없음|해당 사항 없음|  
|Char/wchar(datetimeoffset)|9, 2, 8|9, 4, 8, 10|9, 8, 10, 12|9, 8, 10, 12|9, 8, 10|9, 10|해당 사항 없음|해당 사항 없음|  
  
#### <a name="key-to-symbols"></a>기호 설명  
  
|기호|의미|  
|------------|-------------|  
|-|변환이 지원되지 않습니다.<br />|  
|@shouldalert|제공 된 데이터가 올바르지 않으면 오류가 게시 됩니다. datetimeoffset 값에서 시간 부분은 UTC 변환이 요청되지 않았더라도 UTC로 변환된 후의 범위 안에 포함되어야 합니다. 이는 TDS와 서버에서는 UTC에 맞게 datetimeoffset 값의 시간을 항상 정규화하기 때문입니다. 따라서 클라이언트에서는 UTC로의 변환 후 시간 구성 요소가 지원 범위에 포함되는지 확인해야 합니다.|  
|2|시간 구성 요소가 무시됩니다.|  
|3|잘림을 수행하여 데이터 손실이 발생하면 오류가 게시됩니다. datetime2의 경우 소수 자릿수 초의 자릿수(소수 자릿수)는 다음 표를 기준으로 대상 열의 크기에 따라 결정됩니다. 테이블의 범위보다 열 크기가 큰 경우 소수 자릿수가 9인 것으로 간주됩니다. 이 변환은 소수 자릿수 초의 자릿수를 OLE DB에서 허용하는 최대값인 9자리까지 허용합니다.<br /><br /> **형식** : DBTIME2<br /><br /> **암시된 소수 자릿수 0** 8<br /><br /> **암시된 소수 자릿수 1..9** 1..9<br /><br /> <br /><br /> **형식** : DBTIMESTAMP<br /><br /> **암시된 소수 자릿수 0:** 19<br /><br /> **암시된 소수 자릿수 1..9:** 21..29<br /><br /> <br /><br /> **형식** : DBTIMESTAMPOFFSET<br /><br /> **암시된 소수 자릿수 0:** 26<br /><br /> **암시된 소수 자릿수 1..9:** 28..36|  
|4|날짜 구성 요소가 무시됩니다.|  
|5|표준 시간대가 UTC로 설정됩니다(예: 00:00).|  
|6|시간이 0으로 설정됩니다.|  
|7|날짜가 1900-01-01로 설정됩니다.|  
|8|표준 시간대 오프셋이 무시됩니다.|  
|9|첫 번째 문장 부호 문자 및 나머지 구성 요소가 있는지 여부에 따라 문자열이 date, datetime, datetimeoffset 또는 time 값으로 구문 분석된 후 변환됩니다. 그런 다음, 이 프로세스에서 발견된 원본 형식에 대한 규칙(이 문서의 마지막 부분에 있는 표 참조)에 따라 문자열이 대상 형식으로 변환됩니다. 오류 없이 제공 되는 데이터를 구문 분석할 수 없는 경우 또는 구성 요소 일부가 허용 범위를 벗어난 경우 또는 대상 형식 리터럴 형식에서 변환 작업 없이 있으면 오류가 게시 됩니다. Datetime 및 smalldatetime 매개 변수의 경우 연도가 이러한 형식 지원 범위 밖에 있는 경우 오류가 게시 됩니다.<br /><br /> datetimeoffset의 경우 값은 UTC 변환이 요청되지 않더라도 UTC로 변환된 후의 범위 안에 포함되어야 합니다. 왜냐하면 TDS와 서버는 항상 datetimeoffset 값의 시간을 UTC에 맞게 정규화하므로 클라이언트에서 UTC로의 변환 후 시간 구성 요소가 지원 범위에 포함되는지 확인해야 하기 때문입니다. 값을 지원 되는 UTC 범위 안에 없을 경우 오류가 게시 됩니다.|  
|10|잘림을 수행 하 여 데이터 손실이 발생 하는 경우에 서버 변환을 클라이언트에 대 한 오류가 게시 됩니다. 이 오류는 값이 서버에서 사용된 UTC 범위로 표현할 수 있는 범위 밖에 있는 경우에도 발생합니다. 서버에서 클라이언트로의 변환 시 초 또는 소수 자릿수 초 잘림이 발생하면 경고만 표시됩니다.|  
|11|잘림을 수행 하 여 데이터 손실이 발생 하는 경우에 서버 변환을 클라이언트에 대 한 오류가 게시 됩니다.|
|12|초는 0으로 설정되고 소수 자릿수 초는 삭제됩니다. 잘림 오류가 발생하지 않습니다.|  
|해당 사항 없음|기존 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 및 이전 동작이 유지됩니다.|  
  
## <a name="see-also"></a>참고 항목     
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
