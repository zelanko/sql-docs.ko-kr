---
title: XSINIL을 사용하여 NULL 값 요소 생성 | Microsoft Docs
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
ms.openlocfilehash: 13451c2f9cfa87c1ceb83956e9ebe6056b74b6ad
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665301"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>XSINIL 매개 변수를 사용하여 NULL 값 요소 생성

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**ELEMENTS** 지시어는 각 열 값이 XML의 요소로 매핑되는 XML을 구성합니다. 기본적으로 열 값이 NULL이면 요소가 추가되지 않습니다. 그러나 ELEMENTS 지시어에 선택 항목인 **XSINIL** 매개 변수를 지정하면 NULL 값에 대해서도 요소가 생성되도록 요청할 수 있습니다. 이 경우 **xsi:nil** 특성이 TRUE로 설정된 요소가 각 NULL 열 값에 대해 반환됩니다.  
  
## <a name="see-also"></a>참고 항목

[FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)

[SELECT - FOR 절](../../t-sql/queries/select-for-clause-transact-sql.md)
