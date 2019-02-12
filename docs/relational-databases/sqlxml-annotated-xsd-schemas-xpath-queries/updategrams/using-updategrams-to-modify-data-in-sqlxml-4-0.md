---
title: Updategram을 사용 하 여 SQLXML 4.0의에서 데이터를 수정 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- data insertions [SQLXML]
- data deletions [SQLXML]
- updating data [SQLXML]
- modifying data [SQLXML]
- OPENXML function
- updategrams [SQLXML]
- database modifications [SQLXML]
- data updates [SQLXML]
- modifying databases
- data modifications [SQLXML]
- deleting data
- inserting data
ms.assetid: b8b3b892-cb73-41d0-b945-bce148d81d9b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: df86cae9fe4fd132393b6c882977156bd5c0ff45
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040344"
---
# <a name="using-updategrams-to-modify-data-in-sqlxml-40"></a>SQLXML 4.0에서 updategram을 사용하여 데이터 수정
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  수정할 수 있습니다 (삽입, 업데이트 또는 삭제)의 데이터베이스 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] updategram 이나 OPENXML을 사용 하 여 문서에서 기존 XML [!INCLUDE[tsql](../../../includes/tsql-md.md)] 함수입니다.  
  
 이 섹션에서는 updategram에 대해 설명하고 updategram 사용 예를 보여 줍니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Updategram 소개 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/introduction-to-updategrams-sqlxml-4-0.md)  
 Updategram에 대한 기본 정보 및 예를 제공합니다.  
  
 [Updategram에 주석이 추가 된 매핑 스키마 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)  
 Updategram의 주석이 추가된 매핑 스키마에 대해 설명하고 이에 대한 예를 제공합니다.  
  
 [NULL 처리 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/null-handling-sqlxml-4-0.md)  
 요소 및 특성 값에 NULL을 지정하는 방법에 대해 설명합니다.  
  
 [XML Updategram을 사용 하 여 데이터를 삽입 합니다. &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
 Updategram을 사용하여 데이터를 삽입하는 방법을 설명하고 이에 대한 예를 제공합니다.  
  
 [XML Updategram을 사용 하 여 데이터 삭제 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/deleting-data-using-xml-updategrams-sqlxml-4-0.md)  
 Updategram을 사용하여 데이터를 삭제하는 방법을 설명하고 이에 대한 예를 제공합니다.  
  
 [XML Updategram을 사용 하 여 데이터를 업데이트 하는 중 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md)  
 Updategram을 사용하여 기존 데이터를 수정하는 방법을 설명하고 이에 대한 예를 제공합니다.  
  
 [Updategram에 매개 변수를 전달 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)  
 매개 변수를 updategram에 전달하는 방법을 설명하고 이에 대한 예를 제공합니다.  
  
 [Updategram의 데이터베이스 동시성 문제 처리 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/handling-database-concurrency-issues-in-updategrams-sqlxml-4-0.md)  
 Updategram에서 동시성 문제를 처리하는 데 사용할 수 있는 다양한 수준의 보호에 대해 설명하고 이에 대한 예를 제공합니다.  
  
 [Updategram 예제 응용 프로그램 &#40;SQLXML 4.0&#41;](https://msdn.microsoft.com/library/d2287e10-4007-4ba4-ad84-4e2b6adfede5)  
 Updategram을 사용하는 예제 응용 프로그램을 제공합니다.  
  
 [XML Updategram에 대 한 제한 사항 및 지침 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/guidelines-and-limitations-of-xml-updategrams-sqlxml-4-0.md)  
 Updategram 사용 시 주의해야 할 사항에 대해 설명합니다.  
  
  
