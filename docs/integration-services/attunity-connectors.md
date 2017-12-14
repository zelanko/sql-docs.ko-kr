---
title: "Attunity의 Oracle 및 Teradata용 Microsoft Connectors(SSIS) | Microsoft Docs"
ms.date: 05/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d7e5ca02e2e4f7ee2e1a2e7044f522048a6fb196
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Integration Services(SSIS)에 대한 Attunity의 Oracle 및 Teradata용 Microsoft Connectors

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
