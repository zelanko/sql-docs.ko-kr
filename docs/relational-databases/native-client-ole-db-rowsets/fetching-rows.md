---
title: 행 인출 | Microsoft Docs
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
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 5e6dbe36-b682-464d-adfa-8e886f9bd452
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 24d8b01218b506e5041ad453a07a501ec615e894
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32950148"
---
# <a name="fetching-rows"></a>행 인출
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRowset** 인터페이스는 기본 행 집합 인터페이스입니다. **IRowset** 인터페이스는 순차적으로 행을 인출 하 고, 해당 행에서 데이터를 가져오는 행을 관리 하기 위한 메서드를 제공 합니다. 메서드를 사용 하는 소비자 **IRowset** 모든 기본 행 집합 작업에 대 한 합니다. 여기에는 행 인출 및 해제, 열 값 가져오기 등이 포함됩니다.  
  
 첫 번째 단계는 일반적으로 사용 하 여 행 집합의 기능을 결정 하는 소비자가 행 집합에 대 한 인터페이스 포인터를 입수 하는 경우는 **irowsetinfo:: Getproperties** 메서드. 그러면 행 집합에서 노출하는 인터페이스에 대한 정보뿐 아니라 별도의 인터페이스로 표시되지 않는 행 집합의 기능(예: 최대 활성 행 수, 동시에 보류 중인 업데이트를 포함할 수 있는 행 수)도 반환됩니다.  
  
 다음 단계로 소비자는 행 집합에 있는 열의 특징, 즉 메타데이터를 확인합니다. 이 사용 하는 **IColumnsInfo** 단순 열 정보에 대 한 메서드 또는 **IColumnsRowset** 확장된 열 정보의 대 한 메서드. **GetColumnInfo** 메서드 다음 정보를 반환 합니다.  
  
-   결과 집합 내의 열 수  
  
-   열당 하나씩, DBCOLUMNINFO 구조의 배열  
  
     구조의 순서는 열이 행 집합에 나타나는 순서입니다. 각 DBCOLUMNINFO 구조에는 열 이름, 열의 서수, 열에 있는 값의 가능한 최대 길이, 열의 데이터 형식, 전체 자릿수 및 길이와 같은 열 메타데이터가 포함됩니다.  
  
-   단일 할당 블록 내 모든 문자열 값의 저장소에 대한 포인터  
  
 소비자는 메타데이터에서 또는 행 집합을 생성한 텍스트 명령을 기반으로 필요한 열을 확인합니다. 반환 된 열 정보의 순서에서 필요한 열의 서 수를 결정 **IColumnsInfo** 순서나에서 반환 되는 열 메타 데이터 행 집합의 **IColumnsRowset**합니다.  
  
 **IColumnsInfo** 및 **IColumnsRowset** 인터페이스는 행 집합의 열에 대 한 정보를 추출 하는 데 사용 됩니다. **IColumnsInfo** 인터페이스 제한 된 집합의 정보를 반환 하는 반면 **IColumnsRowset** 모든 메타 데이터를 제공 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 및 이전 버전에서 반환 된 선택적 메타 데이터 열 DBCOLUMN_COMPUTEMODE **icolumnsinfo:: Getcolumnsinfo** (열이 있는지 여부를 설명 하는 값 대신 DBSTATUS_S_ISNULL을 반환 합니다. 계산) 기본 열이 계산 되 고 있는지 여부를 확인할 수 없습니다.  
  
 서수는 열에 대한 바인딩을 지정하는 데 사용됩니다. 바인딩은 소비자 구조의 요소를 열과 연결하는 구조입니다. 바인딩은 열의 데이터 값, 길이 및 상태 값을 바인딩할 수 있습니다.  
  
 바인딩 집합은 하나의 접근자로 수집되며, 이 사용 하 여 만들어집니다는 **iaccessor:: Createaccessor** 메서드. 단일 호출에서 여러 열의 데이터를 검색하거나 설정할 수 있도록 한 접근자에 여러 바인딩이 포함될 수 있습니다. 소비자는 각 응용 프로그램 부분의 서로 다른 사용 패턴에 일치하는 여러 접근자를 만들 수 있으며, 행 집합을 유지하는 동시에 접근자를 만들고 해제할 수 있습니다.  
  
 데이터베이스에서 행을 인출 수 소비자는와 같은 메서드를 호출 **irowset:: Getnextrows** 또는 **irowsetlocate:: Getrowsat**합니다. 이러한 인출 작업은 서버의 행 데이터를 공급자의 행 버퍼에 배치합니다. 소비자는 공급자의 행 버퍼에 직접 액세스할 수 없습니다. 소비자는 **irowset:: Getdata** 소비자 버퍼에 데이터 공급자의 버퍼를 복사 하려면 및 **irowsetchange:: Setdata** 소비자 버퍼의 데이터 변경 내용을 공급자 버퍼로 복사할 합니다.  
  
 호출 하 여 소비자는 **GetData** 메서드 하 고 행, 접근자에 대 한 핸들 및 소비자 할당 버퍼에 대 한 포인터에 핸들을 전달 합니다. **GetData** 데이터를 변환 하 고 접근자를 만드는 데 바인딩에 지정 된 대로 열을 반환 합니다. 소비자는 호출할 수 **GetData** 가 행을 한 번 동일한 데이터의 여러 복사본을 가져올 수 있습니다 다른 접근자 및 버퍼 따라서 소비자를 사용 하 여 합니다.  
  
 가변 길이 열의 데이터는 몇 가지 방법으로 처리할 수 있습니다. 첫째, 이러한 열을 소비자 구조의 한정된 섹션에 바인딩할 수 있습니다. 이 경우 데이터 길이가 버퍼 길이를 초과하면 잘림이 발생합니다. 소비자는 DBSTATUS_S_TRUNCATED 상태를 검사하여 잘림이 발생했는지 확인할 수 있습니다. 소비자가 잘린 데이터 양도 확인할 수 있도록 반환된 길이는 항상 실제 길이(바이트)입니다.  
  
 마치면 소비자 인출 또는 행이 업데이트를 사용 하 여 해제는 **ReleaseRows** 메서드. 이렇게 하면 행 집합에 있는 행의 복사본에서 리소스가 해제되고 새 행을 위한 공간이 만들어집니다. 그런 후에 소비자는 행을 인출하거나 만들고 행의 데이터에 액세스하는 주기를 반복할 수 있습니다.  
  
 소비자가 행 집합을 완료 된 경우 호출 하는 **iaccessor:: Releaseaccessor** 메서드를 접근자를 해제 합니다. 호출 된 **iunknown:: Release** 행 집합을 해제 하는 행 집합에 의해 노출 되는 모든 인터페이스에서 메서드. 행 집합이 해제되면 소비자는 보유한 나머지 행이나 접근자를 강제로 해제합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [다음 인출 위치](../../relational-databases/native-client-ole-db-rowsets/fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>관련 항목:  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
