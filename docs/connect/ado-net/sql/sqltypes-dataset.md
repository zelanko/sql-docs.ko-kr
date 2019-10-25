---
title: SqlTypes 및 데이터 세트
description: 데이터 집합의 SqlTypes에 대 한 형식 지원을 설명 합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 70efb8615a70677c709abd6d9129c63de9420ffc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451987"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes 및 데이터 세트

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ADO.NET 2.0는 <xref:System.Data.SqlTypes> 네임 스페이스를 통해 `DataSet`에 대 한 향상 된 형식 지원을 도입 했습니다. <xref:System.Data.SqlTypes>의 형식은 SQL Server 데이터베이스의 데이터 형식과 의미 체계 및 정밀도가 동일한 데이터 형식을 제공하도록 디자인되었습니다. <xref:System.Data.SqlTypes>의 각 데이터 형식은 SQL Server의 데이터 형식과 동일하며 기본 데이터 표현도 같습니다.  
  
@No__t_1에서 직접 <xref:System.Data.SqlTypes>를 사용 하면 SQL Server 데이터 형식으로 작업 하는 경우 여러 이점이 권한을 부여. <xref:System.Data.SqlTypes>는 SQL Server 네이티브 데이터 형식과 동일한 의미 체계를 지원 합니다. @No__t_1 정의에서 <xref:System.Data.SqlTypes> 중 하나를 지정 하면 decimal 또는 numeric 데이터 형식을 CLR (공용 언어 런타임) 데이터 형식 중 하나로 변환할 때 발생할 수 있는 전체 자릿수가 손실 됩니다.  

다음 예지에서는 <xref:System.Data.DataTable> 개체를 만들고 CLR 형식 대신 <xref:System.Data.SqlTypes>를 사용하여 <xref:System.Data.DataColumn> 데이터 형식을 명시적으로 정의합니다. 이 코드는 SQL Server의 AdventureWorks 데이터베이스에 있는 Sales.SalesOrderDetail 테이블의 데이터로 <xref:System.Data.DataTable>을 채웁니다. 콘솔 창에 표시 되는 출력에는 각 열의 데이터 형식 및 SQL Server에서 검색 된 값이 표시 됩니다.  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
