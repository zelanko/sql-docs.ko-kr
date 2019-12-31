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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f7aed4457df4f262b485147a4d370812eefd7547
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252654"
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
 *Pcparams*[out] [in]  
 
  *prgParamProperties*에 반환된 SSPARAMPROPS 구조의 개수를 포함하는 메모리에 대한 포인터입니다.  
  
 *Prgparamproperties*[out]  
 SSPARAMPROPS 구조의 배열이 반환될 메모리에 대한 포인터입니다. 공급자는 구조에 대 한 메모리를 할당 하 고이 메모리에 주소를 반환 합니다. 소비자는 더 이상 구조가 필요 하지 않을 때 **IMalloc:: Free** 를 사용 하 여이 메모리를 해제 합니다. *Prgparamproperties*에 대해 **IMalloc:: Free** 를 호출 하기 전에, 소비자는 변형에 참조 형식 (예: BSTR)이 포함 된 경우 메모리 누수가 발생 하지 않도록 하기 위해 각 Dbprop 구조의 *Vvalue* 속성에 대해 **VariantClear** 를 호출 해야 합니다. *Pcparams* 가 output에서 0 이거나 DB_E_ERRORSOCCURRED 이외의 오류가 발생 한 경우 공급자는 메모리를 할당 하지 않고 *Prgparamproperties* 가 출력에서 null 포인터 임을 확인 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **Getparameterproperties** 메서드는 DB_S_ERRORSOCCURRED 및 DB_E_ERRORSOCCURED를 발생 시킬 수 없다는 점을 제외 하 고 코어 OLE DB **ICommandProperties:: GetProperties** 메서드와 동일한 오류 코드를 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **ISSCommandWithParameters:: GetParameterProperties** 는 **GetParameterInfo**에 대해 일관 되 게 동작 합니다. [ISSCommandWithParameters:: SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) 또는 **SetParameterInfo** 가 호출 되지 않았거나 cparams가 0으로 호출 된 경우 **GetParameterInfo** 는 매개 변수 정보를 파생 시키고 this를 반환 합니다. 하나 이상의 매개 변수에 대해 **ISSCommandWithParameters:: setparameterproperties** 또는 **SetParameterInfo** 를 호출한 경우 **ISSCommandWithParameters:: getparameterproperties** 는 **ISSCommandWithParameters:: setparameterproperties** 가 호출 된 해당 매개 변수에 대해서만 속성을 반환 합니다. **ISSCommandWithParameters:: setparameterproperties** 가 **ISSCommandWithParameters:: Getparameterproperties** 또는 **GetParameterInfo**이후에 호출 되는 경우 **ISSCommandWithParameters:: Getparameterproperties** 에 대 한 후속 호출은 **ISSCommandWithParameters:: setparameterproperties** 가 호출 된 해당 매개 변수에 대해 재정의 된 값을 반환 합니다.  
  
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
|*cPropertySets*|
  *rgPropertySets*에 있는 DBPROPSET 구조의 개수입니다.|  
|*rgPropertySets*|DBPROPSET 구조의 배열을 반환할 메모리에 대한 포인터입니다.|  
|||

## <a name="see-also"></a>참고 항목  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
