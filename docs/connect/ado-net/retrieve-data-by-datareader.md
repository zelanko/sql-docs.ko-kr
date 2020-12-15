---
title: DataReader로 데이터 검색
description: 이 샘플 코드로 ADO.NET에서 DataReader를 사용하여 데이터를 검색하는 방법을 알아봅니다. DataReader는 버퍼링되지 않은 데이터 스트림을 제공합니다.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 97afc121-fb8b-465b-bab3-6d844420badb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 06bfaa994c2b29959f44cfc554122465db9e0394
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772291"
---
# <a name="retrieve-data-by-a-datareader"></a>DataReader로 데이터 검색

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

**DataReader** 를 사용하여 데이터를 검색하려면 **Command** 개체의 인스턴스를 만든 후 **Command.ExecuteReader** 호출을 통해 **DataReader** 를 만들어 데이터 원본에서 행을 검색합니다. **DataReader** 는 절차적 논리가 데이터 원본의 결과를 효율적이고 순차적으로 처리할 수 있도록 버퍼링되지 않은 데이터 스트림을 제공합니다.

> [!NOTE]
> 대량의 데이터를 검색할 때는 **DataReader** 를 선택하는 것이 좋습니다. 데이터가 메모리에 캐시되지 않기 때문입니다.

다음 예제에서는 **DataReader** 를 사용하는 경우를 보여 줍니다. 여기서 `reader`는 유효한 DataReader를 나타내고 `command`는 유효한 Command 개체를 나타냅니다.  

```csharp
reader = command.ExecuteReader();  
```

쿼리 결과에서 행을 가져오려면 **DataReader.Read** 메서드를 사용합니다. 열의 이름이나 서수를 **DataReader** 에 전달하여 반환된 행의 각 열에 액세스할 수 있습니다. 그러나 최고의 성능을 위해 **DataReader** 는 **GetDateTime**, **GetDouble**, **GetGuid**, **GetInt32** 등의 네이티브 데이터 형식의 열 값에 액세스할 수 있도록 하는 일련의 메서드를 제공합니다. 데이터 공급자별 **DataReader** 의 형식화된 접근자 메서드 목록은 <xref:Microsoft.Data.SqlClient.SqlDataReader>를 참조하세요. 기본 데이터 형식을 알고 있을 때 형식화된 접근자 메서드를 사용하면 열 값을 검색할 때 필요한 형식 변환의 양이 줄어듭니다.  

다음 예제에서는 **DataReader** 개체를 반복하고 각 행에서 두 열을 반환합니다.  

[!code-csharp[DataWorks SqlClient.HasRows#1](~/../sqlclient/doc/samples/SqlDataReader_HasRows.cs#1)]

## <a name="closing-the-datareader"></a>DataReader 닫기  

**DataReader** 개체 사용을 완료하면 항상 **Close** 메서드를 호출합니다.

> [!NOTE]
> **Command** 에 출력 매개 변수나 반환 값이 포함된 경우 이러한 값을 사용하려면 먼저 **DataReader** 를 닫아야 합니다.  

> [!IMPORTANT]
> **DataReader** 가 열려 있는 동안에는 해당 **DataReader** 에서 **Connection** 을 단독으로 사용합니다. 원래 **DataReader** 를 닫아야 다른 **DataReader** 의 생성을 비롯하여 **Connection** 에 대해 명령을 실행할 수 있습니다.  

> [!NOTE]
> **Connection**, **DataReader** 또는 클래스의 **Finalize** 메서드에 있는 다른 모든 관리형 개체에 대해 **Close** 또는 **Dispose** 를 호출하지 마세요. 종료자에서는 클래스에 직접 속한 관리되지 않는 리소스만 해제합니다. 클래스에 비관리형 리소스가 없는 경우 클래스 정의에 **Finalize** 메서드를 포함하지 마세요. 자세한 내용은 [가비지 수집](/dotnet/standard/garbage-collection/index.md)을 참조하세요.
 
## <a name="retrieve-multiple-result-sets-using-nextresult"></a>NextResult를 사용하여 여러 개의 결과 집합 검색

**DataReader** 에서 여러 개의 결과 집합을 반환하는 경우 **NextResult** 메서드를 호출하여 결과 집합을 순차적으로 반복합니다. 다음 예제에서는 <xref:Microsoft.Data.SqlClient.SqlDataReader>가 <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteReader%2A> 메서드를 사용하여 두 가지 SELECT 문 결과를 처리하는 방법을 보여 줍니다.  

[!code-csharp[DataWorks SqlClient.NextResult#1](~/../sqlclient/doc/samples/SqlDataReader_NextResult.cs#1)]

## <a name="get-schema-information-from-the-datareader"></a>DataReader에서 스키마 정보 가져오기  

**DataReader** 가 열려 있는 동안에는 **GetSchemaTable** 메서드를 사용하여 현재 결과 집합에 대한 스키마 정보를 검색할 수 있습니다. **GetSchemaTable** 은 현재 결과 집합에 대한 스키마 정보를 포함하는 행과 열로 채워진 <xref:System.Data.DataTable> 개체를 반환합니다. **DataTable** 은 결과 집합의 열마다 한 행을 포함합니다. 스키마 테이블의 각 열은 결과 집합의 행에 반환된 열의 속성에 매핑됩니다. 여기서 **ColumnName** 은 속성 이름이고 열 값은 속성 값입니다. 다음 예제에서는 **DataReader** 에 대한 스키마 정보를 출력합니다.  

[!code-csharp[DataWorks SqlClient.GetSchemaTable#1](~/../sqlclient/doc/samples/SqlDataReader_GetSchemaTable.cs#1)]

## <a name="see-also"></a>참고 항목

- [DataAdapters 및 DataReaders](dataadapters-datareaders.md)
- [명령 및 매개 변수](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
