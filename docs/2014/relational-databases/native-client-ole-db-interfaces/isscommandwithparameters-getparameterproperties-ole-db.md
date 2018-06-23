---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f06c97d1f6d1e477700117c3038d0186db085fd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089051"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties(OLE DB)
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
 SSPARAMPROPS 구조의 배열이 반환될 메모리에 대한 포인터입니다. 공급자는 구조에 대 한 메모리를 할당 하 고이 메모리에 주소를 반환 사용 하 여이 메모리를 해제 하는 소비자 **imalloc:: Free** 때 구조는 더 이상 필요 합니다. 호출 하기 전에 **imalloc:: Free** 에 대 한 *prgParamProperties*, 소비자도 호출 해야 **VariantClear** 에 대 한는 *vValue* 속성 variant 대 한 참조에 포함 된 경우에 메모리 누수를 방지 하기 위해 각 DBPROP 구조의 형식 (예: BSTR입니다.) 경우 *pcParams* 부분은 출력 시 0 이거나 DB_E_ERRORSOCCURRED 외의 오류가 발생 공급자는 메모리를 할당 하지 않고 사용 하면 *prgParamProperties* 출력에 대 한 null 포인터입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **GetParameterProperties** 메서드는 핵심 OLE DB 동일한 오류 코드 반환 **icommandproperties:: Getproperties** 메서드는 DB_S_ERRORSOCCURRED 및 db_e_errorsoccured가 제외 될 수 없습니다 발생합니다.  
  
## <a name="remarks"></a>Remarks  
 **Isscommandwithparameters:: Getparameterproperties** 기준으로 일관성 있게 동작 **GetParameterInfo**합니다. 경우 [isscommandwithparameters:: Setparameterproperties](isscommandwithparameters-setparameterproperties-ole-db.md) 또는 **SetParameterInfo** 호출 하지 않은 또는 cParams를 0으로 호출 된 **GetParameterInfo**매개 변수 정보를 파생 하 고이 반환 합니다. 경우 **isscommandwithparameters:: Setparameterproperties** 또는 **SetParameterInfo** 매개 변수가 하나 이상에 대 한 호출 된 **isscommandwithparameters:: Getparameterproperties**  는 해당 매개 변수에 대해서만 속성을 반환 **isscommandwithparameters:: Setparameterproperties** 가 호출 되었습니다. 경우 **isscommandwithparameters:: Setparameterproperties** 이후에 호출 **isscommandwithparameters:: Getparameterproperties** 또는 **GetParameterInfo**, 에 대 한 후속 호출 **isscommandwithparameters:: Getparameterproperties** 해당 매개 변수에 대해 재정의 된 값을 반환 **isscommandwithparameters:: Setparameterproperties** 가 호출 되었습니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  