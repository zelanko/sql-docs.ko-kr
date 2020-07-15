---
title: XSINIL을 사용하여 NULL 값 요소 생성 | Microsoft Docs
description: ELEMENTS 지시어에 XSINIL 매개 변수를 사용하여 NULL 값에 대한 XML 요소를 생성하는 방법을 알아봅니다.
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 7cf18eb7c5dea9a61988533205a3a64ab1ae3fd0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85638951"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>XSINIL 매개 변수를 사용하여 NULL 값 요소 생성

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**ELEMENTS** 지시어는 각 열 값이 XML의 요소로 매핑되는 XML을 구성합니다. 기본적으로 열 값이 NULL이면 요소가 추가되지 않습니다. 그러나 ELEMENTS 지시어에 선택 항목인 **XSINIL** 매개 변수를 지정하면 NULL 값에 대해서도 요소가 생성되도록 요청할 수 있습니다. 이 경우 **xsi:nil** 특성이 TRUE로 설정된 요소가 각 NULL 열 값에 대해 반환됩니다.  
  
## <a name="see-also"></a>참고 항목

[FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)

[SELECT - FOR 절](../../t-sql/queries/select-for-clause-transact-sql.md)
