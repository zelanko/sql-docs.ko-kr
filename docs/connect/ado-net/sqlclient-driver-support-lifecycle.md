---
title: SqlClient 드라이버 지원 기간
description: 제품 지원 기간 정보가 포함된 페이지입니다.
ms.date: 11/19/2020
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: eef9e81c94c930b9f00689b41339d54a0f0302be
ms.sourcegitcommit: 0c0e4ab90655dde3e34ebc08487493e621f25dda
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96442714"
---
# <a name="sqlclient-driver-support-lifecycle"></a>SqlClient 드라이버 지원 기간

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft.Data.SqlClient 라이브러리는 모든 릴리스에 대한 최신 .NET Core 지원 정책을 준수합니다.

[.NET Core 지원 정책 보기](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)

## <a name="microsoftdatasqlclient-release-cadence"></a>Microsoft.Data.SqlClient 릴리스 주기

새로운 안정적(GA) 릴리스는 버전 1.2부터 6개월마다 정기적으로 게시되며, 그 사이에 2~3개의 미리 보기가 릴리스됩니다. 몇 가지 조건과 고객 응답을 바탕으로 관련자와 유지 관리자가 장기 지원(LTS) 릴리스를 선택합니다.

### <a name="actively-supported-releases"></a>활발하게 지원되는 릴리스

| 버전 | 공식 릴리스 날짜 | 최신 패치 버전 | 패치 릴리스 날짜 | 지원 수준  | 지원 종료 |
| -- | -- | -- | -- | -- | -- |
| 2.1 | 2020년 11월 19일 | 2.1.0 | 2020년 11월 19일 | 현재 | |
| 2.0 | 2020년 6월 16일 | 2.0.1 | 2020년 8월 25일 | 현재 | 2021년 2월 19일 |
| 1.1 | 2019년 11월 20일 | 1.1.3 | 2020년 5월 15일 | LTS | 2022년 11월 21일 |

### <a name="out-of-support-releases"></a>지원되지 않는 릴리스

| 버전 | 최신 패치 릴리스 날짜 | 최신 패치 버전 | 지원 종료됨 |
| -- | -- | -- | -- |
| 1.0 | 2019년 9월 26일 | 1.0.19269.1 | 2020년 2월 20일 |

### <a name="long-term-support-lts-releases"></a>LTS(장기 지원) 릴리스

LTS 릴리스는 첫 릴리스 후 3년 동안 지원됩니다.

### <a name="current-releases"></a>현재 릴리스

현재 릴리스는 이어지는 현재 또는 LTS 릴리스 후 3개월 동안 지원됩니다.

## <a name="sql-version-compatibility-with-microsoftdatasqlclient"></a>SQL 버전의 Microsoft.Data.SqlClient 호환성

|데이터베이스 버전&nbsp;&#8594;<br />&#8595; 드라이버 버전|Azure SQL Database|Azure Synapse Analytics|Azure SQL Managed Instance|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|
|---|---|---|---|---|---|---|---|---|
|2.1|예|예|예|예|예|예|예|예|
|2.0|예|예|예|예|예|예|예|예|
|1.1|예|예|예|예|예|예|예|예|
|1.0|예|예|예|예|예|예|예|예|

## <a name="supported-os-versions"></a>지원된 OS 버전

### <a name="support-for-net-framework-applications"></a>.NET Framework 애플리케이션 지원

Microsoft.Data.SqlClient는 .NET Framework v4.6 이상에서 지원되는 모든 운영 체제를 지원합니다.

[.NET Framework, 시스템 요구 사항](/dotnet/framework/get-started/system-requirements)

### <a name="support-for-net-core-applications"></a>.NET Core 애플리케이션 지원

Microsoft.Data.SqlClient는 .NET Core v2.1 이상에서 지원되는 모든 운영 체제를 지원합니다.

[.NET Core 지원 OS 수명 주기 정책](https://github.com/dotnet/core/blob/master/os-lifecycle-policy.md)

> [!NOTE]
> 세계화 고정 모드는 현재 지원되지 않습니다.
