---
title: 'Isscommandwithparameters:: Setparameterproperties (OLE DB) | Microsoft Docs'
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
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096984"
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
 *rgParamProperties* 배열의 SSPARAMPROPS 구조 수입니다. 이 숫자가 0 이면 `ISSCommandWithParameters::SetParameterProperties` 명령에서 매개 변수에 대해 지정 된 모든 속성이 삭제 됩니다.  
  
 *rgParamProperties*[in]  
 설정할 SSPARAMPROPS 구조의 배열입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 합니다 `ISSCommandWithParameters::SetParameterProperties` 메서드에서 핵심 OLE DB 동일한 오류 코드도 반환 **icommandproperties:: Setproperties** 메서드.  
  
## <a name="remarks"></a>Remarks  
 서 수 또는 단일 당 매개 변수 별로 수는이 메서드를 사용 하 여 매개 변수 속성 설정 `ISSCommandWithParameters::SetParameterProperties` SSPARAMPROPS 속성 배열에서 빌드된 후 호출 합니다.  
  
 합니다 **SetParameterInfo** 메서드를 호출 하기 전에 호출 해야 합니다 `ISSCommandWithParameters::SetParameterProperties` 메서드. `SetParameterProperties(0, NULL)`를 호출하면 지정한 모든 매개 변수 속성이 지워지지만 `SetParameterInfo(0,NULL,NULL)`를 호출하면 매개 변수와 관련이 있을 수 있는 모든 속성을 비롯하여 모든 매개 변수 정보가 지워집니다.  
  
 호출 `ISSCommandWithParameters::SetParameterProperties` 형식이 아닌 매개 변수 속성을 지정할 DBTYPE_XML or DBTYPE_UDT 반환 DB_E_ERRORSOCCURRED 또는 DB_S_ERRORSOCCURRED 및 표시 합니다 *dwStatus* SSPARAMPROPS에 포함 된 모든 Dbprop의 필드 되를 사용 하 여 해당 매개 변수입니다. DB_E_ERRORSOCCURRED 또는 DB_S_ERRORSOCCURRED가 참조하는 매개 변수를 검색하기 위해 SSPARAMPROPS에 포함된 각 DBPROPSET의 DBPROP 배열을 이동해야 합니다.  
  
 하는 경우 `ISSCommandWithParameters::SetParameterProperties` 사용 하 여 매개 변수 정보가 아직 설정 되지 않은 매개 변수의 속성을 지정 하기 위해 호출 됩니다 **SetParameterInfo**, 공급자는 다음 오류 메시지와 함께 E_UNEXPECTED를 반환 합니다.  
  
 먼저 SetParameterInfo 메서드를 호출해야만 지정한 매개 변수에 대해 SetParameterProperties 메서드를 호출할 수 있습니다. 매개 변수 속성을 설정하기 전에 매개 변수 정보를 설정해야 합니다.  
  
 경우에 대 한 호출 `ISSCommandWithParameters::SetParameterProperties` 여기서 매개 변수 정보 설정 되 고 일부 매개 변수는 매개 변수 정보가 설정 되지 않은, SSPARAMPROPS 속성 집합의 DBPROPSET에 있는 dwStatus 속성이 DBSTATUS_NOTSET로 반환 됩니다 일부 매개 변수를 포함 합니다.  
  
 SSPARAMPROPS 구조는 다음과 같이 정의됩니다.  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 부터 데이터베이스 엔진의 개선 사항 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] isscommandwithparameters:: Setparameterproperties 예상된 결과 대 한 보다 정확한 설명의 얻을를 허용 합니다. 이전 버전의 isscommandwithparameters:: Setparameterproperties 반환한 값에서 다를 수 있습니다 이러한 보다 정확한 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [메타데이터 검색](../native-client/features/metadata-discovery.md)을 참조하세요.  
  
|멤버|Description|  
|------------|-----------------|  
|*iOrdinal*|전달된 매개 변수의 서수입니다.|  
|*cPropertySets*|*rgPropertySets*에 있는 DBPROPSET 구조의 개수입니다.|  
|*rgPropertySets*|DBPROPSET 구조의 배열을 반환할 메모리에 대한 포인터입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
