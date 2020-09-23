---
title: 행 집합(OLE DB 드라이버)
description: OLE DB Driver for SQL Server에서 소비자가 한 세션에서 한 행 집합을 만들도록 지원하는 인터페이스에 대해 알아봅니다. 자세한 내용은 이 섹션의 문서를 참조하세요.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55100932092abeb81da7fa1c156ccb5a61fc193c
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859942"
---
# <a name="rowsets"></a>행 집합
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  행 집합은 데이터 열이 포함된 행의 집합입니다. 행 집합은 모든 OLE DB 데이터 공급자가 결과 집합 데이터를 테이블 형식으로 노출할 수 있도록 하는 중앙 개체입니다.  
  
 소비자는 **IDBCreateSession::CreateSession** 메서드를 사용하여 세션을 만든 후 세션에서 **IOpenRowset** 또는 **IDBCreateCommand** 인터페이스를 사용하여 행 집합을 만들 수 있습니다. OLE DB Driver for SQL Server는 해당 인터페이스를 둘 다 지원합니다. 여기서는 두 메서드에 대해 모두 설명합니다.  
  
-   **IOpenRowset::OpenRowset** 메서드를 호출하여 행 집합을 만듭니다.  
  
     이것은 단일 테이블에 대해 행 집합을 만드는 것과 같습니다. 이 메서드는 단일 기본 테이블의 모든 행이 포함된 행 집합을 열고 반환합니다. **OpenRowset**에 대한 인수 중 하나는 행 집합을 만드는 데 사용할 테이블을 식별하는 테이블 ID입니다.  
  
-   **IDBCreateCommand::CreateCommand** 메서드를 호출하여 명령 개체를 만듭니다.  
  
     명령 개체는 공급자가 지원하는 명령을 실행합니다. 소비자는 SQL Server용 OLE DB 드라이버를 사용하여 SELECT 문이나 저장 프로시저 호출과 같은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 지정할 수 있습니다. 명령 개체를 사용하여 행 집합을 만드는 단계는 다음과 같습니다.  
  
    1.  소비자는 세션에서 **IDBCreateCommand::CreateCommand** 메서드를 호출하여 명령 개체를 가져오고 해당 명령 개체에서 **ICommandText** 인터페이스를 요청합니다. 이 **ICommandText** 인터페이스는 실제 명령 텍스트를 설정하고 검색합니다. 소비자는 **ICommandText::SetCommandText** 메서드를 호출하여 텍스트 명령을 채웁니다.  
  
    2.  사용자는 명령에서 **ICommand::Execute** 메서드를 호출합니다. 명령을 실행할 때 작성된 행 집합 개체에는 명령의 결과 집합이 포함됩니다.  
  
 소비자는 **ICommandProperties** 인터페이스를 사용하여 **ICommand::Execute** 인터페이스가 실행한 명령에서 반환된 행 집합의 속성을 가져오거나 설정할 수 있습니다. 자주 요청되는 속성은 행 집합에서 지원해야 하는 인터페이스입니다. 인터페이스 외에도 소비자는 행 집합이나 인터페이스의 동작을 수정하는 속성을 요청할 수 있습니다.  
  
 소비자는 **IRowset::Release** 메서드를 사용하여 행 집합을 해제합니다. 행 집합을 해제하면 해당 행 집합에서 소비자가 보유한 행 핸들이 모두 해제됩니다. 행 집합을 해제해도 접근자는 해제되지 않습니다. **IAccessor** 인터페이스가 있는 경우 이를 해제해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [IOpenRowset을 사용하여 행 집합 만들기](../../oledb/ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [ICommand::Execute를 사용하여 행 집합 만들기](../../oledb/ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [행 집합 속성 및 동작](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [행 집합 및 SQL Server 커서](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [행 페치](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
-   [IRow를 사용하여 단일 행 페치](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [책갈피](../../oledb/ole-db-rowsets/bookmarks.md)  
  
-   [행 집합의 데이터 업데이트](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
