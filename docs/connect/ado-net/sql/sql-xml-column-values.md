---
title: SQL XML 열 값
description: SQL Server에서 XML 데이터를 검색하고 검색한 데이터로 작업하는 방법을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8dc9d5100f71fed39c1e4166882230451dd139e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451934"
---
# <a name="sql-xml-column-values"></a>SQL XML 열 값

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server에서는 `xml` 데이터 형식을 지원하므로 개발자가 <xref:Microsoft.Data.SqlClient.SqlCommand> 클래스의 표준 동작을 사용하여 이 형식이 포함된 결과 집합을 검색할 수 있습니다. @No__t_0 열은 검색 되는 열과 같은 방식으로 검색할 수 있지만 (예: <xref:Microsoft.Data.SqlClient.SqlDataReader>) 열의 내용을 XML로 사용 하려면 <xref:System.Xml.XmlReader>를 사용 해야 합니다.  
  
## <a name="example"></a>예제  
다음 콘솔 애플리케이션에서는 **AdventureWorks** 데이터베이스의 **Sales.Store** 테이블에서 <xref:Microsoft.Data.SqlClient.SqlDataReader> 인스턴스까지 각각 `xml` 열이 포함된 두 개의 행을 선택합니다. 각 행에 대해 <xref:Microsoft.Data.SqlClient.SqlDataReader>의 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 메서드를 사용 하 여 `xml` 열의 값을 읽습니다. 값은 <xref:System.Xml.XmlReader> 저장 됩니다. 콘텐츠를 <xref:System.Data.SqlTypes.SqlXml> 변수로 설정 하려면 <xref:System.Data.IDataRecord.GetValue%2A> 메서드 대신 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A>를 사용 해야 합니다.  <xref:System.Data.IDataRecord.GetValue%2A> `xml` 열의 값을 문자열로 반환 합니다.  
  
> [!NOTE]
>  **AdventureWorks** 샘플 데이터베이스는 SQL Server를 설치할 때 기본적으로 설치되지 않으며 SQL Server 설치 프로그램을 실행 하 여 설치할 수 있습니다.  
  
[!code-csharp[DataWorks SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>다음 단계
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server의 XML 데이터](xml-data-sql-server.md)
