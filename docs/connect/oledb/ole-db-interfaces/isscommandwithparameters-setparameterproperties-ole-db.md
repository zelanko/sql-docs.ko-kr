---
title: 'Isscommandwithparameters:: Setparameterproperties (OLE DB) | Microsoft Docs'
description: ISSCommandWithParameters::SetParameterProperties(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- SetParameterProperties method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 6d20214d99a9f1b4f9be28be967fb54023057536
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033641"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  매개 변수별 서수로 매개 변수 속성을 설정하거나, SSPARAMPROPS 구조의 배열을 지정하여 대량 매개 변수 속성을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT SetParameterProperties(  
      DB_UPARAMS cParams,   
      SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>인수  
 *cParams*[in]  
 *rgParamProperties* 배열의 SSPARAMPROPS 구조 수입니다. 이 개수가 0이면 **ISSCommandWithParameters::SetParameterProperties**가 명령의 매개 변수에 대해 지정되었을 수 있는 모든 속성을 삭제합니다.  
  
 *rgParamProperties*[in]  
 설정할 SSPARAMPROPS 구조의 배열입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **ISSCommandWithParameters::SetParameterProperties** 메서드에서 핵심 OLE DB **ICommandProperties::SetProperties** 메서드와 동일한 오류 코드를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 이 메서드를 사용한 매개 변수 속성 설정은 매개 변수별 서수로 허용되거나, 속성 배열에서 SSPARAMPROPS가 작성된 후 단일 **ISSCommandWithParameters::SetParameterProperties** 호출을 사용하여 허용됩니다.  
  
 **ISSCommandWithParameters::SetParameterProperties** 메서드를 호출하기 전에 **SetParameterInfo** 메서드를 호출해야 합니다. `SetParameterProperties(0, NULL)`를 호출하면 지정한 모든 매개 변수 속성이 지워지지만 `SetParameterInfo(0,NULL,NULL)`를 호출하면 매개 변수와 관련이 있을 수 있는 모든 속성을 비롯하여 모든 매개 변수 정보가 지워집니다.  
  
 DBTYPE_XML 또는 DBTYPE_UDT 유형이 아닌 매개 변수의 속성을 지정하기 위해 **ISSCommandWithParameters::SetParameterProperties**를 호출하면 DB_E_ERRORSOCCURRED 또는 DB_S_ERRORSOCCURRED가 반환되고, 해당 매개 변수의 SSPARAMPROPS에 포함된 모든 DBPROP의 *dwStatus* 필드에 DBPROPSTATUS_NOTSET가 표시됩니다. DB_E_ERRORSOCCURRED 또는 DB_S_ERRORSOCCURRED가 참조하는 매개 변수를 검색하기 위해 SSPARAMPROPS에 포함된 각 DBPROPSET의 DBPROP 배열을 이동해야 합니다.  
  
 **SetParameterInfo**를 사용하여 매개 변수 정보가 아직 설정되지 않은 매개 변수의 속성을 지정하기 위해 **ISSCommandWithParameters::SetParameterProperties**를 호출하면 공급자가 다음 오류 메시지와 함께 E_UNEXPECTED를 반환합니다.  
  
 먼저 SetParameterInfo 메서드를 호출해야만 지정한 매개 변수에 대해 SetParameterProperties 메서드를 호출할 수 있습니다. 매개 변수 속성을 설정하기 전에 매개 변수 정보를 설정해야 합니다.  
  
 **ISSCommandWithParameters::SetParameterProperties**에 대한 호출에 포함된 일부 매개 변수는 매개 변수 정보가 설정되어 있고 다른 일부 매개 변수는 매개 변수 정보가 설정되어 있지 않은 경우 SSPARAMPROPS 속성 집합의 DBPROPSET에 있는 dwStatus 속성이 DBSTATUS_NOTSET로 반환됩니다.  
  
 SSPARAMPROPS 구조는 다음과 같이 정의됩니다.  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 부터 데이터베이스 엔진의 개선 사항 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] isscommandwithparameters:: Setparameterproperties 예상된 결과 대 한 보다 정확한 설명의 얻을를 허용 합니다. 이전 버전의 isscommandwithparameters:: Setparameterproperties 반환한 값에서 다를 수 있습니다 이러한 보다 정확한 결과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [메타데이터 검색](../../oledb/features/metadata-discovery.md)을 참조하세요.  
  
|멤버|설명|  
|------------|-----------------|  
|*iOrdinal*|전달된 매개 변수의 서수입니다.|  
|*cPropertySets*|*rgPropertySets*에 있는 DBPROPSET 구조의 개수입니다.|  
|*rgPropertySets*|DBPROPSET 구조의 배열을 반환할 메모리에 대한 포인터입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
