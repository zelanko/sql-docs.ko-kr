---
description: 집계 함수, CALC 함수 및 NEW 키워드
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ad6bf4b041fbae0f30e327bd32dd067c1e9c429a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453755"
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>집계 함수, CALC 함수 및 NEW 키워드
데이터 셰이핑은 다음과 같은 기능을 지원 합니다. 작업할 열을 포함 하는 챕터에 할당 된 이름은 *챕터 별칭*입니다.  
  
 장-별칭은 정규화 할 수 있습니다. 각 챕터 열 이름은 *열 이름을* 포함 하는 챕터로 구분 되며 모두 마침표로 구분 됩니다. 예를 들어, 부모 챕터 chap1에 amount 열인 amt가 있는 자식 장 chap2이 포함 된 경우 정규화 된 이름은 chap1입니다.  
  
|집계 함수|설명|  
|-------------------------|-----------------|  
|합계 (*장-별칭** ) 열 이름*)|지정 된 열에 있는 모든 값의 합계를 계산 합니다.|  
|AVG (*장-별칭*).* 열 이름*)|지정 된 열에 있는 모든 값의 평균을 계산 합니다.|  
|최대 (*장-별칭** ) 열 이름*)|지정 된 열의 최대값을 계산 합니다.|  
|MIN (*장-별칭** ) 열 이름*)|지정 된 열의 최소값을 계산 합니다.|  
|개수 (*장-별칭*[.* 열 이름*])|지정 된 별칭의 행 수를 계산 합니다. 열을 지정 하면 해당 열이 Null이 아닌 행만 개수에 포함 됩니다.|  
|STDEV (*장-별칭** ) 열 이름*)|지정 된 열의 표준 편차를 계산 합니다.|  
|모든 (*장-별칭** ) 열 이름*)|지정 된 열의 값입니다. 모든 행에 대해 열 값이 같은 경우에만 예측 가능한 값이 있습니다.<br /><br /> **참고** 열이 챕터의 모든 행에 대해 동일한 값을 포함 하지 않는 경우 SHAPE 명령은 임의 함수의 값으로 값 중 하나를 임의로 반환 합니다.|  
  
|계산 식|설명|  
|---------------------------|-----------------|  
|CALC (*식*)|CALC 함수를 포함 하는 **레코드 집합** 의 행 에서만 임의의 식을 계산 합니다. 이러한 [Visual Basic for Applications (VBA) 함수](../../../ado/guide/data/visual-basic-for-applications-functions.md) 를 사용 하는 식은 허용 됩니다.|  
  
|NEW 키워드|설명|  
|-----------------|-----------------|  
|새 *필드 유형* [(*너비* &#124; *배율* &#124; *전체 자릿수* &#124; *오류* [, *크기 조정* &#124; *오류*])]|지정 된 형식의 빈 열을 **레코드 집합**에 추가 합니다.|  
  
 NEW 키워드와 함께 전달 되는 *필드 형식은* 다음 데이터 형식 중 하나일 수 있습니다.  
  
|OLE DB 데이터 형식|ADO 데이터 형식에 해당 하는 값|  
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
|DBTYPE_BYTES|adBinary, AdVarBinary, Adwvarbinary|  
|DBTYPE_STR|adChar, adVarChar, Adchar Varchar|  
|DBTYPE_WSTR|adWChar, adVarWChar, Adwvarwchar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 새 필드가 decimal 형식 (OLE DB, DBTYPE_DECIMAL 또는 ADO, adDecimal) 이면 전체 자릿수 및 소수 자릿수 값을 지정 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예](../../../ado/guide/data/data-shaping-example.md)   
 [공식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
