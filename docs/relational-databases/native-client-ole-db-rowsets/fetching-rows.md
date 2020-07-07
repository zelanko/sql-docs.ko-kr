---
title: 행 페치 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 5e6dbe36-b682-464d-adfa-8e886f9bd452
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f74d247ef06762d4ca5a9533e04b784aac4c477a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007871"
---
# <a name="fetching-rows"></a>행 인출
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **IRowset** 인터페이스는 기본 행 집합 인터페이스입니다. **IRowset** 인터페이스는 순차적으로 행을 인출하고, 해당 행에서 데이터를 가져오고, 행을 관리하기 위한 메서드를 제공합니다. 소비자는 모든 기본 행 집합 작업에 **IRowset**의 메서드를 사용합니다. 여기에는 행 인출 및 해제, 열 값 가져오기 등이 포함됩니다.  
  
 소비자가 행 집합에 인터페이스 포인터를 가져온 경우 첫 번째 단계로 **IRowsetInfo::GetProperties** 메서드를 사용하여 행 집합의 기능을 확인하는 것이 일반적입니다. 그러면 행 집합에서 노출하는 인터페이스에 대한 정보뿐 아니라 별도의 인터페이스로 표시되지 않는 행 집합의 기능(예: 최대 활성 행 수, 동시에 보류 중인 업데이트를 포함할 수 있는 행 수)도 반환됩니다.  
  
 다음 단계로 소비자는 행 집합에 있는 열의 특징, 즉 메타데이터를 확인합니다. 이러한 목적을 위해 소비자는 단순 열 정보의 경우 **IColumnsInfo** 메서드를 사용하고 확장 열 정보의 경우 **IColumnsRowset** 메서드를 사용합니다. **GetColumnInfo** 메서드는 다음과 같은 정보를 반환합니다.  
  
-   결과 집합 내의 열 수  
  
-   열당 하나씩, DBCOLUMNINFO 구조의 배열  
  
     구조의 순서는 열이 행 집합에 나타나는 순서입니다. 각 DBCOLUMNINFO 구조에는 열 이름, 열의 서수, 열에 있는 값의 가능한 최대 길이, 열의 데이터 형식, 전체 자릿수 및 길이와 같은 열 메타데이터가 포함됩니다.  
  
-   단일 할당 블록 내 모든 문자열 값의 스토리지에 대한 포인터  
  
 소비자는 메타데이터에서 또는 행 집합을 생성한 텍스트 명령을 기반으로 필요한 열을 확인합니다. **IColumnsInfo**에서 반환된 열 정보의 순서나 **IColumnsRowset**에서 반환된 열 메타데이터 행 집합의 서수에서 필요한 열의 서수를 확인합니다.  
  
 **IColumnsInfo** 및 **IColumnsRowset** 인터페이스는 행 집합의 열에 대한 정보를 추출하는 데 사용됩니다. **IColumnsInfo** 인터페이스는 제한된 정보 집합을 반환하는 반면 **IColumnsRowset**는 모든 메타데이터를 제공합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 이전 버전의 경우 **IColumnsInfo::GetColumnsInfo**에서 반환된 선택적 메타데이터 열인 DBCOLUMN_COMPUTEMODE는 기본 열의 계산 여부를 확인할 수 없으므로 열 계산 여부를 설명하는 값 대신 DBSTATUS_S_ISNULL을 반환합니다.  
  
 서수는 열에 대한 바인딩을 지정하는 데 사용됩니다. 바인딩은 소비자 구조의 요소를 열과 연결하는 구조입니다. 바인딩은 열의 데이터 값, 길이 및 상태 값을 바인딩할 수 있습니다.  
  
 바인딩 집합은 하나의 접근자로 수집되며, **IAccessor::CreateAccessor** 메서드를 사용하여 만들어집니다. 단일 호출에서 여러 열의 데이터를 검색하거나 설정할 수 있도록 한 접근자에 여러 바인딩이 포함될 수 있습니다. 소비자는 각 애플리케이션 부분의 서로 다른 사용 패턴에 일치하는 여러 접근자를 만들 수 있으며, 행 집합을 유지하는 동시에 접근자를 만들고 해제할 수 있습니다.  
  
 데이터베이스에서 행을 인출하기 위해 소비자는 **IRowset::GetNextRows** 또는 **IRowsetLocate::GetRowsAt**과 같은 메서드를 호출합니다. 이러한 인출 작업은 서버의 행 데이터를 공급자의 행 버퍼에 배치합니다. 소비자는 공급자의 행 버퍼에 직접 액세스할 수 없습니다. 소비자는 **IRowset::GetData**를 사용하여 공급자 버퍼의 데이터를 소비자 버퍼로 복사하고, **IRowsetChange::SetData**를 사용하여 소비자 버퍼의 데이터 변경 내용을 공급자 버퍼로 복사합니다.  
  
 소비자는 **GetData** 메서드를 호출하고 행에 대한 핸들, 접근자에 대한 핸들 및 소비자 할당 버퍼에 대한 포인터를 전달합니다. **GetData**는 데이터를 변환하고 접근자를 만드는 데 사용된 바인딩에서 지정된 열을 반환합니다. 소비자는 다른 접근자 및 버퍼를 사용하여 한 행에 대해 **GetData**를 여러 번 호출할 수 있으므로 동일한 데이터의 여러 복사본을 가져올 수 있습니다.  
  
 가변 길이 열의 데이터는 몇 가지 방법으로 처리할 수 있습니다. 첫째, 이러한 열을 소비자 구조의 한정된 섹션에 바인딩할 수 있습니다. 이 경우 데이터 길이가 버퍼 길이를 초과하면 잘림이 발생합니다. 소비자는 DBSTATUS_S_TRUNCATED 상태를 검사하여 잘림이 발생했는지 확인할 수 있습니다. 소비자가 잘린 데이터 양도 확인할 수 있도록 반환된 길이는 항상 실제 길이(바이트)입니다.  
  
 소비자는 행 인출이나 업데이트를 마친 후 **ReleaseRows** 메서드를 사용하여 행을 해제합니다. 이렇게 하면 행 집합에 있는 행의 복사본에서 리소스가 해제되고 새 행을 위한 공간이 만들어집니다. 그런 후에 소비자는 행을 인출하거나 만들고 행의 데이터에 액세스하는 주기를 반복할 수 있습니다.  
  
 행 집합을 마치면 소비자는 **IAccessor::ReleaseAccessor** 메서드를 호출하여 접근자를 해제합니다. 행 집합이 노출하는 모든 인터페이스에서 **IUnknown::Release** 메서드를 호출하여 행 집합을 해제합니다. 행 집합이 해제되면 소비자는 보유한 나머지 행이나 접근자를 강제로 해제합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [다음 인출 위치](../../relational-databases/native-client-ole-db-rowsets/fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>참고 항목  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
