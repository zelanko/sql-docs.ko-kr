---
title: 문자열 길이 및 하위 문자열의 동작에 대 한 변경 내용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18643dfc11d2b1b1d875a19c478f9ec8cbdd5be6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66428840"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>string-length 및 substring의 동작에 대한 변경 사항
  Xquery&#41;및 [substring &#40;함수](/sql/xquery/functions-on-string-values-substring) 를 사용 하 여 [문자열 길이 함수 &#40;](/sql/xquery/functions-on-string-values-string-length) xquery&#41;함수는 서로게이트 문자를 포함 하는 XML 데이터베이스와 함께 사용 될 경우 다른 결과를 반환할 수 있습니다.  
  
## <a name="description"></a>Description  
 데이터베이스가와 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]호환 되도록 설정 되 면 유니코드 보조 문자를 처리할 때 xquery [&#41;](/sql/xquery/functions-on-string-values-string-length) 및 substring 함수를 사용 하 여 [xquery&#41;](/sql/xquery/functions-on-string-values-substring) 함수를 &#40;&#40;합니다. U+FFFF보다 큰 코드 포인트를 포함하도록 정의된 각 유니코드 보조 문자는 이전 버전에서와 마찬가지로 이러한 함수를 사용하여 두 문자가 아닌 한 문자로 계산됩니다.  
  
 서로게이트 문자에 대한 자세한 내용은 [서로게이트 및 보조 문자(Surrogates and Supplementary Characters)](https://go.microsoft.com/fwlink/?LinkId=178317)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
