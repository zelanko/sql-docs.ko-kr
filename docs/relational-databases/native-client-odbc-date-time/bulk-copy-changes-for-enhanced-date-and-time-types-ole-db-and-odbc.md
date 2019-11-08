---
title: 향상 된 날짜 및 시간 형식 (OLE DB 및 ODBC)의 대량 복사 변경 내용 Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, bulk copy operations
ms.assetid: c29e0f5e-9b3c-42b3-9856-755f4510832f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6900a021c7ccb2fcc146265bef54f1358f0319cf
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784072"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc"></a>향상된 날짜 및 시간 형식에 대한 대량 복사 변경 사항(OLE DB 및 ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 항목에서는 대량 복사 기능을 지원하기 위한 날짜/시간 개선 사항에 대해 설명합니다. 이 항목의 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client의 OLE DB 및 ODBC 둘 모두에 적용됩니다.  
  
## <a name="format-files"></a>서식 파일  
 서식 파일을 대화형으로 빌드할 경우 다음 표에서는 날짜/시간 형식을 지정하는 데 사용되는 입력 및 해당되는 호스트 파일 데이터 형식 이름을 보여 줍니다.  
  
|파일 스토리지 유형|호스트 파일 데이터 형식|프롬프트에 대 한 응답: "필드의 파일 저장 유형 입력 < field_name > [\<default >]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|날짜/시간|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|날짜|SQLDATE|de|  
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
 문자 데이터 파일에서 날짜 및 시간 값은 odbc의 [Odbc 날짜 및 시간 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md) 또는 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원의 "데이터 형식: 문자열 및 리터럴" 섹션에 설명 된 대로 표시 됩니다. ](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)OLE DB입니다.  
  
 네이티브 데이터 파일의 경우 네 가지 새로운 형식의 날짜 및 시간 값은 해당되는 TDS 표현으로 표시되며 최대 소수 자릿수는 7입니다. 소수 자릿수가 7인 이유는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 지원되는 최대 값이 7이고 bcp 데이터 파일에는 이러한 열의 소수 자릿수가 저장되지 않기 때문입니다. 기존의 **datetime** 및 **smalldatetime** 형식의 스토리지 방식 또는 이러한 형식의 TDS(Tabular Data Stream) 표현에는 변경 사항이 없습니다.  
  
 OLE DB의 경우 파일 스토리지 유형에 따른 스토리지 크기는 다음과 같습니다.  
  
|파일 스토리지 유형|스토리지 크기(바이트)|  
|-----------------------|---------------------------|  
|datetime|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
  
 ODBC의 경우에는 크기가 다음과 같습니다. 이 경우 BCP.exe가 서버에서 전체 자릿수를 항상 가져오기 때문에 서식 또는 데이터 파일에 전체 자릿수를 저장할 필요가 없습니다.  
  
|파일 스토리지 유형|스토리지 크기(바이트)|스토리지 형식|  
|-----------------------|---------------------------|--------------------|  
|datetime(d)|8|TDS|  
|smalldatetime(D)|4|TDS|  
|date(de)|3|TDS|  
|time(te)|6|TDS|  
|datetime2(d2)|9|TDS|  
|datetimeoffset(do)|11|TDS|  
  
## <a name="bcp-types-in-sqlnclih"></a>sqlncli.h의 BCP 형식  
 다음 형식은 ODBC에 대한 BCP API 확장에 사용할 수 있도록 sqlncli.h에 정의됩니다. 이러한 형식은 OLE DB에서 IBCPSession:: BCPColFmt의 *Euserdatatype* 매개 변수와 함께 전달 됩니다.  
  
|파일 스토리지 유형|호스트 파일 데이터 형식|IBCPSession:: BCPColFmt에 사용할 sqlncli을 입력 합니다.|값|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|날짜/시간|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIME4|0x3a|  
|날짜|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Time|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>BCP 데이터 형식 변환  
 다음 표에서는 변환 정보를 보여 줍니다.  
  
 **OLE DB 참고 사항** 다음 변환은 IBCPSession에 의해 수행됩니다. IRowsetFastLoad는 [클라이언트에서 서버로 수행](../../relational-databases/native-client-ole-db-date-time/conversions-performed-from-client-to-server.md)되는 변환에 정의 된 대로 OLE DB 변환을 사용 합니다. datetime 값은 1/300초로 반올림되며 smalldatetime 값은 아래에 설명된 클라이언트 변환이 수행된 후 0초로 설정됩니다. datetime 반올림은 시간 및 분까지만 전파되고 날짜에는 전파되지 않습니다.  
  
|대상 --><br /><br /> 원본|date|time|smalldatetime|datetime|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|날짜|1\.|-|1,6|1,6|1,6|1,5,6|1,3|1,3|  
|Time|해당 사항 없음|1,10|1,7,10|1,7,10|1,7,10|1,5,7,10|1,3|1,3|  
|Smalldatetime|1,2|1,4,10|1\.|1\.|1,10|1,5,10|1,11|1,11|  
|날짜/시간|1,2|1,4,10|1,12|1\.|1,10|1,5,10|1,11|1,11|  
|Datetime2|1,2|1,4,10|1,10(ODBC)1,12(OLE DB)|1,10|1,10|1,5,10|1,3|1,3|  
|Datetimeoffset|1,2,8|1,4,8,10|1,8,10|1,8,10|1,8,10|1,10|1,3|1,3|  
|Char/wchar(date)|9|-|9,6(ODBC)9,6,12(OLE DB)|9,6(ODBC)9,6,12(OLE DB)|9,6|9,5,6|해당 사항 없음|해당 사항 없음|  
|Char/wchar(time)|-|9,10|9,7,10(ODBC)9,7,10,12(OLE DB)|9,7,10(ODBC)9,7,10,12(OLE DB)|9,7,10|9,5,7,10|해당 사항 없음|해당 사항 없음|  
|Char/wchar(datetime)|9,2|9,4,10|9,10(ODBC)9,10,12(OLE DB)|9,10(ODBC)9,10,12(OLE DB)|9,10|9,5,10|해당 사항 없음|해당 사항 없음|  
|Char/wchar(datetimeoffset)|9,2,8|9,4,8,10|9,8,10(ODBC)9,8,10,12(OLE DB)|9,8,10(ODBC)9,8,10,12(OLE DB)|9,8,10|9,10|해당 사항 없음|해당 사항 없음|  
  
#### <a name="key-to-symbols"></a>기호 설명  
  
|기호|의미|  
|------------|-------------|  
|-|변환이 지원되지 않습니다.<br /><br /> SQLSTATE 07006 및 "제한된 데이터 형식 특성을 위반했습니다."라는 메시지가 포함된 ODBC 진단 레코드가 생성됩니다.|  
|1\.|제공된 데이터가 유효하지 않으면 SQLSTATE 22007 및 "잘못된 날짜 시간 형식입니다."라는 메시지가 포함된 ODBC 진단 레코드가 생성됩니다. datetimeoffset 값에서 시간 부분은 UTC 변환이 요청되지 않았더라도 UTC로 변환된 후의 범위 안에 포함되어야 합니다. 이는 TDS와 서버에서는 UTC에 맞게 datetimeoffset 값의 시간을 항상 정규화하기 때문입니다. 따라서 클라이언트에서는 UTC로의 변환 후 시간 구성 요소가 지원 범위에 포함되는지 확인해야 합니다.|  
|2|시간 구성 요소가 무시됩니다.|  
|3|ODBC의 경우 데이터 손실이 있는 잘림이 발생 하면 SQLSTATE 22001 및 메시지의 문자열 데이터를 사용 하 여 진단 레코드가 생성 되 고, 오른쪽으로 잘린 ' 소수 자릿수 초의 자릿수 (소수 자릿수)는 다음에 따라 대상 열의 크기에 따라 결정 됩니다. 다음 표 테이블의 범위보다 열 크기가 큰 경우 소수 자릿수가 7인 것으로 간주됩니다. 이 변환은 소수 자릿수 초의 자릿수를 ODBC에서 허용하는 최대값인 9자리까지 허용합니다.<br /><br /> **형식** : DBTIME2<br /><br /> **암시된 소수 자릿수 0** 8<br /><br /> **암시된 소수 자릿수 1..7** 10,16<br /><br /> <br /><br /> **형식** : DBTIMESTAMP<br /><br /> **암시된 소수 자릿수 0:** 19<br /><br /> **암시된 소수 자릿수 1..7:** 21..27<br /><br /> <br /><br /> **형식** : DBTIMESTAMPOFFSET<br /><br /> **암시된 소수 자릿수 0:** 26<br /><br /> **암시된 소수 자릿수 1..7:** 28..34<br /><br /> OLE DB의 경우 잘림을 수행하여 데이터 손실이 발생하면 오류가 게시됩니다. datetime2의 경우 소수 자릿수 초의 자릿수(소수 자릿수)는 다음 표를 기준으로 대상 열의 크기에 따라 결정됩니다. 테이블의 범위보다 열 크기가 큰 경우 소수 자릿수가 9인 것으로 간주됩니다. 이 변환은 소수 자릿수 초의 자릿수를 OLE DB에서 허용하는 최대값인 9자리까지 허용합니다.<br /><br /> **형식** : DBTIME2<br /><br /> **암시된 소수 자릿수 0** 8<br /><br /> **암시된 소수 자릿수 1..9** 1..9<br /><br /> <br /><br /> **형식** : DBTIMESTAMP<br /><br /> **암시된 소수 자릿수 0:** 19<br /><br /> **암시된 소수 자릿수 1..9:** 21..29<br /><br /> <br /><br /> **형식** : DBTIMESTAMPOFFSET<br /><br /> **암시된 소수 자릿수 0:** 26<br /><br /> **암시된 소수 자릿수 1..9:** 28..36|  
|4|날짜 구성 요소가 무시됩니다.|  
|5|표준 시간대가 UTC로 설정됩니다(예: 00:00).|  
|6|시간이 0으로 설정됩니다.|  
|7|날짜가 1900-01-01로 설정됩니다.|  
|8|표준 시간대 오프셋이 무시됩니다.|  
|9|첫 번째 문장 부호 문자 및 나머지 구성 요소가 있는지 여부에 따라 문자열이 date, datetime, datetimeoffset 또는 time 값으로 구문 분석된 후 변환됩니다. 그런 다음 이 프로세스에서 발견된 원본 형식에 대한 규칙(이 항목의 마지막 부분에 있는 표 참조)에 따라 문자열이 대상 형식으로 변환됩니다. 제공된 데이터를 오류 없이 구문 분석할 수 없거나, 구성 요소 중 하나라도 허용 범위 밖에 있거나, 리터럴 형식에서 대상 형식으로의 변환이 없으면, 오류가 게시되거나(OLE DB) SQLSTATE 22018 및 "캐스트 사양의 문자 값이 올바르지 않습니다."라는 메시지가 포함된 ODBC 진단 레코드가 생성됩니다. datetime 및 smalldatetime 매개 변수의 경우 연도가 이러한 형식에서 지원하는 범위 밖에 있으면 오류가 게시되거나(OLE DB), SQLSATE 22007 및 "잘못된 날짜 시간 형식입니다."라는 메시지가 포함된 ODBC 진단 레코드가 생성됩니다.<br /><br /> datetimeoffset의 경우 값은 UTC 변환이 요청되지 않더라도 UTC로 변환된 후의 범위 안에 포함되어야 합니다. 왜냐하면 TDS와 서버는 항상 datetimeoffset 값의 시간을 UTC에 맞게 정규화하므로 클라이언트에서 UTC로의 변환 후 시간 구성 요소가 지원 범위에 포함되는지 확인해야 하기 때문입니다. 값이 지원되는 UTC 범위에 포함되지 않으면 오류가 게시되거나(OLE DB), SQLSTATE 22007 및 "잘못된 날짜 시간 형식입니다."라는 메시지가 포함된 ODBC 진단 레코드가 생성됩니다.|  
|10|클라이언트에서 서버로의 변환 시 잘림을 수행하여 데이터 손실이 발생하면 오류가 게시되거나(OLE DB), SQLSTATE 22008 및 "Datetime 필드 오버플로"라는 메시지가 포함된 ODBC 진단 레코드가 생성됩니다. 이 오류는 값이 서버에서 사용된 UTC 범위로 표현할 수 있는 범위 밖에 있는 경우에도 발생합니다. 서버에서 클라이언트로의 변환 시 초 또는 소수 자릿수 초 잘림이 발생하면 경고만 표시됩니다.|  
|11|잘림을 수행하여 데이터 손실이 발생하면 진단 레코드가 생성됩니다.<br /><br /> 서버에서 클라이언트로 변환할 경우에는 경고(ODBC SQLSTATE S1000)입니다.<br /><br /> 클라이언트에서 서버로 변환할 경우에는 오류(ODBC SQLSTATE 22001)입니다.|  
|12|초는 0으로 설정되고 소수 자릿수 초는 삭제됩니다. 잘림 오류가 발생하지 않습니다.|  
|해당 사항 없음|기존 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 이전 동작이 유지됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 ODBC 의 [날짜 및 시간 기능 향상 &#40;&#41; ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
