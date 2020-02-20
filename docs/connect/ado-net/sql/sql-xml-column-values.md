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
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: aa02072e139c2446ae67086ef43668af4403890c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244008"
---
# <a name="sql-xml-column-values"></a>SQL XML 열 값

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server에서는 `xml` 데이터 형식을 지원하므로 개발자가 <xref:Microsoft.Data.SqlClient.SqlCommand> 클래스의 표준 동작을 사용하여 이 형식이 포함된 결과 집합을 검색할 수 있습니다. `xml` 열은 다른 열과 같은 방식으로 검색할 수 있지만(예: <xref:Microsoft.Data.SqlClient.SqlDataReader>) 열의 콘텐츠를 XML로 활용하려면 <xref:System.Xml.XmlReader>를 사용해야 합니다.  
  
## <a name="example"></a>예제  
다음 콘솔 애플리케이션에서는 **AdventureWorks** 데이터베이스의 **Sales.Store** 테이블에서 <xref:Microsoft.Data.SqlClient.SqlDataReader> 인스턴스까지 각각 `xml` 열이 포함된 두 개의 행을 선택합니다. 각 행에 대해 <xref:Microsoft.Data.SqlClient.SqlDataReader>의 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 메서드를 사용하여 `xml` 열의 값을 읽습니다. 이 값은 <xref:System.Xml.XmlReader>에 저장됩니다. <xref:System.Data.IDataRecord.GetValue%2A>는 `xml` 열의 값을 문자열로 반환하므로 콘텐츠를 <xref:System.Data.SqlTypes.SqlXml> 변수로 설정하려면 <xref:System.Data.IDataRecord.GetValue%2A> 메서드가 아닌 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A>을 사용해야 합니다.  
  
> [!NOTE]
>  **AdventureWorks** 샘플 데이터베이스는 SQL Server를 설치할 때 기본적으로 설치되지 않으며 SQL Server Setup을 실행하여 설치할 수 있습니다.  
  
[!code-csharp [SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>다음 단계
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server의 XML 데이터](xml-data-sql-server.md)
