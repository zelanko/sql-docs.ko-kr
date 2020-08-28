---
description: XSLT 변환
title: XSLT 변환 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
author: rothja
ms.author: jroth
ms.openlocfilehash: a704245d166b0d53cb7ed17e6a5f8cdfa32d9447
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978804"
---
# <a name="xslt-transformations"></a>XSLT 변환
XSLT는 생성 된 XML에 적용 하 여 다른 형식으로 변환할 수 있습니다. ADO의 XML 형식을 이해 하면 보다 사용자에 게 친숙 한 형식으로 변환할 수 있는 XSLT 템플릿 개발에 도움이 됩니다.  
  
 예를 들어 레코드 집합의 각 행이 rs: data 요소 내의 z:row 요소로 저장 된다는 것을 알 수 있습니다. 마찬가지로 레코드 집합의 각 필드는이 요소에 대 한 특성-값 쌍으로 저장 됩니다.  
  
## <a name="remarks"></a>설명  
 다음 XSLT 스크립트를 이전 섹션에 표시 된 XML에 적용 하 여 브라우저에 표시할 HTML 테이블로 변환할 수 있습니다.  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 XSLT는 ADO Save 메서드로 생성 된 XML 스트림을 테이블 머리글과 함께 레코드 집합의 각 필드를 표시 하는 HTML 테이블로 변환 합니다. 또한 테이블 머리글과 행에는 서로 다른 글꼴 및 색이 할당 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 형식으로 레코드 유지](./persisting-records-in-xml-format.md)