---
title: 서버에서 클라이언트로 수행되는 변환 | Microsoft Docs
description: 서버에서 클라이언트로 수행되는 변환
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], server to client
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 22f3b681f9c4256087c17bd1e74011c2ba0916fe
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015811"
---
# <a name="conversions-performed-from-server-to-client"></a>서버에서 클라이언트로 수행되는 변환
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 문서에서는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상과 SQL Server 용 OLE DB 드라이버를 사용하여 작성된 클라이언트 애플리케이션 간에 수행되는 날짜/시간 변환에 대해 설명합니다.  
  
## <a name="conversions"></a>변환  
 다음 표에서는 클라이언트로 반환된 형식과 바인딩 형식 간의 변환에 대해 설명합니다. 출력 매개 변수의 경우 ICommandWithParameters::SetParameterInfo가 호출된 후 *pwszDataSourceType*에 지정된 형식이 서버의 실제 형식과 일치하지 않으면 서버에 의해 암시적 변환이 수행되며 클라이언트로 반환되는 형식은 ICommandWithParameters::SetParameterInfo를 통해 지정된 형식과 일치하게 됩니다. 따라서 서버의 변환 규칙이 이 문서에서 설명된 내용과 다를 경우 예기치 못한 변환 결과가 나타날 수 있습니다. 예를 들어 기본 날짜를 입력해야 하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 1899-12-30을 사용하지 않고, 1900-1-1을 사용합니다.  
  
|대상 -><br /><br /> 보낸 사람|DATE|DBDATE|DBTIME|DBTIME2|DBTIMESTAMP|DBTIMESTAMPOFFSET|FILETIME|BYTES|VARIANT|SSVARIANT|BSTR|STR|WSTR|  
|----------------------|----------|------------|------------|-------------|-----------------|-----------------------|--------------|-----------|-------------|---------------|----------|---------|----------|  
|Date|1, 7|확인|-|-|1|1, 3|1, 7|-|OK(VT_BSTR)|확인|확인|4|4|  
|Time|5, 6, 7|-|9|확인|6|3, 6|5, 6|-|OK(VT_BSTR)|확인|확인|4|4|  
|Smalldatetime|7|8|9, 10|10|확인|3|7|-|7(VT_DATE)|확인|확인|4|4|  
|DateTime|5, 7|8|9, 10|10|확인|3|7|-|7(VT_DATE)|확인|확인|4|4|  
|Datetime2|5, 7|8|9, 10|10|7|3|5, 7|-|OK(VT_BSTR)|확인|확인|4|4|  
|Datetimeoffset|5, 7, 11|8, 11|9, 10, 11|10, 11|7, 11|확인|5, 7, 11|-|OK(VT_BSTR)|확인|확인|4|4|  
|Char, Varchar,<br /><br /> Nchar, Nvarchar|7, 13|12|12, 9|12|12|12|7, 13|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|  
|Sql_variant<br /><br /> (datetime)|7|8|9, 10|10|확인|3|7|-|7(VT_DATE)|확인|확인|4|4|  
|Sql_variant<br /><br /> (smalldatetime)|7|8|9, 10|10|확인|3|7|-|7(VT_DATE)|확인|확인|4|4|  
|Sql_variant<br /><br /> (date)|1, 7|확인|2|2|1|1, 3|1, 7|-|가능(VT_BSTR)|확인|확인|4|4|  
|Sql_variant<br /><br /> (time)|5, 6, 7|2|6|확인|6|3, 6|5, 6|-|가능(VT_BSTR)|확인|확인|4|4|  
|Sql_variant<br /><br /> (datetime2)|5, 7|8|9, 10|10|확인|3|5, 7|-|가능(VT_BSTR)|확인|확인|4|4|  
|Sql_variant<br /><br /> (datetimeoffset)|5, 7, 11|8, 11|9, 10, 11|10, 11|7, 11|확인|5, 7, 11|-|가능(VT_BSTR)|확인|확인|4|4|  
  
## <a name="key-to-symbols"></a>기호 설명  
  
|기호|의미|  
|------------|-------------|  
|확인|변환이 필요 없습니다.|  
|-|변환이 지원되지 않습니다. IAccessor::CreateAccessor가 호출될 때 바인딩의 유효성이 검사되면 *rgStatus*에 DBBINDSTATUS_UPSUPPORTEDCONVERSION이 반환됩니다. 접근자 유효성 검사가 지연되면 DBSTATUS_E_BADACCESSOR가 설정됩니다.|  
|1|시간 필드가 0으로 설정됩니다.|  
|2|DBSTATUS_E_CANTCONVERTVALUE가 설정됩니다.|  
|3|표준 시간대가 0으로 설정됩니다.|  
|4|클라이언트 버퍼의 크기가 충분하지 않으면 DBSTATUS_S_TRUNCATED가 설정됩니다. 서버 형식에 소수 자릿수 초가 있는 경우 결과 문자열의 자릿수는 서버 형식의 소수 자릿수와 정확하게 일치합니다.|  
|5|초 잘림 또는 소수 자릿수 초가 무시됩니다.|  
|6|원본이 문자열 시간 리터럴이 아니고 대상이 DBTYPE_DATE가 아닌 경우 날짜는 현재 날짜로 설정됩니다. 이 경우에는 1899-12-30이 사용됩니다.|  
|7|값이 오버플로되면 DBSTATUS_E_DATAOVERFLOW가 설정됩니다.|  
|8|시간 필드가 무시됩니다.|  
|9|소수 자릿수 초 필드가 무시됩니다.|  
|10|날짜 구성 요소가 무시됩니다.|  
|11|시간이 클라이언트 표준 시간대로 변환됩니다. 이 변환을 수행하는 동안 오류가 발생하면 DBSTATUS_E_DATAOVERFLOW가 설정됩니다.|  
|12|문자열이 ISO 리터럴로 구문 분석되고 대상 형식으로 변환됩니다. 실패하면 문자열이 OLE 날짜 리터럴(여기에도 시간 구성 요소가 포함되어 있음)로 구문 분석되고 OLE 날짜(DBTYPE_DATE)에서 대상 형식으로 변환됩니다. 문자열은 대상 유형의 ISO 형식 구문 분석이 성공할 수 있도록 리터럴 구문을 준수해야 합니다. OLE 구문 분석이 성공하려면 문자열이 OLE가 인식할 수 있는 구문을 준수해야 합니다. 문자열을 구문 분석할 수 없는 경우 DBSTATUS_E_CANTCONVERTVALUE가 설정됩니다. 범위를 벗어나는 구성 요소 값이 있으면 DBSTATUS_E_DATAOVERFLOW가 설정됩니다.|  
|13|문자열이 ISO 리터럴로 구문 분석되고 대상 형식으로 변환됩니다. 실패하면 문자열이 OLE 날짜 리터럴(여기에도 시간 구성 요소가 포함되어 있음)로 구문 분석되고 OLE 날짜(DBTYPE_DATE)에서 대상 형식으로 변환됩니다. 대상이 DBTYPE_DATE 또는 DBTYPE_DBTIMESTAMP가 아닌 경우 문자열은 날짜/시간 리터럴 구문을 준수해야 합니다. 이 경우에 ISO 형식 구문 분석이 성공하려면 날짜/시간 또는 시간 리터럴이 사용되어야 합니다. OLE 구문 분석이 성공하려면 문자열이 OLE가 인식할 수 있는 구문을 준수해야 합니다. 문자열을 구문 분석할 수 없는 경우 DBSTATUS_E_CANTCONVERTVALUE가 설정됩니다. 범위를 벗어나는 구성 요소 값이 있으면 DBSTATUS_E_DATAOVERFLOW가 설정됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [바인딩 및 변환&#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
  
  
