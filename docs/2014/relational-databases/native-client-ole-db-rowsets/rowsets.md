---
title: 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
ms.assetid: 5e7b3cbe-3670-4e18-8172-2226e0b6b142
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73f16529f84fd9a7eb0158061ab4f875050a8496
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411712"
---
# <a name="rowsets"></a>행 집합
  행 집합은 데이터 열이 포함된 행의 집합입니다. 행 집합은 모든 OLE DB 데이터 공급자가 결과 집합 데이터를 테이블 형식으로 노출할 수 있도록 하는 중앙 개체입니다.  
  
 소비자를 사용 하 여 세션을 만든 후는 **idbcreatesession:: Createsession** 메서드를 소비자 중 하나를 사용할 수는 **IOpenRowset** 하거나 **IDBCreateCommand** 행 집합을 만드는 세션에 대 한 인터페이스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 모두 이러한 인터페이스를 지원 합니다. 여기서는 두 메서드에 대해 모두 설명합니다.  
  
-   호출 하 여 행 집합을 만들어야 합니다 **iopenrowset:: Openrowset** 메서드.  
  
     이것은 단일 테이블에 대해 행 집합을 만드는 것과 같습니다. 이 메서드는 단일 기본 테이블의 모든 행이 포함된 행 집합을 열고 반환합니다. 인수 중 하나 **OpenRowset** 행 집합을 만드는 데 사용할 테이블을 식별 하는 테이블 ID입니다.  
  
-   호출 하 여 명령 개체를 만들 합니다 **idbcreatecommand:: Createcommand** 메서드.  
  
     명령 개체는 공급자가 지원하는 명령을 실행합니다. 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하여 SELECT 문이나 저장 프로시저 호출과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 지정할 수 있습니다. 명령 개체를 사용하여 행 집합을 만드는 단계는 다음과 같습니다.  
  
    1.  소비자 호출을 **idbcreatecommand:: Createcommand** 요청 하는 명령 개체를 가져오려는 세션에서 메서드는 **ICommandText** 명령 개체 인터페이스. 이렇게 **ICommandText** 인터페이스 설정 하 고 실제 명령 텍스트를 검색 합니다. 소비자를 호출 하 여 텍스트 명령을 채웁니다 합니다 **icommandtext:: Setcommandtext** 메서드.  
  
    2.  사용자 호출을 **icommand:: Execute** 명령에는 메서드. 명령을 실행할 때 작성된 행 집합 개체에는 명령의 결과 집합이 포함됩니다.  
  
 소비자가 사용할 수는 **ICommandProperties** 인터페이스를 가져오거나 설정 하 여 실행 한 명령에서 반환 된 행에 대 한 속성을 **icommand:: Execute** 인터페이스. 자주 요청되는 속성은 행 집합에서 지원해야 하는 인터페이스입니다. 인터페이스 외에도 소비자는 행 집합이나 인터페이스의 동작을 수정하는 속성을 요청할 수 있습니다.  
  
 소비자가 행 집합을 해제 합니다 **irowset:: Release** 메서드. 행 집합을 해제하면 해당 행 집합에서 소비자가 보유한 행 핸들이 모두 해제됩니다. 행 집합을 해제해도 접근자는 해제되지 않습니다. 있는 경우는 **IAccessor** 인터페이스에 출시 될 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [IOpenRowset을 사용하여 행 집합 만들기](creating-a-rowset-with-iopenrowset.md)  
  
-   [ICommand::Execute를 사용하여 행 집합 만들기](creating-rowsets-with-icommand-execute.md)  
  
-   [행 집합 속성 및 동작](rowset-properties-and-behaviors.md)  
  
-   [행 집합 및 SQL Server 커서](rowsets-and-sql-server-cursors.md)  
  
-   [행 페치](fetching-rows.md)  
  
-   [IRow를 사용하여 단일 행 페치](fetching-a-single-row-with-irow.md)  
  
-   [책갈피](bookmarks.md)  
  
-   [행 집합의 데이터 업데이트](updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
