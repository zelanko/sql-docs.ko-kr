---
title: Microsoft Connector for Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca25b7425ce74cea820e295a6a99bc3a3c1e2817
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75755848"
---
# <a name="microsoft-connector-for-teradata-preview"></a>Microsoft Connector for Teradata(미리 보기)
[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Microsoft Connector for Teradata를 사용하면 SSIS 패키지의 Teradata 데이터베이스에 데이터를 로드하고 데이터를 내보낼 수 있습니다.

이 새로운 커넥터는 1MB 사용 테이블이 포함된 데이터베이스를 지원합니다.

## <a name="version-support"></a>버전 지원

Microsoft Connector for Teradata에서 지원하는 Microsoft SQL Server 제품은 다음과 같습니다.

- Microsoft SQL Server 2019
- SSDT(Microsoft SQL Server Data Tools)

Microsoft Connector for Teradata는 Teradata Parallel Transporter 애플리케이션 프로그래밍 언어 인터페이스를 사용하여 Teradata 데이터베이스에 데이터를 로드하고 내보냅니다. 지원되는 버전은 다음과 같습니다.

- Teradata PT(Teradata Parallel Transporter) 16.10
- Teradata PT(Teradata Parallel Transporter) 16.20

지원되는 데이터 원본의 Teradata 데이터베이스 버전은 다음과 같습니다.

- Teradata 데이터베이스 16.20
- Teradata 데이터베이스 16.10
- Teradata 데이터베이스 15.10
- Teradata 데이터베이스 15.00

Teradata Parallel Transporter 애플리케이션 프로그래밍 인터페이스 프로그래머 가이드에 대한 자세한 내용은 [Teradata 문서](https://docs.teradata.com/)를 참조하세요.

## <a name="installation"></a>설치

### <a name="prerequisite"></a>필수 요소

32비트 컴퓨터에서는 [Teradata 도구 및 유틸리티 - Windows 설치 패키지](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package)를 통해 다음 드라이버를 설치합니다.

- Teradata ODBC 드라이버(32비트)
- Teradata PT API(32비트)

64비트 컴퓨터에서는 다음 드라이버를 설치합니다.

- Teradata ODBC 드라이버(64비트)
- Teradata PT API(64비트)

Teradata 데이터베이스용 커넥터를 설치하려면 [최신 버전의 Microsoft Connector for Teradata](https://www.microsoft.com/download/details.aspx?id=100599)에서 설치 관리자를 다운로드하여 실행합니다. 그런 다음 설치 마법사의 지시를 따릅니다.

커넥터를 설치한 후에는 SQL Server Integration Services를 다시 시작해야 Teradata 원본 및 대상이 제대로 작동합니다.

SQL Server 2017 및 이전 버전을 대상으로 하는 SSIS 패키지를 실행하려면 아래 링크에서 해당 버전과 함께 **Microsoft Connector for Teradata by Attunity**를 설치해야 합니다.

- [SQL Server 2017: Microsoft Connector Version 5.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016: Microsoft Connector Version 4.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014: Microsoft Connector Version 3.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012: Microsoft Connector Version 2.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

## <a name="uninstallation"></a>제거

제거 마법사를 실행하여 **Microsoft connector for Teradata**를 제거할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Teradata 연결 관리자](teradata-connection-manager.md) 구성
- [Teradata 원본](teradata-source.md) 구성
- [Teradata 대상](teradata-destination.md) 구성
- 질문이 있는 경우 [Tech Community](https://aka.ms/AA6iwdw)를 방문하세요.
