---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6d90f4cdfd9ac42291da9bf6694a2786000ba8d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **ISSCommandWithParameters** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 및 UDT(사용자 정의 형식)에 대한 지원을 노출합니다. 이 인터페이스는 선택적 인터페이스이며 핵심 OLE DB 인터페이스인 **ICommandWithParameters**에서 상속됩니다. **ICommandWithParameters**에서 상속되는 3개의 메서드인 **GetParameterInfo**, **MapParameterNames**및 **SetParameterInfo**외에도 **ISSCommandWithParameters** 는 서버별 데이터 형식을 처리하는 데 사용되는 두 개의 새 메서드를 제공합니다.  
  
> [!NOTE]  
>  서비스 구성 요소가 사용되는 경우 **ISSCommandWithParameters** 인터페이스를 사용할 수 있지만 서비스 구성 요소 자체는 이 인터페이스를 사용하지 않습니다.  
  
|메서드|설명|  
|------------|-----------------|  
|[Isscommandwithparameters:: Getparameterproperties & #40; OLE db& #41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|명령에 전달된 각 UDT 또는 XML 매개 변수에 대해 배열의 **SSPARAMPROPS** 속성 집합 구조를 하나씩 반환하지만 다른 유형의 매개 변수에 대해서는 아무 것도 반환되지 않습니다.|  
|[Isscommandwithparameters:: Setparameterproperties & #40; OLE db& #41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|매개 변수별 서수로 매개 변수 속성을 설정하거나, **SSPARAMPROPS** 구조의 배열을 지정하여 대량 매개 변수 속성을 설정합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [인터페이스 & #40; OLE db& #41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [XML 데이터 형식 사용](../../relational-databases/native-client/features/using-xml-data-types.md)   
 [사용자 정의 형식 사용](../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
