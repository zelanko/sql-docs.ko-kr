---
title: ICommandWithParameters | Microsoft Docs
description: ICommandWithParameters 인터페이스
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: a998292f4d1c03485dc75eee02cefa437dc1fe36
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600051"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  로 시작 하는 데이터베이스 엔진의에서 향상 된 기능 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] icommandwithparameters:: Getparameterinfo 예상된 결과 대 한 보다 정확한 설명의 얻을를 허용 합니다. 이전 버전의 CommandWithParameters::GetParameterInfo 반환한 값에서 다를 수 있습니다 이러한 보다 정확한 결과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [메타데이터 검색](../../oledb/features/metadata-discovery.md)을 참조하세요.  
  
 또한 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터는 ICommandWithParameters::SetParameterInfo를 호출할 때 *pwszName* 매개 변수에 전달된 값이 유효한 식별자여야 합니다. 자세한 내용은 [Database Identifiers](../../../relational-databases/databases/database-identifiers.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스 &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
