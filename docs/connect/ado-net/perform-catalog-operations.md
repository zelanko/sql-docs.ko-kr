---
title: 카탈로그 작업 수행
description: 데이터베이스 스키마를 수정하는 명령을 실행하는 방법을 설명합니다.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: e60f542f-6271-495b-a9e4-48553481c2a3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 85e68bd77b11fd70e4071d7ae67ebf26c643b540
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428241"
---
# <a name="performing-catalog-operations"></a>카탈로그 작업 수행

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

데이터베이스 또는 카탈로그를 수정하는 CREATE TABLE 또는 CREATE PROCEDURE 문과 같은 명령을 실행하려면 적절한 SQL 문과 **Connection** 개체를 사용하여 **Command** 개체를 만듭니다. <xref:Microsoft.Data.SqlClient.SqlCommand> 개체의 <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> 메서드를 사용하여 명령을 실행합니다.

## <a name="example"></a>예

다음 코드 예제에서는 Microsoft SQL Server 데이터베이스에 저장 프로시저를 만듭니다.

[!code-csharp[DataWorks SqlCommand.ExecuteNonQuery#3](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery_SP_DML.cs#3)]

## <a name="see-also"></a>참조

- [명령을 사용하여 데이터 수정](use-commands-to-modify-data.md)
- [명령 및 매개 변수](commands-parameters.md)
