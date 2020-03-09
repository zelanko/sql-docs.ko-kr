---
title: SqlTypes 및 데이터 세트
description: DataSet의 SqlTypes에 대한 형식 지원을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 0a75aca978847a4e1e54f4933bd6ec7fe708a4e3
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896218"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes 및 데이터 세트

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

ADO.NET 2.0은 <xref:System.Data.SqlTypes> 네임스페이스를 통해 `DataSet`에 대해 강화된 형식 지원을 도입했습니다. <xref:System.Data.SqlTypes>의 형식은 SQL Server 데이터베이스의 데이터 형식과 의미 체계 및 정밀도가 동일한 데이터 형식을 제공하도록 디자인되었습니다. <xref:System.Data.SqlTypes>의 각 데이터 형식은 SQL Server의 데이터 형식과 동일하며 기본 데이터 표현도 같습니다.  
  
SQL Server data 형식을 사용할 때 <xref:System.Data.DataSet>에서 직접 <xref:System.Data.SqlTypes>를 사용하면 다양한 혜택이 주어집니다. <xref:System.Data.SqlTypes>는 SQL Server 기본 데이터 형식과 동일한 의미 체계를 지원합니다. <xref:System.Data.DataColumn>의 정의에서 <xref:System.Data.SqlTypes> 중 하나를 지정하면 10진 또는 숫자 데이터 형식을 공용 언어 런타임(CLR) 데이터 형식으로 변환할 때 발생할 수 있는 정확도 손실이 나타나지 않습니다.  

다음 예지에서는 <xref:System.Data.DataTable> 개체를 만들고 CLR 형식 대신 <xref:System.Data.SqlTypes>를 사용하여 <xref:System.Data.DataColumn> 데이터 형식을 명시적으로 정의합니다. 이 코드는 SQL Server의 AdventureWorks 데이터베이스에 있는 Sales.SalesOrderDetail 테이블의 데이터로 <xref:System.Data.DataTable>을 채웁니다. 콘솔 창에 표시되는 출력은 각 열의 데이터 형식과 SQL Server에서 검색된 값을 표시합니다.  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
