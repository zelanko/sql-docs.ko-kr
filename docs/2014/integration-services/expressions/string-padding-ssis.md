---
title: 문자열 패딩(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7141a102efe167c07147dce19ac2a88aa4606f3b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359325"
---
# <a name="string-padding-ssis"></a>문자열 패딩(SSIS)
  식 계산기는 문자열에 선행 및 후행 공백이 포함되어 있는지 확인하지 않으며 문자열을 비교하기 전에 동일한 길이가 되도록 패딩하지도 않습니다. 식에 문자열 패딩이 필요하면 + 연산자를 사용하여 열 값과 빈 문자열을 연결할 수 있습니다. 자세한 내용은 [+&#40;연결&#41;&#40;SSIS 식&#41;](concatenate-ssis-expression.md)를 참조하세요.  
  
 반면 공백을 제거하려는 경우 식 계산기는 선행 또는 후행 공백이나 둘 다를 제거하는 LTRIM, RTRIM 및 TRIM 함수를 제공합니다. 자세한 내용은 [LTRIM&#40;SSIS 식&#41;](trim-ssis-expression.md), [RTRIM&#40;SSIS 식&#41;](rtrim-ssis-expression.md) 및 [TRIM&#40;SSIS 식&#41;](trim-ssis-expression.md)을 참조하세요.  
  
> [!NOTE]  
>  LEN 함수는 선행 및 후행 공백을 개수에 포함합니다.  
  
## <a name="related-content"></a>관련 내용  
 pragmaticworks.com의 기술 문서 - [SSIS 식 치트 시트](https://go.microsoft.com/fwlink/?LinkId=217683)  
  
  
