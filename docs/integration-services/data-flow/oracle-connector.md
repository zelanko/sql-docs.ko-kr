---
title: Microsoft Connector for Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a0ad547d26c86c43b0009cdf20acae33ed7e8ab7
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553237"
---
# <a name="microsoft-connector-for-oracle"></a>Microsoft Connector for Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Microsoft Connector for Oracle를 사용하면 SSIS 패키지에서 Oracle 데이터 원본에서 데이터를 내보내거나 이 원본으로 데이터를 로드할 수 있습니다.

## <a name="version-support"></a>버전 지원

다음 Microsoft SQL Server 제품은 Microsoft Connector for Oracle에서 지원됩니다.

- SQL Server 2019 이상
- SSDT(SQL Server Data Tools)

데이터 원본의 다음 Oracle 데이터베이스 버전이 지원됩니다.

- Oracle 10.x
- Oracle 11.x
- Oracle 12c
- Oracle 18c(Windows 인증 지원 없음)

Oracle 데이터베이스는 모든 운영 체제 및 플랫폼에서 지원됩니다.
> [!NOTE]
>
> SQL Server 2019의 Microsoft Connector for Oracle에는 Oracle 클라이언트가 필요하지 않습니다.

## <a name="installation"></a>설치

SQL Server에서 패키지를 실행해야 하는 경우 [여기](https://www.microsoft.com/en-us/download/details.aspx?id=58228)에서 Microsoft Connector for Oracle 설치 프로그램을 다운로드할 수 있습니다. 그런 다음 설치 마법사의 지시를 따릅니다.

이 커넥터를 설치한 후에는 SQL Server Integration Services를 다시 시작해야 Oracle 원본 및 대상이 제대로 작동합니다.

이 커넥터를 사용하여 패키지를 디자인해야 할 경우 커넥터를 다운로드할 필요가 없습니다. SSDT(SQL Server Data Tools)는 15.9.0 이상 버전에 포함되어 있습니다.

## <a name="uninstallation"></a>제거

제거 마법사를 실행하여 SQL Server에서 Microsoft Connector for Oracle을 제거할 수 있습니다.

## <a name="design-ssis-package-with-previous-version"></a>이전 버전을 사용하여 SSIS 패키지 디자인

버전 15.9.0 이상부터 SSDT에는 Microsoft Connector for Oracle Database가 이미 포함되어 있으므로 SQL Server 2019를 대상으로 하는 SSIS 패키지를 디자인하는 경우에는 설치가 필요하지 않습니다.

SQL Server 2017을 대상으로 하는 SSIS 패키지를 디자인하려면 해당 버전과 함께 Attunity의 Connector for Oracle을 설치해야 합니다.

**다운로드 링크:**

- [SQL Server 2017: Attunity의 Oracle용 Microsoft Connector 버전 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=55179)
- [SQL Server 2016: Attunity의 Oracle용 Microsoft Connector 버전 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=52950)
- [SQL Server 2014: Attunity의 Oracle용 Microsoft Connector 버전 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=44582)
- [SQL Server 2012: Attunity의 Oracle용 Microsoft Connector 버전 2.0](https://www.microsoft.com/en-us/download/details.aspx?id=29283)

## <a name="next-steps"></a>다음 단계

- [Oracle 연결 관리자](oracle-connection-manager.md)를 구성합니다.
- [Oracle 원본](oracle-source.md)을 구성합니다.
- [Oracle 대상](oracle-destination.md)을 구성합니다.
- 질문이 있는 경우 [TechCommunity](https://aka.ms/AA5u35j)을 방문하세요.
