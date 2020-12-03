---
title: 데이터 형식 매핑
description: Microsoft SqlClient Data Provider for SQL Server에서 사용하는 데이터 형식에 대해 설명합니다.
ms.date: 11/13/2020
ms.assetid: d4afab94-ada6-4c77-a73c-41f17bae6b5a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 03af2a8544763aab7609fd713790622bbb1bfef4
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419766"
---
# <a name="data-type-mappings-in-adonet"></a>ADO.NET에서 데이터 형식 매핑

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

ADO.NET은 런타임에서 형식을 선언, 사용 및 관리하는 방법을 정의하는 공통 형식 시스템을 기반으로 합니다. .NET Framework는 값 형식과 참조 형식으로 구성되며, 두 형식 모두 <xref:System.Object> 기본 형식에서 파생됩니다. 데이터 소스로 작업할 경우 데이터 형식을 명시적으로 지정하지 않으면 데이터 공급자에서 데이터 형식이 유추됩니다. 예를 들어 <xref:System.Data.DataSet> 개체는 모든 데이터 소스에 대해 독립적입니다. `DataSet`의 데이터는 데이터 소스에서 검색되며 변경 내용은 `DataAdapter`를 사용하여 데이터 소스에 다시 적용됩니다. 이 프로그램 흐름은 `DataAdapter`가 데이터 원본의 값으로 `DataSet`의 <xref:System.Data.DataTable>을 채울 때 `DataTable`에 있는 열의 결과 데이터 형식이 데이터 원본에 연결하는 데 사용되는 Microsoft SqlClient Data Provider for SQL Server에 특정한 형식이 아니라 .NET Framework 형식임을 의미합니다.

마찬가지로 `DataReader`가 데이터 원본에서 값을 반환하면 결과 값은 .NET Framework 유형을 가진 로컬 변수에 저장됩니다. `DataAdapter`의 `Fill` 작업과 `DataReader`의 `Get` 메서드 모두에 대해 .NET Framework 유형은 Microsoft SqlClient Data Provider for SQL Server에서 반환된 값에서 유추됩니다.

반환되는 값의 형식을 알고 있는 경우에는 유추되는 데이터 형식을 사용하는 대신 `DataReader`의 형식화된 접근자 메서드를 사용할 수 있습니다. 형식화된 접근자 메서드는 특정 .NET Framework 형식으로 값을 반환하여 더 나은 성능을 제공하므로 추가 형식 변환이 필요하지 않습니다.

> [!NOTE]
> Microsoft SqlClient Data Provider for SQL Server 데이터 형식의 Null 값은 `DBNull.Value`로 표시됩니다.

## <a name="in-this-section"></a>섹션 내용

[ SQL Server 데이터 형식 매핑 ](sql-server-data-type-mappings.md) <xref:Microsoft.Data.SqlClient>에 대한 유추된 데이터 형식 매핑 및 데이터 접근자 메서드를 나열합니다.

[부동 소수점 숫자](floating-point-numbers.md) 개발자가 부동 소수점 숫자로 작업할 때 자주 발생하는 문제를 설명합니다.

## <a name="see-also"></a>참고 항목

- [SQL Server 데이터 형식 및 ADO.NET](./sql/sql-server-data-types.md)
- [매개 변수 구성](configure-parameters.md)
