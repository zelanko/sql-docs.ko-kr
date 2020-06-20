---
title: 클라이언트에서 서버로 수행되는 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], client to server
ms.assetid: 6bb24928-0f3e-4119-beda-cfd04a44a3eb
author: rothja
ms.author: jroth
ms.openlocfilehash: 33655f1a5cc704907753ac1ab7ce43020c22fb3e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85043874"
---
# <a name="conversions-performed-from-client-to-server"></a>클라이언트에서 서버로 수행되는 변환
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB로 작성한 클라이언트 애플리케이션과 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 간에 수행되는 날짜/시간 변환에 대해 설명합니다.  
  
## <a name="conversions"></a>변환  
 이 항목에서는 클라이언트에서 수행되는 변환에 대해 설명합니다. 클라이언트가 매개 변수에 지정한 소수 자릿수 초의 전체 자릿수가 서버에 정의된 것과 다르면 서버에서 작업을 허용하는 경우에 클라이언트 변환이 실패할 수 있습니다. 특히 클라이언트는 소수 자릿수 초 잘림을 모두 오류로 취급하는 반면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 시간 값을 가장 근사한 정수 초로 반올림합니다.  
  
 ICommandWithParameters:: SetParameterInfo를 호출 하지 않으면 DBTYPE_DBTIMESTAMP 바인딩이 인 것 처럼 변환 됩니다 `datetime2` .  
  
|대상 -><br /><br /> 시작|DBDATE(date)|DBTIME(time)|DBTIME2(time)|DBTIMESTAMP(smalldatetime)|DBTIMESTAMP(datetime)|DBTIMESTAMP(datetime2)|DBTIMESTAMPOFFSET(datetimeoffset)|STR|WSTR|SQLVARIANT<br /><br /> (sql_variant)|  
|----------------------|---------------------|---------------------|----------------------|-----------------------------------|------------------------------|-------------------------------|------------------------------------------|---------|----------|-------------------------------------|  
|DATE|1,2|1,3,4|4,12|1,12|1,12|1,12|1,5, 12|1,12|1,12|1,12<br /><br /> datetime2(0)|  
|DBDATE|1|-|-|1,6|1,6|1,6|1,5, 6|1,10|1,10|1<br /><br /> date|  
|DBTIME|-|1|1|1,7|1,7|1,7|1,5, 7|1,10|1,10|1<br /><br /> Time(0)|  
|DBTIME2|-|1,3|1|1,7,10,14|1,7,10,15|1,7,10|1,5,7,10|1,10,11|1,10,11|1<br /><br /> Time(7)|  
|DBTIMESTAMP|1,2|1,3,4|1,4,10|1,10,14|1,10,15|1,10|1,5,10|1,10,11|1,10,11|1,10<br /><br /> datetime2(7)|  
|DBTIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10,14|1,8,10,15|1,8,10|1,10|1,10,11|1,10,11|1,10<br /><br /> datetimeoffset(7)|  
|FILETIME|1,2|1,3,4|1,4,13|1,13|1,13|1,13|1,5,13|1,13|1,10|1,13<br /><br /> datetime2(3)|  
|BYTES|-|-|-|-|-|-|-|해당 없음|해당 없음|해당 없음|  
|VARIANT|1|1|1|1,10|1,10|1,10|1,10|해당 없음|해당 없음|1,10|  
|SSVARIANT|1,16|1,16|1,16|1,10,16|1,10,16|1,10,16|1,10,16|해당 없음|해당 없음|1,16|  
|BSTR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|해당 없음|해당 없음|해당 없음|  
|STR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|해당 없음|해당 없음|해당 없음|  
|WSTR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|해당 없음|해당 없음|해당 없음|  
  
## <a name="key-to-symbols"></a>기호 설명  
  
|기호|의미|  
|------------|-------------|  
|-|변환이 지원되지 않습니다. IAccessor::CreateAccessor가 호출될 때 바인딩의 유효성이 검사되면 *rgStatus*에 DBBINDSTATUS_UPSUPPORTEDCONVERSION이 반환됩니다. 접근자 유효성 검사가 지연되면 DBSTATUS_E_BADACCESSOR가 설정됩니다.|  
|해당 없음|해당 사항 없음|  
|1|지정한 데이터가 유효하지 않으면 DBSTATUS_E_CANTCONVERTVALUE가 설정됩니다. 입력 데이터는 변환이 적용되기 전에 유효성이 검사되므로 이후 변환에서 구성 요소를 무시하더라도 계속 유효해야 변환에 성공할 수 있습니다.|  
|2|시간 필드가 무시됩니다.|  
|3|소수 자릿수 초가 0이어야 하며 그렇지 않으면 DBSTATUS_E_DATAOVERFLOW가 설정됩니다.|  
|4|날짜 구성 요소가 무시됩니다.|  
|5|표준 시간대가 클라이언트의 표준 시간대 설정으로 지정됩니다.|  
|6|시간이 0으로 설정됩니다.|  
|7|날짜가 현재 날짜로 설정됩니다.|  
|8|시간이 UTC로 변환됩니다. 이 변환이 수행되는 동안 오류가 발생하면 DBSTATUS_E_CANTCONVERTVALUE가 설정됩니다.|  
|9|문자열이 ISO 리터럴로 구문 분석되고 대상 형식으로 변환됩니다. 실패하면 문자열이 OLE 날짜 리터럴(여기에도 시간 구성 요소가 포함되어 있음)로 구문 분석되고 OLE 날짜(DBTYPE_DATE)에서 대상 형식으로 변환됩니다.<br /><br /> 대상 유형이 DBTIMESTAMP, `smalldatetime`, `datetime` 또는 `datetime2`인 경우 문자열은 날짜, 시간 또는 `datetime2` 리터럴 구문 또는 OLE에서 인식할 수 있는 구문을 준수해야 합니다. 문자열이 날짜 리터럴인 경우 모든 시간 구성 요소는 0으로 설정됩니다. 문자열이 시간 리터럴인 경우 날짜는 현재 날짜로 설정됩니다.<br /><br /> 다른 모든 대상 유형의 경우 문자열은 대상 유형의 리터럴 구문을 준수해야 합니다.|  
|10|데이터 손실을 유발하는 소수 자릿수 초 잘림이 발생하면 DBSTATUS_E_DATAOVERFLOW가 설정됩니다. 문자열 변환의 경우 문자열이 ISO 구문을 준수하는 경우에만 오버플로 검사가 가능합니다. 문자열이 OLE 날짜 리터럴인 경우에는 소수 자릿수 초가 반올림됩니다.<br /><br /> DBTIMESTAMP(datetime)에서 smalldatetime으로 변환하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서는 DBSTATUS_E_DATAOVERFLOW 오류를 발생시키는 대신 초 값을 자동으로 자릅니다.|  
|11|소수 자릿수 초의 자릿수(소수 자릿수)는 다음 표를 기준으로 대상 열의 크기에 따라 결정됩니다. 테이블의 범위보다 열 크기가 큰 경우 소수 자릿수가 9인 것으로 간주됩니다. 이 변환은 소수 자릿수 초의 자릿수를 OLE DB에서 허용하는 최대값인 9자리까지 허용합니다.<br /><br /> 그러나 원본 형식이 DBTIMESTAMP이고 소수 자릿수 초가 0인 경우에는 소수 자릿수 초의 자릿수 또는 소수점이 생성되지 않습니다. 이 동작은 이전 OLE DB 공급자를 사용하여 개발된 애플리케이션과의 호환성을 보장합니다.<br /><br /> 열 크기가 ~0이면 OLE DB에 크기 제한이 없음을 나타냅니다(DBTIMESTAMP의 3자리 규칙이 적용되지 않는 경우 9자리).<br /><br /> **DBTIME2** - 8, 10..18 (문자에서 길이); 0, 1..9 (배율)<br /><br /> **DBTIMESTAMP** - 19, 21..29 (문자에서 길이); 0, 1..9 (배율)<br /><br /> **DBTIMESTAMPOFFSET** - 26, 28..36 (문자에서 길이); 0, 1..9 (배율)|  
|12|DBTYPE_DATE에 대한 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전의 변환 의미가 유지됩니다. 소수 자릿수 초는 0으로 잘립니다.|  
|13|DBTYPE_FILETIME에 대한 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전의 변환 의미가 유지됩니다. Windows FileTimeToSystemTime API를 사용하는 경우 소수 자릿수 초의 전체 자릿수는 1밀리초로 제한됩니다.|  
|14|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에 대한 `smalldatetime` 이전의 변환 의미가 유지됩니다. 초는 0으로 설정됩니다.|  
|15|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에 대한 `datetime` 이전의 변환 의미가 유지됩니다. 초는 가장 근사한 300초로 반올림됩니다.|  
|16|SSVARIANT 클라이언트 구조에 포함된 값(지정된 형식)의 변환 동작은 SSVARIANT 클라이언트 구조에 포함되지 않은 동일한 값 및 형식의 동작과 같습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [바인딩 및 변환&#40;OLE DB&#41;](conversions-ole-db.md)  
  
  
