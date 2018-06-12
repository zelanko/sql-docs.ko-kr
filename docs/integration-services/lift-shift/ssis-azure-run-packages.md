---
title: Azure에서 SSIS 패키지 실행 | Microsoft Docs
ms.description: Provides an overview of the available methods for running packages deployed to Azure SQL Database.
ms.date: 05/29/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4d733b49f8353fc430f90161ef25c352c8cac8f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34586092"
---
# <a name="run-an-ssis-package-in-azure"></a>Azure에서 SSIS 패키지 실행

이 문서에 설명된 옵션 중 하나를 선택하여 Azure SQL Database 서버의 SSISDB 카탈로그 데이터베이스에 배포된 SSIS 패키지를 실행할 수 있습니다. 패키지를 직접 실행하거나 Azure Data Factory 파이프라인의 일부로 패키지를 실행할 수 있습니다. Azure의 SSIS에 대한 개요는 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

- 패키지 직접 실행

  - [SSMS를 사용하여 실행](#ssms)

  - [저장 프로시저를 사용하여 실행](#sproc)

  - [스크립트 또는 코드를 사용하여 실행](#script)

- Azure Data Factory 파이프라인의 일부로 패키지 실행

  - [SSIS 패키지 실행 작업을 사용하여 실행](#exec_activity)

  - [저장 프로시저 작업을 사용하여 실행](#sproc_activity)

> [!NOTE]
> `dtexec.exe`을 사용한 패키지 실행은 Azure에 배포된 패키지를 사용하여 테스트되지 않았습니다.

## <a name="ssms"></a> SSMS를 사용하여 패키지 실행

SSMS(SQL Server Management Studio)에서 SSIS 카탈로그 데이터베이스인 SSISDB에 배포된 패키지를 마우스 오른쪽 단추로 클릭하고, **실행**을 선택하여 **패키지 실행** 대화 상자를 열 수 있습니다. 자세한 내용은 [SSMS(SQL Server Management Studio)를 사용하여 SSIS 패키지 실행](../ssis-quickstart-run-ssms.md)을 참조하세요.

## <a name="sproc"></a> 저장 프로시저를 사용하여 패키지 실행

Azure SQL Database에 연결하고 Transact SQL 코드를 실행할 수 있는 모든 환경에서 다음의 저장 프로시저를 호출하여 패키지를 실행할 수 있습니다.

1. **[catalog].[create_execution]**. 자세한 내용은 [catalog.create_execution](../system-stored-procedures/catalog-create-execution-ssisdb-database.md)를 참조하세요.

2. **[catalog].[set_execution_parameter_value]**. 자세한 내용은 [catalog.set_execution_parameter_value](../system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)를 참조하세요.

3. **[catalog].[start_execution]**. 자세한 내용은 [catalog.start_execution](../system-stored-procedures/catalog-start-execution-ssisdb-database.md)를 참조하세요.

자세한 내용은 다음 예제를 참조하세요.

- [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행](../ssis-quickstart-run-tsql-ssms.md)

- [Transact-SQL을 사용하여 Visual Studio Code에서 SSIS 패키지 실행](../ssis-quickstart-run-tsql-vscode.md)

## <a name="script"></a> 스크립트 또는 코드를 사용하여 패키지 실행

`Microsoft.SQLServer.Management.IntegrationServices` 네임 스페이스에서 `Package` 개체의 `Execute` 메서드를 호출하여 관리되는 API를 호출할 수 있는 모든 개발 환경에서 패키지를 실행할 수 있습니다.

자세한 내용은 다음 예제를 참조하세요.

- [PowerShell을 사용하여 SSIS 패키지 실행](../ssis-quickstart-run-powershell.md)

- [.NET 앱에서 C# 코드가 있는 SSIS 패키지 실행](../ssis-quickstart-run-dotnet.md)

## <a name="exec_activity"></a> SSIS 패키지 실행 작업을 사용하여 패키지 실행

자세한 내용은 [Azure Data Factory에서 SSIS 패키지 실행 작업을 사용하여 SSIS 패키지 실행](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)을 참조하십시오.

## <a name="sproc_activity"></a> 저장 프로시저 작업을 사용하여 패키지 실행

자세한 내용은 [Azure Data Factory에서 저장 프로시저 작업을 사용하여 SSIS 패키지 실행](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)을 참조하십시오.

## <a name="next-steps"></a>다음 단계

Azure에 배포된 SSIS 패키지를 예약하기 위한 옵션을 알아봅니다. 자세한 내용은 [Azure에서 SSIS 패키지 실행 예약](ssis-azure-schedule-packages.md)을 참조하세요.