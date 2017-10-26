---
title: "Oracle 및 Teradata by Attunity (SSIS)에 대 한 Microsoft 커넥터 | Microsoft Docs"
ms.date: 05/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 926c0c51b5a55a2869b73666f5620fa56e139cca
ms.openlocfilehash: fd8b0177227167f6caa3417029bb2acb974fe181
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Oracle 및 Teradata by Attunity Integration Services (SSIS)에 대 한 Microsoft 커넥터

By Attunity는 SSIS 패키지에 데이터를 주고 Oracle 또는 Teradata를 로드할 때 성능을 최적화 하는 Integration Services에 대 한 커넥터를 다운로드할 수 있습니다.

## <a name="download-the-latest-attunity-connectors"></a>최신 Attunity 커넥터를 다운로드 합니다.

여기에 연결선의 최신 버전을 가져오기:  
[Oracle 및 Teradata에 대 한 Microsoft 커넥터 v5.0](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>SSIS 도구 상자에 표시 되지 문제-Attunity 커넥터

SSIS 도구 상자에 Attunity 커넥터를 보려면 항상는 대상이 SQL Server Data Tools (SSDT) 버전으로 동일한 버전의 SQL Server 설치 컴퓨터에 커넥터의 버전을 설치 해야 합니다. (또한 해야 이전 버전의 설치 된 커넥터.) 이 요구 사항은 SSIS 프로젝트 및 패키지의 대상으로 지정할 SQL Server의 버전에 독립적인입니다.

예를 들어 최신 버전의 SSDT 설치한 다음 있으면 17 버전의 SSDT 14로 시작 하 여 빌드 번호입니다. 이 버전의 SSDT는 SQL Server 2017에 대 한 지원을 추가합니다. 확인 하 고 Attunity를 사용 하 여 SSIS에서 커넥터 개발-이전 버전의 SQL Server를 대상으로 지정할-버전 5.0 Attunity 커넥터의 최신 버전을 설치 해야 하는 경우에 패키지 합니다. 커넥터의이 버전에는 SQL Server 2017에 대 한 지원을 추가합니다.

SSDT의 Visual Studio에서의 설치 된 버전을 확인 **도움말** | **에 대 한 Microsoft Visual Studio**, 또는 **프로그램 및 기능** 제어판에서. 다음은 다음 표에서 Attunity 커넥터의 해당 버전을 설치 합니다.

|SSDT 버전|SSDT 빌드 번호|대상 SQL Server 버전|커넥터의 필수 버전|
|---------|---------|---------|---------|
|17|시작 하 고 14|SQL Server 2017|[Oracle 및 Teradata에 대 한 Microsoft 커넥터 v5.0](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|시작 하 고 13|SQL Server 2016|[Oracle 및 Teradata에 대 한 Microsoft 커넥터 v4.0](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>다운로드는 최신 SQL Server 데이터 도구 (SSDT)

최신 버전의 SSDT 여기 가져오기:  
[SSDT(SQL Server Data Tools) 다운로드](..//ssdt/download-sql-server-data-tools-ssdt.md)

