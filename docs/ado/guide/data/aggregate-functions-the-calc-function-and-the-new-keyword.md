---
title: "집계 함수, CALC 함수 및 NEW 키워드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], functions
- CALC function [ADO]
- NEW keyword [ADO]
- aggregate functions [ADO]
ms.assetid: 0590b466-2a36-49a2-868e-028ef5e49394
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aab522abece6300345819649380be206a277a456
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="aggregate-functions-the-calc-function-and-the-new-keyword"></a>집계 함수, CALC 함수 및 NEW 키워드
데이터 모양 지정 다음 기능을 지원 합니다. 작업을 수행할 열을 포함 하는 장에 할당 된 이름은 *장 별칭*합니다.  
  
 장 별칭 정규화를 포함 하는 장 각 장 열 이름으로 구성 된 수의 *열 이름* 모두 마침표로 분리 된 합니다. 예를 들어 chap1, 부모 장에서 자식 장, chap2, 포함 하에 amt amount 열 경우 정규화 된 이름이 chap1.chap2.amt 표시 됩니다.  
  
|집계 함수|Description|  
|-------------------------|-----------------|  
|SUM (*장 별칭*. *열 이름*)|지정 된 열의 모든 값의 합계를 계산합니다.|  
|AVG (*장 별칭*. *열 이름*)|지정 된 열의 모든 값의 평균을 계산합니다.|  
|MAX (*장 별칭*. *열 이름*)|지정 된 열의 최대값을 계산합니다.|  
|MIN (*장 별칭*. *열 이름*)|지정 된 열의 최소값을 계산합니다.|  
|COUNT (*장 별칭*[. *열 이름*])|지정된 된 별칭의 행 수를 계산합니다. 열을 지정 하는 경우를 해당 열이 Null이 아닌 행만 개수에 포함 됩니다.|  
|STDEV (*장 별칭*. *열 이름*)|지정 된 열의 표준 편차를 계산 합니다.|  
|모든 (*장 별칭*. *열 이름*)|지정 된 열의 값입니다. 모든 열의 값이 장에 있는 모든 행에 대해 동일 하 게 하는 경우에 예측 가능한 값을 갖습니다.<br /><br /> **참고** 장에 있는 행에 대해 동일한 값이 포함 되지 않은 열, SHAPE 명령 임의로 반환 ANY 함수의 값으로 값 중 하나입니다.|  
  
|계산 된 식|Description|  
|---------------------------|-----------------|  
|계산 (*식*)|행에만 임의의 식을 계산는 **레코드 집합** CALC 함수를 포함 하 합니다. 이 사용 하 여 모든 식 [VBA 함수에 대 한 Visual Basic](../../../ado/guide/data/visual-basic-for-applications-functions.md)|  
  
|NEW 키워드|Description|  
|-----------------|-----------------|  
|새 *필드 형식* [(*너비* &#124; *배율* &#124; *정밀도* &#124; *오류* [, *배율* &#124; *오류*])]|에 지정 된 형식의 빈 열에 추가 된 **레코드 집합**합니다.|  
  
 *필드 형식* 새 키워드와 함께 전달 된 다음 데이터 형식 중 하나가 될 수 있습니다.  
  
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
|DBTYPE_BYTES|adBinary 제외할 수, adLongVarBinary|  
|DBTYPE_STR|adChar, 집합이 있으므로, 필요 adLongVarChar|  
|DBTYPE_WSTR|adWChar, adVarWChar, adLongVarWChar|  
|DBTYPE_NUMERIC|adNumeric|  
|DBTYPE_DBDATE|adDBDate|  
|DBTYPE_DBTIME|adDBTime|  
|DBTYPE_DBTIMESTAMP|adDBTimeStamp|  
|DBTYPE_VARNUMERIC|adVarNumeric|  
|DBTYPE_FILETIME|adFileTime|  
|DBTYPE_ERROR|adError|  
  
 새 필드가 10 진수 형식은 (OLE DB DBTYPE_DECIMAL, 또는 ADO, adDecimal)의 경우 전체 자릿수 및 소수 자릿수 값을 지정 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 예제를 셰이핑](../../../ado/guide/data/data-shaping-example.md)   
 [형식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
