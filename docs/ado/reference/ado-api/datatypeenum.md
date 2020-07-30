---
title: DataTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
author: rothja
ms.author: jroth
ms.openlocfilehash: 456b11972fcb9b7bb20ee07b58e36d2daa5cc0da
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242386"
---
# <a name="datatypeenum"></a>DataTypeEnum
[필드](../../../ado/reference/ado-api/field-object.md), [매개 변수](../../../ado/reference/ado-api/parameter-object.md)또는 [속성](../../../ado/reference/ado-api/property-object-ado.md)의 데이터 형식을 지정 합니다. 해당 OLE DB 형식 표시기는 다음 표의 설명 열에 괄호 안에 표시 됩니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|다른 데이터 형식의 배열을 나타내는 플래그 값으로, 항상 다른 데이터 형식 상수와 결합 됩니다. ADOX에는 적용 되지 않습니다.|  
|**adBigInt**|20|부호 있는 8 바이트 정수 (DBTYPE_I8)를 나타냅니다.|  
|**adBinary**|128|이진 값 (DBTYPE_BYTES)을 나타냅니다.|  
|**adBoolean**|11|**부울** 값 (DBTYPE_BOOL)을 나타냅니다.|  
|**adBSTR**|8|Null 종료 문자열 (유니코드) (DBTYPE_BSTR)을 나타냅니다.|  
|**adChapter**|136|자식 행 집합 (DBTYPE_HCHAPTER)의 행을 식별 하는 4 바이트 챕터 값을 나타냅니다.|  
|**adChar**|129|문자열 값 (DBTYPE_STR)을 나타냅니다.|  
|**adCurrency**|6|통화 값 (DBTYPE_CY)을 나타냅니다. Currency는 소수점 오른쪽에 네 자리가 있는 고정 소수점 숫자입니다. 1만으로 조정 된 8 바이트 부호 있는 정수에 저장 됩니다.|  
|**adDate**|7|날짜 값 (DBTYPE_DATE)을 나타냅니다. 날짜는 double로 저장 되 고,의 전체 부분은 12 월 1899 30 일 이후의 일 수이 고,의 소수 부분은 하루 중 분수입니다.|  
|**adDBDate**|133|날짜 값 (yyyymmdd) (DBTYPE_DBDATE)을 나타냅니다.|  
|**adDBTime**|134|시간 값 (hhmmss) (DBTYPE_DBTIME)을 나타냅니다.|  
|**adDBTimeStamp**|135|날짜/시간 스탬프 (yyyymmddhhmmss + billionths의 분수)를 나타냅니다 (DBTYPE_DBTIMESTAMP).|  
|**adDecimal**|14|고정 전체 자릿수와 소수 자릿수가 있는 정확한 숫자 값 (DBTYPE_DECIMAL)을 나타냅니다.|  
|**adDouble**|5|배정밀도 부동 소수점 값 (DBTYPE_R8)을 나타냅니다.|  
|**adEmpty**|0|값 (DBTYPE_EMPTY)을 지정 하지 않습니다.|  
|**adError**|10|32 비트 오류 코드 (DBTYPE_ERROR)를 나타냅니다.|  
|**adFileTime**|64|1601 (DBTYPE_FILETIME) 1 월 1 일 이후 100 나노초 간격의 수를 나타내는 64 비트 값을 나타냅니다.|  
|**adGUID**|72|GUID (globally unique identifier) (DBTYPE_GUID)를 나타냅니다.|  
|**adIDispatch**|9|COM 개체 (DBTYPE_IDISPATCH)의 **IDispatch** 인터페이스에 대 한 포인터를 나타냅니다.<br /><br /> **참고** 이 데이터 형식은 현재 ADO에서 지원 되지 않습니다. 사용 하면 예기치 않은 결과가 발생할 수 있습니다.|  
|**adInteger**|3|부호 있는 4 바이트 정수 (DBTYPE_I4)를 나타냅니다.|  
|**adIUnknown**|13|COM 개체 (DBTYPE_IUNKNOWN)의 **IUnknown** 인터페이스에 대 한 포인터를 나타냅니다.<br /><br /> **참고** 이 데이터 형식은 현재 ADO에서 지원 되지 않습니다. 사용 하면 예기치 않은 결과가 발생할 수 있습니다.|  
|**adLongVarBinary**|205|긴 이진 값을 나타냅니다.|  
|**adLongVarChar**|201|긴 문자열 값을 나타냅니다.|  
|**adLongVarWChar**|203|Long null로 끝나는 유니코드 문자열 값을 나타냅니다.|  
|**adNumeric**|131|고정 전체 자릿수와 소수 자릿수가 있는 정확한 숫자 값 (DBTYPE_NUMERIC)을 나타냅니다.|  
|**adPropVariant**|138|Automation PROPVARIANT (DBTYPE_PROP_VARIANT)를 나타냅니다.|  
|**adSingle**|4|단 정밀도 부동 소수점 값 (DBTYPE_R4)을 나타냅니다.|  
|**adSmallInt**|2|부호 있는 2 바이트 정수 (DBTYPE_I2)를 나타냅니다.|  
|**adTinyInt**|16|부호 있는 1 바이트 정수 (DBTYPE_I1)를 나타냅니다.|  
|**adUnsignedBigInt**|21|부호 없는 8 바이트 정수 (DBTYPE_UI8)를 나타냅니다.|  
|**adUnsignedInt**|19|부호 없는 4 바이트 정수 (DBTYPE_UI4)를 나타냅니다.|  
|**adUnsignedSmallInt**|18|부호 없는 2 바이트 정수 (DBTYPE_UI2)를 나타냅니다.|  
|**adUnsignedTinyInt**|17|부호 없는 1 바이트 정수 (DBTYPE_UI1)를 나타냅니다.|  
|**adUserDefined**|132|사용자 정의 변수 (DBTYPE_UDT)를 나타냅니다.|  
|**adVarBinary**|204|이진 값을 나타냅니다.|  
|**adVarChar**|200|문자열 값을 나타냅니다.|  
|**adVariant**|12|Automation **Variant** (DBTYPE_VARIANT)를 나타냅니다.<br /><br /> **참고** 이 데이터 형식은 현재 ADO에서 지원 되지 않습니다. 사용 하면 예기치 않은 결과가 발생할 수 있습니다.|  
|**adVarNumeric**|139|숫자 값을 나타냅니다.|  
|**adVarWChar**|202|Null로 끝나는 유니코드 문자열을 나타냅니다.|  
|**adWChar**|130|Null로 끝나는 유니코드 문자열 (DBTYPE_WSTR)을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums 타임 스탬프|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums.|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums UNSIGNEDBIGINT|  
|AdoEnums INT|  
|AdoEnums.|  
|AdoEnums UNSIGNEDTINYINT|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Append 메서드(ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
        [CreateParameter 메서드(ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [CreateRecordset 메서드(RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)  
        [Type 속성(ADO)](../../../ado/reference/ado-api/type-property-ado.md)  
    :::column-end:::
:::row-end:::
