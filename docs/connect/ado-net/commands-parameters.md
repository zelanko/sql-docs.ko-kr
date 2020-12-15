---
title: 명령 및 매개 변수
description: Microsoft SqlClient Data Provider for SQL Server의 Command 개체를 사용하여 명령을 실행하고 데이터 원본에서 결과를 반환하는 방법을 알아봅니다.
ms.date: 11/25/2020
ms.assetid: b623f810-d871-49a5-b0f5-078cc3c34db6
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: f899ad41e609874cbcc22c2a3ac959c41574e0eb
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761531"
---
# <a name="commands-and-parameters"></a>명령 및 매개 변수

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

데이터 소스에 대한 연결을 설정한 후에는 <xref:System.Data.Common.DbCommand> 개체를 사용하여 명령을 실행하고 데이터 소스에서 결과를 반환할 수 있습니다. Microsoft SqlClient Data Provider for SQL Server의 명령 생성자 중 하나를 사용하여 명령을 만들 수 있습니다. 생성자는 데이터 소스에서 실행하는 SQL 문, <xref:System.Data.Common.DbConnection> 개체 또는 <xref:System.Data.Common.DbTransaction> 개체와 같은 선택적 인수를 사용할 수 있습니다.

이러한 개체를 명령의 속성으로 구성할 수도 있습니다. 또한 <xref:System.Data.Common.DbConnection.CreateCommand%2A> 개체의 `DbConnection` 메서드를 사용하여 특정 연결에 대한 명령을 만들 수 있습니다. 명령을 통해 실행되는 SQL 문은 <xref:System.Data.Common.DbCommand.CommandText%2A> 속성을 사용하여 구성할 수 있습니다. Microsoft SqlClient Data Provider for SQL Server에는 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체가 있습니다.

## <a name="in-this-section"></a>섹션 내용

[명령 실행](execute-command.md)  
ADO.NET `Command` 개체 및 이 개체를 사용하여 데이터 소스에 대해 쿼리와 명령을 실행하는 방법을 설명합니다.

[매개 변수 구성](configure-parameters.md)  
방향, 데이터 형식 및 매개 변수 구문을 포함하여 `Command` 매개 변수로 작업하는 방법을 설명합니다.

[CommandBuilder를 사용하여 명령 생성](generate-commands-with-commandbuilders.md)  
명령 작성기를 사용하여 단일 테이블 SELECT 명령이 들어 있는 `DataAdapter`에 대해 INSERT, UPDATE 및 DELETE 명령을 자동으로 생성하는 방법을 설명합니다.

[데이터베이스에서 단일 값 가져오기](obtain-single-value-from-database.md)  
`ExecuteScalar` 개체의 `Command` 메서드를 사용하여 데이터베이스 쿼리에서 단일 값을 반환하는 방법을 설명합니다.

[명령을 사용하여 데이터 수정](use-commands-to-modify-data.md)  
Microsoft SqlClient Data Provider for SQL Server를 사용하여 저장 프로시저 또는 DDL(데이터 정의 언어) 문을 실행하는 방법을 설명합니다.

## <a name="see-also"></a>참고 항목

- [데이터 원본에 연결](connecting-to-data-source.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
