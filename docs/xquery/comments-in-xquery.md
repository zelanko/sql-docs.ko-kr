---
title: XQuery의 설명 | Microsoft Docs
description: XQuery에 주석을 추가 하기 위한 구문 및 구분 기호에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- comments [XQuery]
- XQuery, comments
ms.assetid: 4d977268-de9d-4bf0-b310-b63f6a0fb0db
author: rothja
ms.author: jroth
ms.openlocfilehash: 67f2ad02eb9486508840f0b731b1d6e705d94f7a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726747"
---
# <a name="comments-in-xquery"></a>XQuery의 주석
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery에 주석을 추가할 수 있습니다. 주석 문자열은 "`(:`" 및 "`:)`" 구분 기호를 사용하여 추가됩니다. 예를 들면 다음과 같습니다.  
  
```  
declare @x xml  
set @x=''  
SELECT @x.query('  
(: simple query to construct an element :)  
<ProductModel ProductModelID="10" />  
')  
```  
  
 다음은 **xml** 유형의 명령 열에 대해 쿼리를 지정 하는 또 다른 예입니다.  
  
```  
SELECT Instructions.query('  
(: declare prefix and namespace binding in the prolog. :)  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  (: Following expression retrieves the <Location> element children of the <root> element. :)  
  /AWMI:root/AWMI:Location  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
  
