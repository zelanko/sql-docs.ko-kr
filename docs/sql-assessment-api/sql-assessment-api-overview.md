---
title: SQL Server 평가 API
description: SQL Server 평가 API란 무엇인지 설명합니다.
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: 76a6e99d06061ae581b753ce0edd96a5a82d0f95
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78946715"
---
# <a name="sql-assessment-api"></a>SQL 평가 API

SQL 평가 API는 모범 사례에 대해 SQL Server 구성을 평가하는 메커니즘을 제공합니다. 이 API는 SQL Server 팀에서 제안하는 모범 사례 규칙을 포함하는 규칙 집합과 함께 제공됩니다. 이 규칙 집합은 새 버전 릴리스로 향상되지만, 이와 동시에 API는 사용자 지정 가능하고 확장 가능한 솔루션을 제공하기 위한 목적으로 빌드됩니다. 따라서 사용자는 기본 규칙을 조정하고 자체 규칙을 직접 만들 수 있습니다.

SQL 평가 API는 SQL Server 구성이 권장되는 모범 사례를 따르는지 확인하려는 경우에 유용합니다. 초기 평가 후에는 정기적으로 예약된 평가를 통해 구성 안정성을 추적할 수 있습니다.

이 API를 사용하여 Azure SQL Database Managed Instance 및 SQL Server 버전 2012 이상을 평가할 수 있습니다. Linux의 SQL이 지원됩니다.

## <a name="rules"></a>규칙

검사라고도 하는 규칙은 JSON 형식 파일에 정의되어 있습니다. 규칙 집합 형식에는 규칙 집합 이름 및 버전을 지정해야 합니다. 따라서 사용자 지정 규칙 집합을 사용하는 경우 어떤 규칙 집합이 어떤 권장 사항을 제공하는지 쉽게 알 수 있습니다. 

Microsoft에서 제공하는 규칙 집합은 GitHub에서 이용할 수 있습니다. 자세한 내용은 [샘플 리포지토리](https://aka.ms/sql-assessment-api)를 참조하세요.

## <a name="sql-assessment-cmdlets-and-smo-extension"></a>SQL 평가 cmdlet 및 SMO 확장

SQL 평가 API는 [SMO(SQL Server 관리 개체)](../relational-databases/server-management-objects-smo/installing-smo.md) 2019년 7월 릴리스 버전 이상 및 [SQL Server PowerShell 모듈](../powershell/download-sql-server-ps-module.md) 2019년 7월 릴리스 버전 이상에 포함되어 있습니다.

* [SMO 설치](../relational-databases/server-management-objects-smo/installing-smo.md)

* [SQL Server PowerShell 모듈 설치](../powershell/download-sql-server-ps-module.md)

SqlServer 모듈이 SQL 평가 API를 사용하는 두 개의 새 cmdlet을 가져옵니다.

* **Get-SqlAssessmentItem** – SQL Server 개체에 사용 가능한 평가 검사 목록을 제공합니다.

* **Invoke-SqlAssessment** – 평가 결과를 제공합니다.

SMO 프레임워크는 다음 메서드를 제공하는 SQL 평가 API 확장을 통해 보완됩니다.

* **GetAssessmentItems** – 특정 SQL 개체에 사용 가능한 검사를 반환합니다(IEnumerable<…>).

* **GetAssessmentResults** – 평가를 동기적으로 평가하고 결과 및 오류(있을 경우)를 반환합니다(IEnumerable<…>).

* **GetAssessmentResultsList** – 평가를 비동기적으로 평가하고 결과 및 오류(있을 경우)를 반환합니다(Task<…>).

## <a name="get-started-using-sql-assessment-cmdlets"></a>SQL 평가 cmdlet 사용

평가는 선택한 SQL Server 개체에 대해 수행됩니다. 기본 규칙 집합에는 두 가지 개체, 즉 서버 및 데이터베이스(이밖에 API는 파일 그룹 및 가용성 그룹을 추가로 지원)에 대한 검사만 있습니다. 한 SQL 인스턴스와 그 안의 모든 데이터베이스를 평가하려는 경우에는 각 개체에 대해 SQL 평가 cmdlet을 별도로 실행해야 합니다. 또는, 평가할 개체를 변수 또는 파이프라인으로 SQL 평가 cmdlet에 전달할 수 있습니다.

SqlServer 및 RegisteredServer 개체는 서로 교환할 수 있으므로 아무 개체나 SQL 평가 cmdlet에 전달할 수 있습니다.

시작하려면 아래 예제를 참조하세요.

1. 로컬 기본 인스턴스에 대해 사용 가능한 검사 목록을 확인하여 검사를 숙지합니다. 이 예제에서는 Get-SqlInstance cmdlet의 출력을 SqlAssessmentItem cmdlet으로 파이프하여 인스턴스 개체를 전달합니다.

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

2. 인스턴스의 모든 데이터베이스에 대해 사용 가능한 검사 목록을 가져옵니다. 여기서는 Get-Item cmdlet과 Windows PowerShell SQL Server 공급자로 구현된 경로를 사용하여 데이터베이스 목록을 가져온 다음, Get-SqlDatabase cmdlet으로 파이핑합니다.

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```

    또한 Get-SqlDatabase cmdlet을 사용하여 동일한 작업을 수행할 수 있습니다.

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

3. 인스턴스의 모든 데이터베이스에 대해 사용 가능한 검사 목록을 가져옵니다. 여기서는 Get-Item cmdlet과 Windows PowerShell SQL Server 공급자로 구현된 경로를 사용하여 데이터베이스 목록을 가져온 다음, Get-SqlDatabase cmdlet으로 파이핑합니다.

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```

    또한 Get-SqlDatabase cmdlet을 사용하여 동일한 작업을 수행할 수 있습니다.

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

4. 인스턴스에 대한 평가를 호출하고 결과를 SQL 테이블에 저장합니다. 이 예제에서는 Get-SqlInstance cmdlet의 출력을 Invoke-SqlAssessment cmdlet으로 파이프하고, 해당 결과는 Write-SqlTableData cmdlet으로 파이프됩니다. 이 예제에서는 `-FlattenOutput` 매개 변수를 사용하여 Invoke-Assessment cmdlet을 실행합니다. 이 매개 변수는 출력을 Write-SqlTableData cmdlet에 적합하게 만듭니다. 매개 변수를 생략하면 오류가 발생합니다.

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

    이제 인스턴스의 모든 데이터베이스에 대한 평가를 호출하고 결과를 동일한 표에 추가해 보겠습니다.

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

5. 권장 사항을 보다 자세히 이해하려면 표의 설명 및 링크를 따르세요.

6. 사용자 환경 및 조직 요구 사항에 따라 규칙을 사용자 지정합니다(아래 참조).

7. 태스크 또는 작업을 예약하여 정기적으로 또는 요청 시 평가를 실행하여 진행률을 측정합니다.

## <a name="customizing-rules"></a>규칙 사용자 지정

규칙은 사용자 지정이 가능하고 확장 가능하도록 설계되었습니다. Microsoft의 규칙 집합은 대부분의 환경에서 작동하도록 설계되었습니다. 그러나 모든 개별 환경에 유효한 단일 규칙 집합이란 불가능합니다. 사용자는 자신의 JSON 파일을 작성하고 기존 규칙을 사용자 지정하거나 새 규칙을 추가할 수 있습니다. 사용자 지정 예제 및 Microsoft에서 릴리스한 전체 규칙 집합은 [샘플 리포지토리](https://aka.ms/sql-assessment-api)에서 이용할 수 있습니다. 사용자 지정 JSON 파일을 사용하여 SQL 평가 cmdlet을 실행하는 방법에 대한 자세한 내용을 알아보려면 Get-Help cmdlet을 사용합니다.

### <a name="options-available-with-rule-customization-feature"></a>규칙 사용자 지정 기능에 사용할 수 있는 옵션

#### <a name="enablingdisabling-certain-rules-or-groups-of-rules-using-tags"></a>특정 규칙 또는 규칙 그룹 사용/사용 안 함(태그 사용)

사용자 환경에 적용되지 않거나 예약된 작업을 수행하여 문제를 해결할 때까지 특정 규칙을 대기 상태로 설정할 수 있습니다.

#### <a name="changing-threshold-parameters"></a>임계값 매개 변수 변경

특정 규칙에는 문제를 찾기 위해 메트릭의 현재 값과 비교되는 임계값이 있습니다. 기본 임계값이 적합하지 않는 경우 변경할 수 있습니다.

#### <a name="adding-more-rules-written-by-you-or-third-parties"></a>사용자 또는 제3자가 작성한 규칙 추가

하나 이상의 JSON 파일을 SQL 평가 API 호출에 매개 변수로 추가하여 규칙 집합을 함께 지정할 수 있습니다. 조직에서 해당 파일을 작성하거나 타사에서 가져올 수 있습니다. 예를 들어 Microsoft 규칙 집합에서 특정 규칙을 사용하지 않도록 설정하는 JSON 파일을 사용하고 사용자 환경에 유용한 규칙을 포함하는 업계 전문가의 JSON 파일을 또 하나 사용하여 자체 JSON 파일에서 일부 임계값을 변경할 수 있습니다.

> [!IMPORTANT]  
> 신뢰할 수 없는 소스에서 제공되는 규칙 집합은 철저히 검토하여 안전성이 확인되기 전에는 사용하지 않아야 합니다.

## <a name="next-steps"></a>다음 단계

[SMO(SQL Server 관리 개체)](../relational-databases/server-management-objects-smo/overview-smo.md) 및 [PowerShell](../powershell/download-sql-server-ps-module.md)을 살펴보세요.
