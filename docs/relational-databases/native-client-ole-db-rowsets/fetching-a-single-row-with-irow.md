---
title: IRow 사용 하 여 단일 행 페치 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ab4a6e50ce20b1bceddfb639e5780938f3687639
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412002"
---
# <a name="fetching-a-single-row-with-irow"></a>IRow를 사용하여 단일 행 인출
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  합니다 **IRow** 인터페이스의 구현을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 성능을 향상 시키기 위해 간소화 됩니다. **IRow** 단일 행 개체의 열에 직접 액세스할 수 있습니다. 명령 실행의 결과 정확히 하나의 행을 생성는 미리 알고 있으면 **IRow** 해당 행의 열을 검색 합니다. 결과 집합에 여러 행을 포함 하는 경우 **IRow** 첫 번째 행만 표시 됩니다.  
  
 합니다 **IRow** 구현 행의 모든 탐색을 허용 하지 않습니다. 한 가지 경우를 제외하고 행의 각 열은 한 번만 액세스할 수 있습니다. 한 가지 예외는 열 크기를 찾기 위해 열에 한 번 액세스하고 데이터를 인출하기 위해 다시 액세스할 수 있다는 점입니다.  
  
> [!NOTE]  
>  **Irow:: Open** 만 DBGUID_STREAM 및 DBGUID_NULL 개체 유형의 열을 지원 합니다.  
  
 사용 하 여 행 개체를 가져올 **icommand:: Execute** 메서드를 IID_IRow를 전달 되어야 합니다. 합니다 **IMultipleResults** 인터페이스를 사용 하 여 여러 결과 집합을 처리할 수 있어야 합니다. **IMultipleResults** 지원 **IRow** 하 고 **IRowset**합니다. **IRowset** 대량 작업에 사용 됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [IRow::GetColumns 사용](../../relational-databases/native-client-ole-db-rowsets/using-irow-getcolumns.md)  
  
-   [IRow를 사용하여 BLOB 데이터 인출](http://msdn.microsoft.com/library/badbd6ac-20aa-4891-a14f-48d38e7f30de)  
  
## <a name="see-also"></a>관련 항목  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
