---
title: SQL Server 데이터 형식 및 ADO.NET
description: SQL Server 데이터 형식을 사용하는 방법 및 SQL Server 데이터 형식이 .NET 데이터 형식과 상호 작용하는 방식을 설명합니다.
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 50a6e158f5678b30028337b70e1da6914038e64a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896546"
---
# <a name="sql-server-data-types-and-adonet"></a>SQL Server 데이터 형식 및 ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server와 .NET은 서로 다른 형식의 시스템을 기반으로 하기 때문에 데이터가 손실될 수 있습니다. SQL Server용 Microsoft SqlClient Data Provider(<xref:Microsoft.Data.SqlClient>)는 데이터 무결성 유지를 위해 SQL Server 데이터를 사용을 위해 형식화된 접근자 메서드를 제공합니다. 사용자는 <xref:System.Data.SqlDbType> 클래스의 열거형을 사용하여 <xref:Microsoft.Data.SqlClient.SqlParameter> 데이터 형식을 지정할 수 있습니다.  
  
SQL Server 2008에서는 날짜 및 시간, 구조화, 반구조화, 비구조화 데이터를 사용해야 할 비즈니스 요구 사항에 맞게 설계된 새로운 데이터 형식을 소개합니다. 이 내용은 SQL Server 2008 온라인 설명서에 문서화되어 있습니다.  
  
애플리케이션에서 사용할 수 있는 SQL Server 데이터 형식은 사용 중인 SQL Server의 버전에 따라 달라집니다. 자세한 내용은 SQL Server 온라인 설명서에서 [데이터 형식(데이터베이스 엔진)](https://go.microsoft.com/fwlink/?LinkID=107468)을 참조하세요.
  
## <a name="in-this-section"></a>섹션 내용  
[SqlTypes 및 데이터 세트](sqltypes-dataset.md)  
`SqlTypes`의 `DataSet`에 대한 형식 지원에 대해 설명합니다.  
  
[NULL 값 처리](handle-null-values.md)  
null 값과 값이 세 개인 논리로 작업하는 방법에 대해 설명합니다.  
  
[GUID 및 uniqueidentifier 값 비교](compare-guid-uniqueidentifier-values.md)  
SQL Server 및 .NET에서 GUID 및 uniqueidentifier 값을 사용하는 방법을 보여 줍니다.  
  
[날짜 및 시간 데이터](date-time-data.md)  
SQL Server 2008에서 도입된 새 날짜 및 시간 데이터 형식을 사용하는 방법을 설명합니다.  
  
[큰 UDT](large-udts.md)  
SQL Server 2008에 도입된 큰 값의 UDT에서 데이터를 검색하는 방법을 보여 줍니다.  
  
[SQL Server의 XML 데이터](xml-data-sql-server.md)  
SQL Server에서 검색된 XML 데이터를 사용하는 방법을 설명합니다.  
  
## <a name="reference"></a>참조  
<xref:System.Data.DataSet>  
`DataSet` 클래스와 모든 해당 멤버에 대해 설명합니다.  
  
<xref:System.Data.SqlTypes>  
`SqlTypes` 네임스페이스와 모든 해당 멤버에 대해 설명합니다.  
  
<xref:System.Data.SqlDbType>  
`SqlDbType` 열거형과 모든 해당 멤버에 대해 설명합니다.  
  
<xref:System.Data.DbType>  
`DbType` 열거형과 모든 해당 멤버에 대해 설명합니다.  
  
## <a name="next-steps"></a>다음 단계
- [테이블 반환 매개 변수](table-valued-parameters.md)
- [SQL Server 이진 및 큰 값 데이터](sql-server-binary-large-value-data.md)
