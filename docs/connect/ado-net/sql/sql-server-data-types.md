---
title: SQL Server 데이터 형식 및 ADO.NET
description: SQL Server 데이터 형식을 사용하는 방법 및 SQL Server 데이터 형식이 .NET 데이터 형식과 상호 작용하는 방식을 설명합니다.
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 12ad13d6788ae2b8995289100883b06c5ab6d7c6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452029"
---
# <a name="sql-server-data-types-and-adonet"></a>SQL Server 데이터 형식 및 ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server와 .NET은 서로 다른 형식 시스템을 기반으로 하기 때문에 데이터가 손실 될 수 있습니다. 데이터 무결성을 유지 하기 위해 Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>)는 SQL Server 데이터를 사용 하기 위한 형식화 된 접근자 메서드를 제공 합니다. @No__t_0 클래스에서 열거형을 사용 하 여 <xref:Microsoft.Data.SqlClient.SqlParameter> 데이터 형식을 지정할 수 있습니다.  
  
SQL Server 2008에는 날짜 및 시간, 구조적, 반구조적 및 비구조적 데이터를 사용 하는 비즈니스 요구를 충족 하도록 설계 된 새로운 데이터 형식이 도입 되었습니다. 이 내용은 SQL Server 2008 온라인 설명서에 문서화되어 있습니다.  
  
응용 프로그램에서 사용할 수 있는 SQL Server 데이터 형식은 사용 중인 SQL Server 버전에 따라 달라 집니다. 자세한 내용은 SQL Server 온라인 설명서에서 [데이터 형식 (데이터베이스 엔진)](https://go.microsoft.com/fwlink/?LinkID=107468) 을 참조 하세요.
  
## <a name="in-this-section"></a>섹션 내용  
[SqlTypes 및 데이터 세트](sqltypes-dataset.md)  
`DataSet`의 `SqlTypes`에 대한 형식 지원에 대해 설명합니다.  
  
[NULL 값 처리](handle-null-values.md)  
Null 값 및 3 값 논리를 사용 하는 방법을 보여 줍니다.  
  
[GUID 및 uniqueidentifier 값 비교](compare-guid-uniqueidentifier-values.md)  
SQL Server 및 .NET에서 GUID 및 uniqueidentifier 값을 사용 하는 방법을 보여 줍니다.  
  
[날짜 및 시간 데이터](date-time-data.md)  
SQL Server 2008에서 도입 된 새 날짜 및 시간 데이터 형식을 사용 하는 방법을 설명 합니다.  
  
[큰 UDT](large-udts.md)  
SQL Server 2008에 도입 된 대량 값 Udt에서 데이터를 검색 하는 방법을 보여 줍니다.  
  
[SQL Server의 XML 데이터](xml-data-sql-server.md)  
SQL Server에서 검색 된 XML 데이터로 작업 하는 방법에 대해 설명 합니다.  
  
## <a name="reference"></a>참조  
<xref:System.Data.DataSet>  
@No__t_0 클래스와 모든 해당 멤버에 대해 설명 합니다.  
  
<xref:System.Data.SqlTypes>  
@No__t_0 네임 스페이스와 모든 해당 멤버에 대해 설명 합니다.  
  
<xref:System.Data.SqlDbType>  
@No__t_0 열거와 모든 해당 멤버에 대해 설명 합니다.  
  
<xref:System.Data.DbType>  
@No__t_0 열거와 모든 해당 멤버에 대해 설명 합니다.  
  
## <a name="next-steps"></a>다음 단계
- [테이블 반환 매개 변수](table-valued-parameters.md)
- [SQL Server 이진 및 큰 값 데이터](sql-server-binary-large-value-data.md)
