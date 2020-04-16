---
title: sql:identity 및 sql:guid 주석 사용
description: XSD 스키마에서 sql:IDENTITY 및 sql:guid 주석을 사용하여 XML 업데이트그램의 동작을 정의하는 방법을 알아봅니다.
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f581c1a5c0d925d48df5a16d95cdb141e2d48f83
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388102"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>sql:identity 및 sql:guid 주석 사용
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  의 데이터베이스 열에 매핑되는 노드에서 XSD 스키마에서 **sql:identity** 및 **sql:guid** 주석을 지정할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트 그램 형식은 **updg:at-identity** 및 **updg:guid** 특성을 지원하는 반면 DiffGram 형식은 지원하지 않습니다. **updg:at-IDENTITY** 특성은 IDENTITY 형식 열을 업데이트할 때의 동작을 정의합니다. **updg:guid** 특성을 사용하면 GUID 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져와 업데이트 그램에서 사용할 수 있습니다. 자세한 정보 및 작업 샘플은 [SQLXML 4.0&#41;&#40;XML 업데이트그램을 사용하여 데이터 삽입을 ](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)참조하십시오.  
  
 **sql:IDENTITY** 및 **sql:guid** 주석은 이 기능을 DiffGrams로 확장합니다.  
  
 DiffGram을 실행하면 DiffGram이 먼저 updategram으로 변환된 다음 이 updategram이 실행됩니다. XSD 스키마에서 **sql:identity** 및 **sql:guid** 주석을 지정하면 실제로 업데이트 그램의 동작을 정의할 수 있습니다. 따라서 모든 주석이 updategram의 컨텍스트에서 기술됩니다. DiffGram과 updategram에 모두 주석을 사용할 수 있지만 이 중 updategram이 ID 및 GUID 값을 처리하는 더 강력한 방법을 제공합니다.  
  
 **sql:IDENTITY** 및 **sql:guid** 주석은 복잡한 콘텐츠 요소에 정의할 수 있습니다.  
  
## <a name="sqlidentity-annotation"></a>sql:identity 주석  
 ID 형식 데이터베이스 열에 매핑되는 모든 노드에서 XSD 스키마에서 **sql:IDENTITY** 추가를 지정할 수 있습니다. 이 추가에 대해 지정된 값은 IDENTITY 형식 열이 업데이트되는 방법을 정의합니다(업데이트 그램에 제공된 값을 사용하여 열을 수정하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]값을 무시하여 이 열에 -생성된 값이 사용됩니다).  
  
 **sql:IDENTITY** 추가는 다음 두 값을 할당할 수 있습니다.  
  
 ignore  
 해당 열에 대해 updategram에 제공된 모든 값을 무시하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 통해 ID 값을 생성하도록 updategram에 지시합니다.  
  
 useValue  
 updategram에 제공된 값을 사용하여 IDENTITY 형식의 열을 업데이트하도록 updategram에 지시합니다. updategram은 열이 ID 값인지 여부는 확인하지 않습니다.  
  
 updategram에서 IDENTITY 형식 열에 대 한 값을 지정 하는 경우 **sql:identity="useValue"** 스키마에 지정 해야 합니다.  
  
## <a name="sqlguid-annotation"></a>sql:guid 주석  
 updategram은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 GUID 값을 생성하도록 하고 이 값을 updategram에 사용할 수 있습니다. DiffGrams의 컨텍스트에서 **sql:guid** 추가를 사용하여 SQL Server에서 생성되는 GUID 값을 사용할지 또는 해당 열의 updategram에 제공된 값을 사용할지 지정할 수 있습니다.  
  
 **sql:guid** 추가는 다음 두 값을 할당할 수 있습니다.  
  
 generate  
 업데이트 작업 시 해당 열에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성한 GUID를 사용하도록 지정합니다.  
  
 useValue  
 updategram에 지정된 값을 해당 열에 사용하도록 지정합니다. 기본값입니다.  
  
  
