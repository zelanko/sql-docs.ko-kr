---
title: ICommand(OLE DB 드라이버) | Microsoft Docs
description: OLE DB Driver for SQL Server와 관련된 ICommand::Execute 메서드의 동작에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf787628804f3597fa724c0ab6313a450e365d58
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861906"
---
# <a name="icommand-ole-db"></a>ICommand(OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 문서에서는 OLE DB Driver for SQL Server와 관련된 OLE DB 동작에 대해 설명합니다.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 열 크기보다 큰 데이터를 삽입하면 일반적으로 오류가 발생합니다. 그러나 S_OK가 반환되고 `dwStatus`가 DBSTATUS_S_TRUNCATED로 설정되는 경우가 있습니다. 일반적으로 발생하는 몇 가지 시나리오는 다음과 같습니다.

- 매개 변수를 사용하여 데이터를 삽입하는 경우  
- 열이 데이터를 보관할 수 있을 만큼 크지 않은 경우  
- `ICommandWithParameters::SetParameterInfo`가 호출되지 않은 경우  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
