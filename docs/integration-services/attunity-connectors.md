---
title: Attunity의 Oracle 및 Teradata용 Microsoft Connectors(SSIS) | Microsoft Docs
ms.date: 08/16/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ''
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 255c526a1de285dcf23c10fb97a6f6bb75a9ae2c
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542241"
---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Integration Services(SSIS)에 대한 Attunity의 Oracle 및 Teradata용 Microsoft Connectors

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

> [!NOTE]
> Oracle 및 Teradata용 Attunity 커넥터는 SQL Server 2017 이하를 지원합니다.
>
> SQL Server 2019에서 Oracle 및 Teradata용 최신 커넥터를 다음 위치에서 다운로드할 수 있습니다.
> - [Microsoft Connector for Oracle](data-flow/oracle-connector.md)
> - [Microsoft Connector for Teradata](data-flow/teradata-connector.md)

SSIS 패키지에서 Oracle 또는 Teradata 간 데이터를 로드할 때 성능을 최적화하는 Attunity의 Integration Services에 대한 커넥터를 다운로드할 수 있습니다.

## <a name="download-the-latest-attunity-connectors"></a>최신 Attunity 커넥터 다운로드

여기에서 최신 버전의 커넥터를 가져옵니다.  
[Oracle 및 Teradata용 Microsoft Connectors v5.0](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>문제 - SSIS 도구 상자에 Attunity 커넥터가 표시되지 않음

SSIS 도구 상자에서 Attunity 커넥터를 보려면 컴퓨터에 설치된 대상이 SSDT(SQL Server Data Tools)의 버전으로 동일한 버전의 SQL Server를 대상으로 하는 커넥터의 버전을 항상 설치해야 합니다. (또한 이전 버전의 커넥터를 설치했을 수도 있습니다.) 이 요구 사항은 SSIS 프로젝트 및 패키지에서 대상으로 하려는 SQL Server의 버전의 영향을 받지 않습니다.

예를 들어 최신 버전의 SSDT를 설치한 경우 14로 시작하는 빌드 번호로 버전 17의 SSDT를 갖습니다. 이 버전의 SSDT는 SQL Server 2017에 대한 지원을 추가합니다. 이전 버전의 SQL Server를 대상으로 하는 경우에도 SSIS 패키지 개발에서 Attunity 커넥터를 확인하고 사용하려면 최신 버전의 Attunity 커넥터, 버전 5.0을 설치해야 합니다. 이 버전의 커넥터는 SQL Server 2017에 대한 지원도 추가합니다.

**도움말** | **Microsoft Visual Studio 정보**의 Visual Studio 또는 제어판의 **프로그램 및 기능**에서 설치된 SSDT의 버전을 확인합니다. 그런 다음 아래 표에서 Attunity 커넥터의 해당 버전을 설치합니다.

|SSDT 버전|SSDT 빌드 번호|대상 SQL Server 버전|커넥터의 필수 버전|
|---------|---------|---------|---------|
|17|14로 시작|SQL Server 2017|[Oracle 및 Teradata용 Microsoft Connectors v5.0](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|13으로 시작|SQL Server 2016|[Oracle 및 Teradata용 Microsoft Connectors v4.0](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>최신 SSDT(SQL Server Data Tools) 다운로드

여기에서 최신 버전의 SSDT를 가져옵니다.  
[SSDT(SQL Server Data Tools) 다운로드](..//ssdt/download-sql-server-data-tools-ssdt.md)
