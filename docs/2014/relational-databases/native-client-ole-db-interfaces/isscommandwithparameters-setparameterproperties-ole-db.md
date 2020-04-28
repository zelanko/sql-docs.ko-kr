---
title: ISSCommandWithParameters::SetParameterProperties(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 778021ce007f0c1eac68197e0c07e2cb7b0bb001
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62638773"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties(OLE DB)
  매개 변수별 서수로 매개 변수 속성을 설정하거나, SSPARAMPROPS 구조의 배열을 지정하여 대량 매개 변수 속성을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT SetParameterProperties(  
DB_UPARAMS cParams,   
SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>인수  
 *cParams*[in]  
 *rgParamProperties* 배열의 SSPARAMPROPS 구조 수입니다. 이 숫자가 0 이면는 명령의 `ISSCommandWithParameters::SetParameterProperties` 모든 매개 변수에 대해 지정 되었을 수 있는 모든 속성을 삭제 합니다.  
  
 *rgParamProperties*[in]  
 설정할 SSPARAMPROPS 구조의 배열입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 메서드 `ISSCommandWithParameters::SetParameterProperties` 는 Core OLE DB **ICommandProperties:: SetProperties** 메서드와 동일한 오류 코드를 반환 합니다.  
  
## <a name="remarks"></a>설명  
 이 메서드를 사용 하 여 매개 변수 속성을 설정 하는 것은 매개 변수 별로, 서 `ISSCommandWithParameters::SetParameterProperties` 수로 설정 하거나, SSPARAMPROPS가 속성 배열에서 빌드된 후에 한 번 호출 하 여 허용 됩니다.  
  
 메서드 **SetParameterInfo** 를 `ISSCommandWithParameters::SetParameterProperties` 호출 하기 전에 SetParameterInfo 메서드를 호출 해야 합니다. `SetParameterProperties(0, NULL)`를 호출하면 지정한 모든 매개 변수 속성이 지워지지만 `SetParameterInfo(0,NULL,NULL)`를 호출하면 매개 변수와 관련이 있을 수 있는 모든 속성을 비롯하여 모든 매개 변수 정보가 지워집니다.  
  
 DBTYPE_XML `ISSCommandWithParameters::SetParameterProperties` 또는 DBTYPE_UDT 형식이 아닌 매개 변수에 대 한 속성을 지정 하기 위해를 호출 하면 DB_E_ERRORSOCCURRED 또는 DB_S_ERRORSOCCURRED이 반환 되 고 해당 매개 변수에 대 한 SSPARAMPROPS에 포함 된 모든 Dbprops의 *dwstatus* 필드가 DBPROPSTATUS_NOTSET로 표시 됩니다. DB_E_ERRORSOCCURRED 또는 DB_S_ERRORSOCCURRED가 참조하는 매개 변수를 검색하기 위해 SSPARAMPROPS에 포함된 각 DBPROPSET의 DBPROP 배열을 이동해야 합니다.  
  
 SetParameterInfo `ISSCommandWithParameters::SetParameterProperties` 를 사용 하 여 매개 변수 정보가 아직 설정 되지 않은 매개 변수의 속성을 지정 하기 **SetParameterInfo**위해가 호출 되는 경우 공급자는 다음과 같은 오류 메시지와 함께 E_UNEXPECTED 반환 합니다.  
  
 먼저 SetParameterInfo 메서드를 호출해야만 지정한 매개 변수에 대해 SetParameterProperties 메서드를 호출할 수 있습니다. 매개 변수 속성을 설정하기 전에 매개 변수 정보를 설정해야 합니다.  
  
 에 대 `ISSCommandWithParameters::SetParameterProperties` 한 호출에 매개 변수 정보가 설정 된 일부 매개 변수가 포함 되어 있고 매개 변수 정보가 설정 되지 않은 일부 매개 변수가 포함 된 경우 SSPARAMPROPS 속성 집합의 DBPROPSET dwstatus 속성은 DBSTATUS_NOTSET로 반환 됩니다.  
  
 SSPARAMPROPS 구조는 다음과 같이 정의됩니다.  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 데이터베이스 엔진의 기능이 향상되어 ISSCommandWithParameters::SetParameterProperties를 통해 예상 결과에 대한 보다 정확한 설명을 얻을 수 있습니다. 보다 정확한 결과는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 ISSCommandWithParameters::SetParameterProperties가 반환한 값과 다를 수 있습니다. 자세한 내용은 [메타데이터 검색](../native-client/features/metadata-discovery.md)을 참조하세요.  
  
|멤버|설명|  
|------------|-----------------|  
|*iOrdinal*|전달된 매개 변수의 서수입니다.|  
|*cPropertySets*|*rgPropertySets*에 있는 DBPROPSET 구조의 개수입니다.|  
|*rgPropertySets*|DBPROPSET 구조의 배열을 반환할 메모리에 대한 포인터입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ISSCommandWithParameters&#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
