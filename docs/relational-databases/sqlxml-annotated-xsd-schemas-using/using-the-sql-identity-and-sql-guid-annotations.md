---
title: sql:identity 및 sql:guid 주석 사용
description: 'XSD 스키마에서 sql: identity 및 sql: guid 주석을 사용 하 여 XML updategram의 동작을 정의 하는 방법에 대해 알아봅니다.'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:guid
- annotated XSD schemas, IDENTITY-type columns
- annotated XSD schemas, GUID values
- DiffGrams [SQLXML], annotations
- identity annotation
- XSD schemas [SQLXML], GUID values
- GUIDs [SQLXML]
- guid annotation
- sql:identity
- IDENTITY-type column
- XSD schemas [SQLXML], IDENTITY-type columns
- updategrams [SQLXML], GUID values
ms.assetid: 7661dfd0-6573-4692-a8f1-3597adcd33c4
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7c66bac3f83aff00a458d3fed14296d2b03071f7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479324"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>sql:identity 및 sql:guid 주석 사용
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  의 데이터베이스 열에 매핑되는 노드의 XSD 스키마에 **sql: identity** 및 **sql: guid** 주석을 지정할 수 있습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Updategram 형식은 **updg: identity** 및 **updg: guid** 특성을 지원 하지만 DiffGram 형식은 지원 하지 않습니다. **Updg: identity** 특성은 id 유형 열을 업데이트 하는 동작을 정의 합니다. **Updg: guid** 특성을 사용 하면에서 guid 값을 가져와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] updategram에서 사용할 수 있습니다. 자세한 내용 및 작업 예제는 [XML Updategrams을 사용 하 여 데이터 삽입 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)을 참조 하세요.  
  
 **Sql: identity** 및 **sql: guid** 주석은이 기능을 diffgram로 확장 합니다.  
  
 DiffGram을 실행하면 DiffGram이 먼저 updategram으로 변환된 다음 이 updategram이 실행됩니다. XSD 스키마에서 **sql: identity** 및 **sql: guid** 주석을 지정 하 여 실제로 updategram 동작을 정의 합니다. 따라서 모든 주석이 updategram의 컨텍스트에서 기술됩니다. DiffGram과 updategram에 모두 주석을 사용할 수 있지만 이 중 updategram이 ID 및 GUID 값을 처리하는 더 강력한 방법을 제공합니다.  
  
 **Sql: identity** 및 **sql: guid** 주석은 복합 콘텐츠 요소에 정의 될 수 있습니다.  
  
## <a name="sqlidentity-annotation"></a>sql:identity 주석  
 ID 형식 데이터베이스 열에 매핑되는 노드의 XSD 스키마에서 **sql: identity** 주석을 지정할 수 있습니다. 이 주석에 대해 지정 된 값은 updategram에 제공 된 값을 사용 하 여 열을 수정 하거나 값을 무시 하 여 ID 유형 열이 업데이트 되는 방법을 정의 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .이 경우이 열에 대해 생성 된 값이 사용 됩니다.  
  
 **Sql: identity** 주석에는 다음 두 값을 할당할 수 있습니다.  
  
 ignore  
 해당 열에 대해 updategram에 제공된 모든 값을 무시하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 통해 ID 값을 생성하도록 updategram에 지시합니다.  
  
 useValue  
 updategram에 제공된 값을 사용하여 IDENTITY 형식의 열을 업데이트하도록 updategram에 지시합니다. updategram은 열이 ID 값인지 여부는 확인하지 않습니다.  
  
 Updategram가 ID 유형 열에 대 한 값을 지정 하는 경우 스키마에 **sql: identity = "useValue"** 를 지정 해야 합니다.  
  
## <a name="sqlguid-annotation"></a>sql:guid 주석  
 updategram은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 GUID 값을 생성하도록 하고 이 값을 updategram에 사용할 수 있습니다. Diffgram의 컨텍스트에서 **sql: guid** 주석을 사용 하 여 SQL Server에서 생성 된 guid 값을 사용할지 아니면 해당 열에 대해 updategram에 제공 된 값을 사용할지를 지정할 수 있습니다.  
  
 **Sql: guid** 주석에는 다음 두 값을 할당할 수 있습니다.  
  
 generate  
 업데이트 작업 시 해당 열에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성한 GUID를 사용하도록 지정합니다.  
  
 useValue  
 updategram에 지정된 값을 해당 열에 사용하도록 지정합니다. 기본값입니다.  
  
  
