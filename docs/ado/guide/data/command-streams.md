---
description: 명령 스트림
title: 명령 스트림 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
author: rothja
ms.author: jroth
ms.openlocfilehash: 2db139f3f5ae4ff701e36179a9df7ce30eecd94e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453665"
---
# <a name="command-streams"></a>명령 스트림
ADO는 항상 **CommandText** 속성에 지정 된 문자열 형식으로 지원 되는 명령 입력을 지원 합니다. 또는 ADO 2.7 이상에서는 명령을 **commandstream** 속성에 할당 하 여 명령 입력에 대 한 정보 스트림을 사용할 수도 있습니다. ADO **스트림** 개체나 COM **IStream** 인터페이스를 지 원하는 개체를 할당할 수 있습니다.  
  
 명령 스트림의 콘텐츠는 단순히 ADO에서 공급자로 전달 되기 때문에이 기능이 작동 하려면 공급자가 stream에서 명령 입력을 지원 해야 합니다. 예를 들어 SQL Server는 XML 템플릿 형식 또는 Transact-sql에 대 한 OpenXML 확장 형식의 쿼리를 지원 합니다.  
  
 스트림의 세부 정보는 공급자가 해석 해야 하므로 **언어** 속성을 설정 하 여 명령 언어를 지정 해야 합니다. **언어** 의 값은 공급자가 정의한 GUID를 포함 하는 문자열입니다. 공급자가 지 원하는 **언어** 에 대 한 유효한 값에 대 한 자세한 내용은 공급자 설명서를 참조 하세요.  
  
## <a name="xml-template-query-example"></a>XML 템플릿 쿼리 예제  
 다음 예제는 Northwind 데이터베이스에 VBScript로 작성 되었습니다.  
  
 먼저 쿼리 스트림을 포함 하는 데 사용할 **Stream** 개체를 초기화 하 고 엽니다.  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 쿼리 스트림의 내용은 XML 템플릿 쿼리가 됩니다.  
  
 템플릿 쿼리에는 태그의 sql: 접두사로 식별 된 XML 네임 스페이스에 대 한 참조가 필요 합니다 \<sql:query> . SQL SELECT 문은 XML 템플릿의 내용으로 포함 되며 다음과 같이 문자열 변수에 할당 됩니다.  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 다음으로 스트림에 문자열을 씁니다.  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 AdoStreamQuery를 ADO **명령** 개체의 **commandstream** 속성에 할당 합니다.  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 SQL Server OLE DB 공급자가 명령 스트림을 해석 하는 방법을 나타내는 **명령 언어 언어**를 지정 합니다. 공급자별 GUID로 지정 된 언어:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 마지막으로 쿼리를 실행 하 고 결과를 **레코드 집합** 개체로 반환 합니다.  
  
```  
Set objRS = adoCmd.Execute  
```
