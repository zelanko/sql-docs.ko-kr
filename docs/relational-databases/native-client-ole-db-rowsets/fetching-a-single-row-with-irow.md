---
description: IRow를 사용 하 여 단일 행 페치 (Native Client OLE DB 공급자)
title: IRow를 사용 하 여 단일 행 페치 (Native Client OLE DB 공급자) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 60fd6650b2f8c0ae3a43513848e145d14c0c546d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469294"
---
# <a name="fetching-a-single-row-with-irow-native-client-ole-db-provider"></a>IRow를 사용 하 여 단일 행 페치 (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Native Client OLE DB 공급자에서 **IRow** 인터페이스를 구현 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능을 향상 시킬 수 있습니다. **IRow** 를 사용하여 단일 행 개체의 열에 직접 액세스할 수 있습니다. 명령 실행의 결과로 정확히 하나의 행이 생성된다는 것을 미리 알고 있는 경우 **IRow** 는 해당 행의 열을 검색합니다. 결과 집합에 여러 행이 포함되는 경우 **IRow** 는 첫 번째 행만 노출합니다.  
  
 **IRow** 구현에서는 행을 탐색할 수 없습니다. 한 가지 경우를 제외하고 행의 각 열은 한 번만 액세스할 수 있습니다. 한 가지 예외는 열 크기를 찾기 위해 열에 한 번 액세스하고 데이터를 인출하기 위해 다시 액세스할 수 있다는 점입니다.  
  
> [!NOTE]  
>  **IRow::Open** 은 DBGUID_STREAM 및 DBGUID_NULL 개체 유형만 열 수 있습니다.  
  
 **ICommand::Execute** 메서드를 사용하여 행 개체를 가져오려면 IID_IRow를 전달해야 합니다. 여러 결과 집합을 처리하려면 **IMultipleResults** 인터페이스를 사용해야 합니다. **IMultipleResults** 는 **IRow** 및 **IRowset** 을 지원합니다. **IRowset** 은 대량 작업에 사용합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [IRow::GetColumns 사용](../../relational-databases/native-client-ole-db-rowsets/using-irow-getcolumns.md)  
  
-   [IRow를 사용하여 BLOB 데이터 인출]()  
  
## <a name="see-also"></a>참고 항목  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
