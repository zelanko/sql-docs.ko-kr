---
title: CLR 데이터베이스 개체에서 XML 직렬화 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- serialization
- XML serialization [CLR integration]
- common language runtime [SQL Server], XML serialization
- XmlSerializer class
ms.assetid: ac84339b-9384-4710-bebc-01607864a344
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 646d15dc3091323e6e7db2af757640122fb2f0fd
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158479"
---
# <a name="xml-serialization-from-clr-database-objects"></a>CLR 데이터베이스 개체에서 XML 직렬화
  XML 직렬화는 다음과 같은 두 가지 시나리오에서 필요합니다.  
  
-   CLR(공용 언어 런타임) 개체에서 웹 서비스를 호출하는 경우  
  
-   UDT(사용자 정의 형식)를 XML로 변환하는 경우  
  
 `XmlSerializer` 클래스를 호출하여 XML 직렬화를 수행하면 일반적으로 추가 직렬화 어셈블리가 생성되어 원본 어셈블리와 함께 프로젝트로 오버로드됩니다. 그러나 CLR에서는 보안을 위해 이 오버로드가 실행되지 않습니다. 따라서 웹 서비스를 호출 하거나 UDT에서 내에 XML 변환을 수행할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 어셈블리 라는 도구를 사용 하 여 수동으로 만들어야 **Sgen.exe** 필요한을 생성 하는.NET Framework와 함께 제공 serialization 어셈블리입니다. `XmlSerializer`를 호출하는 경우 다음 단계에 따라 직렬화 어셈블리를 직접 만들어야 합니다.  
  
1.  실행 합니다 **Sgen.exe** 원본 어셈블리에 대 한 XML 직렬 변환기가 포함 된 어셈블리를 만들려면.NET Framework SDK와 함께 제공 되는 도구입니다.  
  
2.  `CREATE ASSEMBLY` 문을 사용하여 생성한 어셈블리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 등록합니다.  
  
 XML serialization을 수행할 때 발생할 수 있는 오류에 대 한 정보를 다음 Microsoft 지원 문서를 참조 하세요. ["동적으로 생성 된 serialization 어셈블리를 로드할 수 없습니다"](https://support.microsoft.com/kb/913668)합니다.  
  
 XMLSerializer에서 지원하지 않는 데이터 형식에 대한 자세한 내용은 .NET Framework 설명서의 .NET Framework에서 XML 스키마의 바인딩 지원을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 데이터베이스 개체에서 데이터 액세스](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CREATE ASSEMBLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
  
