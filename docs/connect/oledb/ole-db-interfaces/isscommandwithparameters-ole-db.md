---
title: ISSCommandWithParameters(OLE DB 드라이버)
description: ISSCommandWithParameters(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
author: pmasl
ms.author: pelopes
ms.openlocfilehash: bf289aefc600b0bf7772574af91fc43272347457
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244229"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters(OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ISSCommandWithParameters** 매개 변수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 및 UDT(사용자 정의 형식)에 대한 지원을 노출합니다. 핵심 OLE DB 인터페이스인 **ICommandWithParameters**에서 상속되는 선택적 인터페이스입니다. **ICommandWithParameters**에서 상속되는 3개의 메서드인 **GetParameterInfo**, **MapParameterNames**및 **SetParameterInfo** 외에 **ISSCommandWithParameters**는 서버별 데이터 형식을 처리하는 데 사용되는 두 개의 새 메서드를 제공합니다.  
  
> [!NOTE]  
>  서비스 구성 요소가 사용되는 경우 **ISSCommandWithParameters** 인터페이스를 사용할 수 있지만 서비스 구성 요소는 이 인터페이스를 사용하지 않습니다.  
  
|방법|Description|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|명령에 전달된 각 UDT 또는 XML 매개 변수에 대해 배열의 **SSPARAMPROPS** 속성 집합 구조를 하나씩 반환하지만 다른 유형의 매개 변수에 대해서는 아무 것도 반환되지 않습니다.|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|매개 변수별 서수로 매개 변수 속성을 설정하거나, **SSPARAMPROPS** 구조의 배열을 지정하여 대량 매개 변수 속성을 설정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [XML 데이터 형식 사용](../../oledb/features/using-xml-data-types.md)   
 [사용자 정의 형식 사용](../../oledb/features/using-user-defined-types.md)  
  
  
