---
title: 행 집합 | Microsoft Docs
description: OLE DB Driver for SQL Server의에서 행 집합
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d3f187118cd273712ed8145bbfef3af712091028
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="rowsets"></a>행 집합
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  행 집합은 데이터 열이 포함된 행의 집합입니다. 행 집합은 모든 OLE DB 데이터 공급자가 결과 집합 데이터를 테이블 형식으로 노출할 수 있도록 하는 중앙 개체입니다.  
  
 소비자가 사용 하 여 세션을 만든 후의 **idbcreatesession:: Createsession** 메서드를 소비자 하나를 사용할 수는 **IOpenRowset** 또는 **IDBCreateCommand** 인터페이스에는 행 집합을 만들 수 있습니다. OLE DB Driver for SQL Server 두이 인터페이스를 지원합니다. 여기서는 두 메서드에 대해 모두 설명합니다.  
  
-   호출 하 여 행 집합을 만듭니다는 **iopenrowset:: Openrowset** 메서드.  
  
     이것은 단일 테이블에 대해 행 집합을 만드는 것과 같습니다. 이 메서드는 단일 기본 테이블의 모든 행이 포함된 행 집합을 열고 반환합니다. 에 대 한 인수 중 하나가 **OpenRowset** 행 집합을 만드는 데 사용할 테이블을 식별 하는 테이블 id입니다.  
  
-   호출 하 여 명령 개체를 만들는 **idbcreatecommand:: Createcommand** 메서드.  
  
     명령 개체는 공급자가 지원하는 명령을 실행합니다. OLE DB 드라이버와 SQL Server에 대 한 소비자는를 지정할 수 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT 문 또는 저장된 프로시저에 대 한 호출 등의 문. 명령 개체를 사용하여 행 집합을 만드는 단계는 다음과 같습니다.  
  
    1.  호출 하 여 소비자는 **idbcreatecommand:: Createcommand** 요청 명령 개체를 가져오려는 세션에서 메서드는 **ICommandText** command 개체 인터페이스입니다. 이 **ICommandText** 인터페이스 설정 하 고 실제 명령 텍스트를 검색 합니다. 호출 하 여 텍스트 명령을 채웁니다 소비자는 **icommandtext:: Setcommandtext** 메서드.  
  
    2.  호출 하 여 사용자는 **icommand:: Execute** 명령에는 메서드. 명령을 실행할 때 작성된 행 집합 개체에는 명령의 결과 집합이 포함됩니다.  
  
 소비자가 사용할 수는 **ICommandProperties** 가져오거나 실행 한 명령에서 반환 된 행 집합에 대 한 속성을 설정 하는 인터페이스는 **icommand:: Execute** 인터페이스입니다. 자주 요청되는 속성은 행 집합에서 지원해야 하는 인터페이스입니다. 인터페이스 외에도 소비자는 행 집합이나 인터페이스의 동작을 수정하는 속성을 요청할 수 있습니다.  
  
 소비자가 행 집합을 릴리스는 **irowset:: Release** 메서드. 행 집합을 해제하면 해당 행 집합에서 소비자가 보유한 행 핸들이 모두 해제됩니다. 행 집합을 해제해도 접근자는 해제되지 않습니다. 있는 경우는 **IAccessor** 인터페이스,이를 해제 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [IOpenRowset를 사용 하 여 행 집합 만들기](../../oledb/ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [Icommand:: Execute를 사용 하 여 행 집합 만들기](../../oledb/ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [행 집합 속성 및 동작](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [행 집합 및 SQL Server 커서](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [행 인출](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
-   [IRow와 단일 행 인출](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [책갈피](../../oledb/ole-db-rowsets/bookmarks.md)  
  
-   [행 집합의 데이터 업데이트](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
