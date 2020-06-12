---
title: 로컬 이름 함수 (XQuery) | Microsoft Docs
description: XQuery 함수 로컬 이름 ()을 사용 하 여 노드의 로컬 이름 부분을 반환 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name function
- local-name function
ms.assetid: c901ef5d-89c5-482a-bf64-3eefbcf3098d
author: rothja
ms.author: jroth
ms.openlocfilehash: d3a10ab445bfcf9f61b7eb6c952100af9b6fadbb
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689569"
---
# <a name="functions-on-nodes---local-name"></a>노드 함수 - local-name
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  *$Arg* 이름의 로컬 부분을 길이가 0 인 문자열이 나 Xs: NCName의 어휘 형식으로 사용할 xs: 문자열로 반환 합니다. 인수를 제공하지 않으면 기본값은 컨텍스트 노드입니다.  
  
## <a name="syntax"></a>구문  
  
```  
fn:local-name() as xs:string  
fn:local-name($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>인수  
 *$arg*  
 로컬 이름 부분이 검색될 노드 이름입니다.  
  
## <a name="remarks"></a>설명  
  
-   SQL Server에서 인수 없이 **fn: 로컬 이름 ()** 은 컨텍스트 종속 조건자의 컨텍스트에서만 사용할 수 있습니다. 특히 사용 시 대괄호(`[ ]`)로 묶어야 합니다.  
  
-   인수가 제공되었지만 빈 시퀀스인 경우 함수는 길이가 0인 문자열을 반환합니다.  
  
-   대상 노드가 문서 노드이거나 설명이거나 텍스트 노드이기 때문에 대상 노드의 이름이 없는 경우 함수는 길이가 0인 문자열을 반환합니다.  
  
## <a name="examples"></a>예  
 이 항목에서는 AdventureWorks 데이터베이스의 다양 한 **xml** 유형 열에 저장 된 xml 인스턴스에 대 한 XQuery 예를 제공 합니다.  
  
### <a name="a-retrieve-local-name-of-a-specific-node"></a>A. 특정 노드의 로컬 이름 검색  
 다음은 형식화되지 않은 XML 인스턴스에 대해 지정된 쿼리입니다. `local-name(/ROOT[1])` 쿼리 식은 지정한 노드의 로컬 이름 부분을 검색합니다.  
  
```  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('local-name(/ROOT[1])')  
-- result = ROOT  
```  
  
 다음은 ProductModel 테이블의 형식화된 xml 열인 Instructions 열에 대해 지정된 쿼리입니다. `local-name(/AWMI:root[1]/AWMI:Location[1])` 식은 지정된 노드의 로컬 이름 `Location`을 반환합니다.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     local-name(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
-- result = Location  
```  
  
### <a name="b-using-local-name-without-argument-in-a-predicate"></a>B. 조건자에서 인수가 없는 로컬 이름 사용  
 다음 쿼리는 제품 모델 테이블의 명령 열, 형식화 된 **xml** 열에 대해 지정 됩니다. `root`이 식은 QName의 로컬 이름 부분이 "Location" 인 <> 요소의 모든 요소 자식을 반환 합니다. **로컬 이름 ()** 함수는 조건자에 지정 되 고 함수는 컨텍스트 노드를 사용 하는 인수를 포함 하지 않습니다.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
  /AWMI:root//*[local-name() = "Location"]') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 이 쿼리는 `Location` <> 요소의 모든 <> 요소 자식을 반환 합니다 `root` .  
  
## <a name="see-also"></a>참고 항목  
 [노드의 함수](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [네임 스페이스 uri 함수 &#40;XQuery&#41;](../xquery/functions-on-nodes-namespace-uri.md)  
  
  
