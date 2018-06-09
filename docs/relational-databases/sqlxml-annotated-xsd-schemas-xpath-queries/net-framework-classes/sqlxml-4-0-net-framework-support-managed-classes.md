---
title: SQLXML 관리 되는 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 13212c73e4f12ed83e6677a8c819b3306eab3118
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708501"
---
# <a name="sqlxml-40-net-framework-support---managed-classes"></a>SQLXML 4.0.NET Framework 지원-관리 되는 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스에서 XML 데이터에 액세스하고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 환경으로 데이터를 가져와서 처리한 후 업데이트를 다시 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 보내는 응용 프로그램을 작성하는 데 사용할 수 있는 기능을 지원합니다. 
  
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 관리되는 클래스는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 내에서 SQLXML 4.0의 기능을 공개합니다. SQLXML 관리되는 클래스를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 XML 데이터에 액세스하고, .NET Framework 환경으로 데이터를 가져오며, 데이터를 처리하고, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 업데이트를 DiffGram으로 다시 보내 적용하는 C# 응용 프로그램을 작성할 수 있습니다. SQLXML 관리되는 클래스를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스로 업데이트를 적용할 때는 매핑 스키마를 사용해야 합니다. 작업 예제를 참조 하십시오. [.NET 환경에서 SQLXML 기능 액세스](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)합니다.  
  
 SQLXML 4.0에서 SQLXML 관리되는 클래스를 사용하려면 Microsoft Visual Studio를 설치해야 합니다.  
  
> [!NOTE]  
>  .NET Framework에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .NET 데이터 공급자가 포함되어 있습니다. 이 공급자는 .NET 환경에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 액세스하는 데 사용할 수 있지만 기존 SQL 쿼리(FOR XML 쿼리를 제외한 관계형 데이터베이스 쿼리)만 처리할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 XML 템플릿 또는 서버 쪽 XPath 쿼리를 실행할 수 없습니다.  

 데이터 액세스 및 수정 하는 방법에 대 한 정보에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 및 DiffGrams를 사용 하 여 데이터를 업데이트 하는 방법에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블, 참조 [.NET환경에서SQLXML기능에액세스](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
> [!NOTE]  
>  XML 대량 로드를 사용하여 XML 문서를 대량 로드하는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 응용 프로그램을 작성할 수도 있습니다. 자세한 내용은 참조 [XML 데이터의 대량 로드 수행 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)합니다. 응용 프로그램에 XML 대량 로드 DLL(Xblkld4.dll)에 대한 참조를 추가해야 합니다. 이 DLL은 Visual Studio .NET에서 자동으로 래퍼 라이브러리를 만드는 COM DLL입니다.  
  
  이 섹션에서는 사용 하는 방법을 보여 주는 예제 응용 프로그램에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 관리 되는 클래스:  
 [SQL 쿼리 실행 &#40;SQLXML 관리 되는 클래스&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)  
  [ExecuteXMLReader 메서드를 사용하여 SQL 쿼리 실행](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-by-using-the-executexmlreader-method.md)  
  [클라이언트 쪽에서 XML 처리 &#40;SQLXML 관리 되는 클래스&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/processing-xml-on-the-client-side-sqlxml-managed-classes.md)  
  [XPath 쿼리 실행 &#40;SQLXML 관리 되는 클래스&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-sqlxml-managed-classes.md)  
  [네임 스페이스로 XPath 쿼리 실행 &#40;SQLXML 관리 되는 클래스&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)  
  [CommandText 속성을 사용하여 템플릿 파일 실행](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandtext-property.md)  
  [CommandStream 속성을 사용하여 템플릿 파일 실행](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandstream-property.md)  
  [XSL 변환 적용 &#40;SQLXML 관리 되는 클래스&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)  
  

  
  
