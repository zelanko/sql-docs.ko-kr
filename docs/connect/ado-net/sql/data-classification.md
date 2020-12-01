---
title: SqlClient의 데이터 검색 및 분류
description: SQL Server 데이터베이스에서 데이터 분류를 지원하는지 확인하는 방법 및 SqlDataReader 개체를 통해 데이터 분류 정보에 액세스하는 방법을 설명합니다.
ms.date: 11/23/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 32c4968c4e734abf7bcb4addfde69bbdc5294d1c
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123866"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>SqlClient의 데이터 검색 및 분류

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[데이터 검색 및 분류](../../../relational-databases/security/sql-data-discovery-and-classification.md)는 데이터베이스에서 중요한 데이터를 검색, 분류, 레이블 지정하기 위한 고급 서비스의 집합입니다. SqlClient는 기본 원본이 기능을 지원하는 경우 읽기 전용 데이터 검색 및 분류 정보를 노출하는 API를 제공합니다. 이 정보는 SqlDataReader를 통해 액세스합니다.

Microsoft.Data.SqlClient v2.1.0에서는 데이터 분류의 `Sensitivity Rank` 정보에 대한 지원이 도입되었습니다. `Sensitivity Rank`는 민감도 순위를 정의하는 미리 정의된 값 집합을 기반으로 하는 식별자입니다. Advanced Threat Protection과 같은 다른 서비스에서 순위에 따라 변칙을 검색하는 데 사용됩니다. 이제 Microsoft.Data.SqlClient.DataClassification 네임스페이스에서 다음 데이터 분류 API를 사용할 수 있습니다.

```csharp
// New in Microsoft.Data.SqlClient v2.1.0
public enum SensitivityRank
{
    NOT_DEFINED = -1,
    NONE = 0,
    LOW = 10,
    MEDIUM = 20,
    HIGH = 30,
    CRITICAL = 40
}

public sealed class SensitivityClassification
{
  // Returns the sensitivity rank for the query associated with the active 'SqlDataReader'.
  // New in Microsoft.Data.SqlClient v2.1.0
  public SensitivityRank SensitivityRank;

  // Returns the labels collection for this 'SensitivityClassification' Object
  public ReadOnlyCollection<Label> Labels;

  // Returns the information types collection for this 'SensitivityClassification' Object
  public ReadOnlyCollection<InformationType> InformationTypes;

  // Returns the column sensitivity for this 'SensitivityClassification' Object
  public ReadOnlyCollection<ColumnSensitivity> ColumnSensitivities;
}

public sealed class SensitivityProperty
{
  // Returns the sensitivity rank for this 'SensitivityProperty' Object
  // New in Microsoft.Data.SqlClient v2.1.0
  public SensitivityRank SensitivityRank;

  // Returns the label for this 'SensitivityProperty' Object
  public Label Label;

  // Returns the information type for this 'SensitivityProperty' Object
  public InformationType InformationType;
}

public sealed class Label
{
  // Gets the name for this 'Label' object
  public string Name;

  // Gets the ID for this 'Label' object
  public string Id;
}

public sealed class InformationType
{
  // Gets the name for this 'InformationType' object
  public string Name;

  // Gets the ID for this 'InformationType' object
  public string Id;
}

public sealed class ColumnSensitivity
{
  // Returns the list of sensitivity properties as received from Server for this 'ColumnSensitivity' information      
  public ReadOnlyCollection<SensitivityProperty> SensitivityProperties;
}
```

> [!NOTE]
> Microsoft.Data.SqlClient에서는 SQL Server가 순위가 있는 데이터 분류를 지원하는 경우에만 `Sensitivity Rank` 정보를 읽습니다. 순위 없이 이전 버전의 데이터 분류를 사용하는 서버의 경우 쿼리 순위 값은 "정의되지 않음"입니다.

이 샘플 애플리케이션은 SqlDataReader의 데이터 분류 속성에 액세스하는 방법을 보여 줍니다.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]


**참고 항목**  

 - [SQL Server 기능 및 ADO.NET](sql-server-features-adonet.md)
 - [sys.sensitivity_classifications(Transact-SQL)](../../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)
 - [ADD SENSITIVITY CLASSIFICATION](../../../t-sql/statements/add-sensitivity-classification-transact-sql.md)