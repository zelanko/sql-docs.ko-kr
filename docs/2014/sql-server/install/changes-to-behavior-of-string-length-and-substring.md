---
title: String-length 및 substring의 동작 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
caps.latest.revision: 9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0261587f42bfa52f2a1db59ab76fefb0c8670be7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312883"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>string-length 및 substring의 동작에 대한 변경 사항
  합니다 [string-length 함수 &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) 하 고 [substring 함수 &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) 함수를 포함 하는 XML 데이터베이스와 함께 사용할 때 다른 결과 반환할 수 있습니다 서로게이트 문자입니다.  
  
## <a name="description"></a>Description  
 와 호환 되도록 데이터베이스가 설정 된 경우 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 동작을 [string-length 함수 &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) 하 고 [substring 함수 &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) 유니코드 보충 문자를 처리할 때 함수 변경 됩니다. U+FFFF보다 큰 코드 포인트를 포함하도록 정의된 각 유니코드 보조 문자는 이전 버전에서와 마찬가지로 이러한 함수를 사용하여 두 문자가 아닌 한 문자로 계산됩니다.  
  
 서로게이트 문자에 대한 자세한 내용은 [서로게이트 및 보조 문자(Surrogates and Supplementary Characters)](http://go.microsoft.com/fwlink/?LinkId=178317)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
