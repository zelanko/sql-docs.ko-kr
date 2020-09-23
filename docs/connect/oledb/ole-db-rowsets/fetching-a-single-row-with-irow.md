---
title: IRow를 사용하여 단일 행 페치(OLE DB 드라이버) | Microsoft Docs
description: IRow를 사용하여 단일 행 개체의 열에 직접 액세스할 수 있습니다. OLE DB Driver for SQL Server의 IRow 인터페이스는 단순화되어 성능이 향상되었습니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- OLE DB Driver for SQL Server, fetching
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a305692bb544d9a9bbb0572cbd93449781aaabe9
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862470"
---
# <a name="fetching-a-single-row-with-irow-ole-db-driver"></a>IRow를 사용하여 단일 행 페치(OLE DB 드라이버)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server의 **IRow** 인터페이스 구현이 간소화되어 성능이 향상되었습니다. **IRow**를 사용하여 단일 행 개체의 열에 직접 액세스할 수 있습니다. 명령 실행의 결과로 정확히 하나의 행이 생성된다는 것을 미리 알고 있는 경우 **IRow**는 해당 행의 열을 검색합니다. 결과 집합에 여러 행이 포함되는 경우 **IRow**는 첫 번째 행만 노출합니다.  
  
 **IRow** 구현에서는 행을 탐색할 수 없습니다. 한 가지 경우를 제외하고 행의 각 열은 한 번만 액세스할 수 있습니다. 한 가지 예외는 열 크기를 찾기 위해 열에 한 번 액세스하고 데이터를 인출하기 위해 다시 액세스할 수 있다는 점입니다.  
  
> [!NOTE]  
>  **IRow::Open**은 DBGUID_STREAM 및 DBGUID_NULL 개체 유형만 열 수 있습니다.  
  
 **ICommand::Execute** 메서드를 사용하여 행 개체를 가져오려면 IID_IRow를 전달해야 합니다. 여러 결과 집합을 처리하려면 **IMultipleResults** 인터페이스를 사용해야 합니다. **IMultipleResults**는 **IRow** 및 **IRowset**을 지원합니다. **IRowset**은 대량 작업에 사용합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [IRow::GetColumns 사용](../../oledb/ole-db-rowsets/using-irow-getcolumns.md)   
  
## <a name="see-also"></a>참고 항목  
 [행 집합](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
