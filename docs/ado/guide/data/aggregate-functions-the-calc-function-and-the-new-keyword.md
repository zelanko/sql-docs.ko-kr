---
title: 집계 함수, CALC 함수 및 NEW 키워드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76fbb95117b1aae982242f24dc2cb1e815bc2356
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063099"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>집계 함수, CALC 함수 및 NEW 키워드
데이터 모양 지정은 다음 함수를 지원 합니다. 작업을 수행할 열이 포함 된 장 할당 이름은 합니다 *장-별칭*합니다.  
  
 장-별칭을 정규화를 포함 하는 장 각 장 열 이름으로 이루어진 수는 *열 이름,* 마침표로 구분 된 모든 합니다. 예를 들어 chap1, 부모 장에서 자식 장에서 chap2, 포함 된 경우 amt amount 열도 포함 다음 정규화 된 이름이 chap1.chap2.amt 표시 됩니다.  
  
|집계 함수|Description|  
|-------------------------|-----------------|  
|SUM (*장-별칭*. *열 이름*)|지정 된 열의 모든 값의 합계를 계산합니다.|  
|AVG (*장-별칭*. *열 이름*)|지정 된 열의 모든 값의 평균을 계산 합니다.|  
|최대 (*장-별칭*. *열 이름*)|지정 된 열의 최대값을 계산합니다.|  
|MIN (*장-별칭*. *열 이름*)|지정 된 열의 최소값을 계산합니다.|  
|COUNT(*chapter-alias*[.*column-name*])|지정된 된 별칭의 행 수를 셉니다. 에 지정 된 개수에는 해당 열이 Null이 아닌 행만 포함 됩니다.|  
|STDEV(*chapter-alias*.*column-name*)|지정 된 열의 표준 편차를 계산 합니다.|  
|모든 (*장-별칭*. *열 이름*)|지정 된 열의 값입니다. 모든 열의 값이 챕터의 모든 행에 대해 동일 하 게 하는 경우에 예측 가능한 값이 있습니다.<br /><br /> **참고** 열 챕터에 행에 대해 동일한 값이 없는 경우 SHAPE 명령 하나를 임의로 반환 값과 모든 함수의 값입니다.|  
  
|계산된 식|Description|  
|---------------------------|-----------------|  
|CALC(*expression*)|행에만 임의의 식을 계산 합니다 **레코드 집합** CALC 함수를 포함 하 합니다. 이 사용 하 여 모든 식 [VBA 함수에 대 한 Visual Basic](../../../ado/guide/data/visual-basic-for-applications-functions.md)|  
  
|새 키워드|Description|  
|-----------------|-----------------|  
|NEW *field-type* [(*width* &#124; *scale* &#124; *precision* &#124; *error* [, *scale* &#124; *error*])]|지정 된 형식의 빈 열을 추가 합니다 **레코드 집합**합니다.|  
  
 합니다 *필드 형식* NEW 키워드를 사용 하 여 전달 된 다음 데이터 형식 중 하나가 될 수 있습니다.  
  
|OLE DB 데이터 형식|ADO 데이터 상응 하는 형식|  
|-----------------------|-----------------------------------|  
|DBTYPE_BSTR|adBSTR|  
|DBTYPE_BOOL|adBoolean|  
|DBTYPE_DECIMAL|adDecimal|  
|DBTYPE_UI1|adUnsignedTinyInt|  
|DBTYPE_I1|adTinyInt|  
|DBTYPE_UI2|adUnsignedSmallInt|  
|DBTYPE_UI4|adUnsignedInt|  
|DBTYPE_I8|adBigInt|  
|DBTYPE_UI8|adUnsignedBigInt|  
|DBTYPE_GUID|adGuid|  
|DBTYPE_BYTES|adBinary, AdVarBinary, adLongVarBinary|  
|DBTYPE_STR|adChar, adVarChar, adLongVarChar|  
|DBTYPE_WSTR|adWChar, adVarWChar, adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 새 필드 (OLE DB DBTYPE_DECIMAL, 또는 ADO를 adDecimal) 10 진수 형식의 경우 전체 자릿수 및 소수 자릿수 값을 지정 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)   
 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
