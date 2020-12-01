---
title: 데이터 검색 및 수정
description: .NET Framework에서 Microsoft SqlClient Data Provider for SQL Server는 데이터를 읽고 업데이트하기 위한 애플리케이션과 데이터 원본 간의 브리지 역할을 합니다.
ms.date: 11/13/2020
ms.assetid: 722e7f87-3691-46c6-87e8-7d159722d675
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: cbe61aafd8dcd1681230c355187a65a231535e00
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126461"
---
# <a name="retrieving-and-modifying-data-in-adonet"></a>ADO.NET에서 데이터 검색 및 수정

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

데이터베이스 애플리케이션의 기본 기능은 데이터 소스에 연결하여 포함된 데이터를 검색하는 것입니다. SqlClient 데이터 공급자는 애플리케이션과 데이터 원본 사이의 다리 역할을 하므로 명령을 실행하고 **DataReader** 또는 **DataAdapter** 를 사용하여 데이터를 검색할 수 있습니다. 모든 데이터베이스 애플리케이션의 한 가지 핵심 기능은 데이터베이스에 저장된 데이터를 업데이트하는 것입니다. Microsoft SqlClient Data Provider for SQL Server에서, 데이터 업데이트에는 **DataAdapter**, <xref:System.Data.DataSet> 및 **Command** 개체 사용이 포함됩니다. 트랜잭션을 사용하는 것도 포함될 수 있습니다.

## <a name="in-this-section"></a>섹션 내용

[데이터 원본에 연결](connecting-to-data-source.md) 데이터 원본에 대한 연결을 설정하는 방법과 연결 이벤트로 작업하는 방법을 설명합니다.

[연결 문자열](connection-strings.md) 연결 문자열 키워드, 보안 정보, 저장 및 검색 등 연결 문자열 사용의 다양한 측면을 설명하는 항목이 포함되어 있습니다.

[연결 풀링](connection-pooling.md) Microsoft SqlClient Data Provider for SQL Server에 대한 연결 풀링을 설명합니다.

## <a name="see-also"></a>참고 항목

- [ADO.NET에서 데이터 형식 매핑](data-type-mappings-ado-net.md)
- [SQL Server 및 ADO.NET](./sql/index.md)
