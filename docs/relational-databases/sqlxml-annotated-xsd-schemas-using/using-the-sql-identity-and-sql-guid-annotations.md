---
title: 'Sql: identity 및 sql: guid 주석 사용 | Microsoft Docs'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
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
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6220abfc616fc82bd0d1c16dd2d066da496c1f0a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021606"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>sql:identity 및 sql:guid 주석 사용
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  지정할 수 있습니다 합니다 **sql: identity** 하 고 **sql: guid** 데이터베이스 열에 매핑되는 모든 노드에서 XSD 스키마에서 주석을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. Updategram 형식에서 지 원하는 반면 합니다 **updg: id에** 하 고 **updg: guid** 특성인 DiffGram 형식은 그렇지 않습니다. 합니다 **updg: id에서** 특성 업데이트는 IDENTITY 유형 열에서 동작을 정의 합니다. 합니다 **updg: guid** 특성에서 GUID 값을 가져올 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] updategram에서 사용 합니다. 자세한 내용 및 작업 예제를 참조 하세요 [XML Updategram를 사용 하 여 데이터 삽입 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)합니다.  
  
 **sql: identity** 하 고 **sql: guid** 주석 DiffGrams에이 기능을 확장 합니다.  
  
 DiffGram을 실행하면 DiffGram이 먼저 updategram으로 변환된 다음 이 updategram이 실행됩니다. 지정 하 여를 **sql: identity** 하 고 **sql: guid** XSD 스키마에서 주석을 것은 updategram의 동작을 정의 합니다. 따라서 모든 주석이 updategram의 컨텍스트에서 기술됩니다. DiffGram과 updategram에 모두 주석을 사용할 수 있지만 이 중 updategram이 ID 및 GUID 값을 처리하는 더 강력한 방법을 제공합니다.  
  
 합니다 **sql: identity** 하 고 **sql: guid** 복합 콘텐츠 요소에서 주석을 정의할 수 있습니다.  
  
## <a name="sqlidentity-annotation"></a>sql:identity 주석  
 지정할 수 있습니다 합니다 **sql: identity** IDENTITY 형식의 데이터베이스 열에 매핑되는 임의의 노드에에서 XSD 스키마에서 주석입니다. 이 주석에 지정 된 값을 IDENTITY 형식의 열 업데이트 방법을 정의 (updategram에 제공 된 값을 사용 하 여 열을 수정 하거나 여는 경우 값이 무시를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-생성 된 값은이 열에 사용).  
  
 합니다 **sql: identity** 주석 두 값을 할당할 수 있습니다.  
  
 ignore  
 해당 열에 대해 updategram에 제공된 모든 값을 무시하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 통해 ID 값을 생성하도록 updategram에 지시합니다.  
  
 useValue  
 updategram에 제공된 값을 사용하여 IDENTITY 형식의 열을 업데이트하도록 updategram에 지시합니다. updategram은 열이 ID 값인지 여부는 확인하지 않습니다.  
  
 Updategram은 IDENTITY 유형 열에 대 한 값을 지정 하는 경우는 **sql: identity = "useValue"** 스키마를 지정 해야 합니다.  
  
## <a name="sqlguid-annotation"></a>sql:guid 주석  
 updategram은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 GUID 값을 생성하도록 하고 이 값을 updategram에 사용할 수 있습니다. Diffgram의 컨텍스트에서 사용할 수 있습니다 합니다 **sql: guid** 주석 SQL Server에서 생성 되는 GUID 값을 사용할지 여부를 지정 하거나 해당 열의 updategram에 제공 되는 값을 사용 합니다.  
  
 합니다 **sql: guid** 주석 두 값을 할당할 수 있습니다.  
  
 generate  
 업데이트 작업 시 해당 열에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성한 GUID를 사용하도록 지정합니다.  
  
 useValue  
 updategram에 지정된 값을 해당 열에 사용하도록 지정합니다. 이것은 기본값입니다.  
  
  
