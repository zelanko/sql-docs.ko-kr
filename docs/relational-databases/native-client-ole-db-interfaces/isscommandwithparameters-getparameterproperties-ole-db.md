---
title: ISSCommandWithParameters::GetParameterProperties(OLE DB)
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26c95c64f0f2922ef11946841b160879f001e358
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290083"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  각 UDT 또는 XML 매개 변수당 SSPARAMPROPS 속성 집합을 하나씩 반환하는 방식으로 SSPARAMPROPS 속성 집합 구조의 배열을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>인수  
 *pcParams*[out][in]  
 *prgParamProperties*에 반환된 SSPARAMPROPS 구조의 개수를 포함하는 메모리에 대한 포인터입니다.  
  
 *prgParamProperties*[out]  
 SSPARAMPROPS 구조의 배열이 반환될 메모리에 대한 포인터입니다. 공급자는 구조에 대한 메모리를 할당하고 주소를 이 메모리에 반환합니다. 소비자는 **IMalloc::Free를** 통해 이 메모리를 해제합니다. **IMalloc::Free** *prgParamProperties에*대 한 무료, 소비자는 또한 호출 해야 **VariantClear** 각 DBPROP 구조의 *vValue* 속성에 대 한 변종 에 포함 된 경우 메모리 누수를 방지 하기 위해 (예: BSTR.) *pcParams* 출력에 0 또는 DB_E_ERRORSOCCURRED 발생 하는 이외의 오류가 발생 하는 경우 공급자는 메모리를 할당 하지 않습니다 및 *prgParamProperties* 출력에 null 포인터는 확인 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **GetParameterProperties** 메서드는 코어 OLE DB **ICommandProperties::GetProperties** 메서드와 동일한 오류 코드를 반환합니다.DB_S_ERRORSOCCURRED 및 DB_E_ERRORSOCCURED 발생될 수 없습니다.  
  
## <a name="remarks"></a>설명  
 **ISSCommandWithParameters::GetParameterProperties** **GetParameterInfo**에 대해 일관되게 수행됩니다. [ISSCommandWithParameters::SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) 또는 **SetParameterInfo** 호출 되지 않은 경우 또는 0으로 같은 cParams와 함께 호출 **되었습니다., GetParameterInfo** 매개 변수 정보를 파생 하 고이 반환 합니다. **ISSCommandWithParameters::SetParameterProperties** 또는 **SetParameterInfo가** 하나 이상의 매개 변수에 대해 호출된 경우 **ISSCommandWithParameters::GetParameterProperties는** **ISSCommandWithParameters::SetParameterProperties가** 호출된 해당 매개 변수에 대해서만 속성을 반환합니다. **ISSCommandWithParameters::SetParameterProperties** **ISSCommandWithParameters::GetParameterProperties또는** **GetParameterInfo,** **ISSCommandWithParameters::GetParameterProperties에** 대한 후속 호출 후 호출은 **ISSCommandWithParameters::SetParameterProperties가** 호출된 해당 매개 변수에 대해 재정의된 값을 반환합니다.  
  
 SSPARAMPROPS 구조는 다음과 같이 정의됩니다.  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

|멤버|설명|  
|------------|-----------------|  
|*iOrdinal*|전달된 매개 변수의 서수입니다.|  
|*cPropertySets*|*rgPropertySets*에 있는 DBPROPSET 구조의 개수입니다.|  
|*rgPropertySets*|DBPROPSET 구조의 배열을 반환할 메모리에 대한 포인터입니다.|  
|||

## <a name="see-also"></a>참고 항목  
 [ISSCommandWithParameters&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
