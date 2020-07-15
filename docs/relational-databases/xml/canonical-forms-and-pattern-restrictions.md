---
title: 정규 형식 및 패턴 제한 사항 | Microsoft 문서
description: 기본 값 형식의 정식 표현이 XSD 패턴 패싯의 패턴 제한을 따르지 않는 경우 발생하는 문제를 방지하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- pattern restrictions
- canonical forms
ms.assetid: 088314ec-7d0b-4a05-8a33-f35da5bfe59c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e6042ae1a63b61cd47fa42470c0707877625c5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775627"
---
# <a name="canonical-forms-and-pattern-restrictions"></a>정규 형식 및 패턴 제한 사항
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  XSD 패턴 패싯을 사용하면 단순 유형의 어휘 영역을 제한할 수 있습니다. 어휘 표현이 둘 이상 있는 형식에 패턴 제한을 적용한 경우 일부 값으로 인해 유효성 검사 후 예기치 않은 동작이 발생할 수 있습니다.  
  
 이러한 동작은 이러한 값의 어휘 표현이 데이터베이스에 저장되지 않기 때문에 발생합니다. 따라서 출력으로 직렬화될 때 값이 해당 정규 표현으로 변환됩니다. 문서에 있는 값의 정규 형식이 값 형식에 대한 패턴 제한을 준수하지 않는 경우 사용자가 이 값을 다시 삽입하려고 하면 해당 문서는 거부됩니다.  
  
 이 문제를 방지하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 값의 정규 형식에서 패턴 제한 사항을 위반하기 때문에 다시 삽입할 수 없는 값이 포함된 XML 문서를 거부합니다. 예를 들어 "33.000"이라는 값은 "33 **.0+"라는 패턴 제한이 있는** xs:decimal\\에서 파생된 형식에 대해 유효성이 확인되지 않습니다. "33.000"은 이 패턴을 준수하지만 정규 형식인 "33"은 이 패턴을 준수하지 않습니다.  
  
 따라서 **boolean**, **decimal**, **float**, **double**, **dateTime**, **time**, **date**, **hexBinary**, 및 **base64Binary**의 기본 형식에서 파생된 형식에 패턴 패싯을 적용할 때 주의해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 경고가 발생됩니다.  
  
 부동 소수점 값을 부정확하게 직렬화할 경우 비슷한 문제가 발생합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용되는 부동 소수점 직렬화 알고리즘으로 인해 유사한 값들이 동일한 정규 형식을 공유할 수 있습니다. 부동 소수점 값을 직렬화하고 다시 삽입하면 값이 약간 변경될 수도 있습니다. 드물지만 이로 인해 값을 다시 삽입한 경우 값이 해당 형식에 대해 **enumeration**, **minInclusive**, **minExclusive**, **maxInclusive**또는 **maxExclusive**와 같은 패싯 중 하나를 위반할 수 있습니다. 이 문제를 방지하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 직렬화 및 다시 삽입할 수 없는 `xs:float` 또는 `xs:double` 에서 파생되는 형식의 값을 모두 거부합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
