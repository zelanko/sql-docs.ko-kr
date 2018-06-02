---
title: 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
ms.assetid: 5e7b3cbe-3670-4e18-8172-2226e0b6b142
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1d12a7c6dfc3a63d20a16a4a4361ffd46e4f8972
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34708491"
---
# <a name="rowsets"></a>행 집합
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  행 집합은 데이터 열이 포함된 행의 집합입니다. 행 집합은 모든 OLE DB 데이터 공급자가 결과 집합 데이터를 테이블 형식으로 노출할 수 있도록 하는 중앙 개체입니다.  
  
 소비자가 사용 하 여 세션을 만든 후의 **idbcreatesession:: Createsession** 메서드를 소비자 중 하나를 사용할 수는 **IOpenRowset** 또는 **IDBCreateCommand** 인터페이스는 행 집합을 만드는 세션입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 이러한 인터페이스의 모두 지원 합니다. 여기서는 두 메서드에 대해 모두 설명합니다.  
  
-   호출 하 여 행 집합을 만듭니다는 **iopenrowset:: Openrowset** 메서드.  
  
     이것은 단일 테이블에 대해 행 집합을 만드는 것과 같습니다. 이 메서드는 단일 기본 테이블의 모든 행이 포함된 행 집합을 열고 반환합니다. 에 대 한 인수 중 하나가 **OpenRowset** 행 집합을 만드는 데 사용할 테이블을 식별 하는 테이블 id입니다.  
  
-   호출 하 여 명령 개체를 만들는 **idbcreatecommand:: Createcommand** 메서드.  
  
     명령 개체는 공급자가 지원하는 명령을 실행합니다. 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하여 SELECT 문이나 저장 프로시저 호출과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 지정할 수 있습니다. 명령 개체를 사용하여 행 집합을 만드는 단계는 다음과 같습니다.  
  
    1.  호출 하 여 소비자는 **idbcreatecommand:: Createcommand** 요청 명령 개체를 가져오려는 세션에서 메서드는 **ICommandText** command 개체 인터페이스입니다. 이 **ICommandText** 인터페이스 설정 하 고 실제 명령 텍스트를 검색 합니다. 호출 하 여 텍스트 명령을 채웁니다 소비자는 **icommandtext:: Setcommandtext** 메서드.  
  
    2.  호출 하 여 사용자는 **icommand:: Execute** 명령에는 메서드. 명령을 실행할 때 작성된 행 집합 개체에는 명령의 결과 집합이 포함됩니다.  
  
 소비자가 사용할 수는 **ICommandProperties** 가져오거나 실행 한 명령에서 반환 된 행 집합에 대 한 속성을 설정 하는 인터페이스는 **icommand:: Execute** 인터페이스입니다. 자주 요청되는 속성은 행 집합에서 지원해야 하는 인터페이스입니다. 인터페이스 외에도 소비자는 행 집합이나 인터페이스의 동작을 수정하는 속성을 요청할 수 있습니다.  
  
 소비자가 행 집합을 릴리스는 **irowset:: Release** 메서드. 행 집합을 해제하면 해당 행 집합에서 소비자가 보유한 행 핸들이 모두 해제됩니다. 행 집합을 해제해도 접근자는 해제되지 않습니다. 있는 경우는 **IAccessor** 인터페이스,이를 해제 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [IOpenRowset을 사용하여 행 집합 만들기](../../relational-databases/native-client-ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [ICommand::Execute를 사용하여 행 집합 만들기](../../relational-databases/native-client-ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [행 집합 속성 및 동작](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [행 집합 및 SQL Server 커서](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [행 페치](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [IRow를 사용하여 단일 행 페치](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [책갈피](../../relational-databases/native-client-ole-db-rowsets/bookmarks.md)  
  
-   [행 집합의 데이터 업데이트](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
