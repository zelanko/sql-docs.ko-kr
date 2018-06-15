---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 713169c273466260872ba29d65ab9c691dc5baf6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32949008"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  각 UDT 또는 XML 매개 변수당 SSPARAMPROPS 속성 집합을 하나씩 반환하는 방식으로 SSPARAMPROPS 속성 집합 구조의 배열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>인수  
 *pcParams*[in] [out]  
 반환 된 SSPARAMPROPS 구조의 개수를 포함 하는 메모리에 대 한 포인터 *prgParamProperties*합니다.  
  
 *prgParamProperties*[out]  
 SSPARAMPROPS 구조의 배열이 반환될 메모리에 대한 포인터입니다. 공급자는 구조에 대 한 메모리를 할당 하 고이 메모리에 주소를 반환 사용 하 여이 메모리를 해제 하는 소비자 **imalloc:: Free** 때 구조는 더 이상 필요 합니다. 호출 하기 전에 **imalloc:: Free** 에 대 한 *prgParamProperties*, 소비자도 호출 해야 **VariantClear** 에 대 한는 *vValue* variant 참조 형식 (예: BSTR입니다.)을 포함 되어 있는 경우에서 메모리 누수를 방지 하기 위해 각 DBPROP 구조의 속성 경우 *pcParams* 부분은 출력 시 0 이거나 DB_E_ERRORSOCCURRED 외의 오류가 발생 공급자는 메모리를 할당 하지 않고 사용 하면 *prgParamProperties* 출력에 대 한 null 포인터입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **GetParameterProperties** 메서드는 핵심 OLE DB 동일한 오류 코드 반환 **icommandproperties:: Getproperties** 메서드는 DB_S_ERRORSOCCURRED 및 db_e_errorsoccured가 제외 하 고 수준을 올릴 수 없습니다.  
  
## <a name="remarks"></a>주의  
 **Isscommandwithparameters:: Getparameterproperties** 기준으로 일관성 있게 동작 **GetParameterInfo**합니다. 경우 [isscommandwithparameters:: Setparameterproperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) 또는 **SetParameterInfo** 호출 하지 않은 또는 cParams를 0으로 호출 된 **GetParameterInfo** 매개 변수 정보를 파생 하 고이 반환 합니다. 경우 **isscommandwithparameters:: Setparameterproperties** 또는 **SetParameterInfo** 매개 변수가 하나 이상에 대 한 호출 된 **isscommandwithparameters:: Getparameterproperties** 는 해당 매개 변수에 대해서만 속성을 반환 **isscommandwithparameters:: Setparameterproperties** 가 호출 되었습니다. 경우 **isscommandwithparameters:: Setparameterproperties** 이후에 호출 **isscommandwithparameters:: Getparameterproperties** 또는 **GetParameterInfo**후속에 대 한 호출이 **isscommandwithparameters:: Getparameterproperties** 해당 매개 변수에 대해 재정의 된 값을 반환 **isscommandwithparameters:: Setparameterproperties** 가 호출 된 합니다.  
  
 SSPARAMPROPS 구조는 다음과 같이 정의됩니다.  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|멤버|Description|  
|------------|-----------------|  
|*iOrdinal*|전달된 매개 변수의 서수입니다.|  
|*cPropertySets*|DBPROPSET 수가 구조체에 *rgPropertySets*합니다.|  
|*rgPropertySets*|DBPROPSET 구조의 배열을 반환할 메모리에 대한 포인터입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [ISSCommandWithParameters & #40; OLE db& #41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
