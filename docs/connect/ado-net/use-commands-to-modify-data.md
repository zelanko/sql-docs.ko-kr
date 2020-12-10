---
title: 명령을 사용하여 데이터 수정
description: 데이터 공급자를 사용하여 저장 프로시저 또는 DDL(데이터 정의 언어) 문을 실행하는 방법을 설명합니다.
ms.date: 11/25/2020
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 98127e41b5b07c38030ef27214c9c92bf7c4b4be
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761481"
---
# <a name="using-commands-to-modify-data"></a>명령을 사용하여 데이터 수정

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient Data Provider for SQL Server를 사용하면 저장 프로시저 또는 데이터 정의 언어 문(예: CREATE TABLE 및 ALTER COLUMN)을 실행하여 데이터베이스 또는 카탈로그에서 스키마 조작을 수행할 수 있습니다. 이러한 명령은 쿼리에서처럼 행을 반환하지 않으므로 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체가 <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>를 제공하여 행을 처리합니다.

**ExecuteNonQuery** 메서드를 사용하면 스키마를 수정하는 것 외에, 데이터를 수정하지만 행을 반환하지 않는 INSERT, UPDATE, DELETE 등의 SQL 문을 처리할 수도 있습니다.

**ExecuteNonQuery** 메서드는 행을 반환하지 않지만 **Command** 개체의 **Parameters** 컬렉션을 통해 입력 및 출력 매개 변수와 반환 값을 전달하고 반환할 수 있습니다.

## <a name="in-this-section"></a>섹션 내용

[데이터 원본에서 데이터 업데이트](update-data-inside-data-source.md)  
데이터베이스의 데이터를 수정하는 명령 또는 저장 프로시저를 실행하는 방법을 설명합니다.

[카탈로그 작업 수행](perform-catalog-operations.md)  
데이터베이스 스키마를 수정하는 명령을 실행하는 방법을 설명합니다.

## <a name="see-also"></a>참조

- [ADO.NET에서 데이터 검색 및 수정](retrieving-modifying-data.md)
- [명령 및 매개 변수](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
