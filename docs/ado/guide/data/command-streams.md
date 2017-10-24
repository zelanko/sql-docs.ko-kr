---
title: "스트림 명령 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1be2cc9528e62e548feb242b06686ad50a1753c8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="command-streams"></a>명령 스트림
ADO에서 지정 된 문자열 형식에 대 한 명령 입력 지원 왔지만 **CommandText** 속성입니다. 대신 ado 2.7 이상을 사용할 수도 있습니다 정보의 스트림입니다 명령 입력에 대 한 스트림을 지정 하 여는 **CommandStream** 속성입니다. ADO를 할당할 수 **스트림** 개체나 지 원하는 COM 개체 **IStream** 인터페이스입니다.  
  
 명령 스트림의 콘텐츠 단순히에서 전달 됩니다 ADO 공급자에 공급자 스트림에이 기능을 사용 하 여 명령 입력을 지원 해야 합니다. 예를 들어 SQL Server는 XML 서식 파일 또는 TRANSACT-SQL에 대 한 OpenXML 확장 형식으로의 쿼리를 지원합니다.  
  
 스트림에 대 한 세부 정보는 공급자에 의해 해석 해야, 있으므로 설정 하 여 명령 언어를 지정 해야는 **언어** 속성입니다. 값 **언어** 공급자에 의해 정의 되는 GUID를 포함 하는 문자열입니다. 에 대 한 유효한 값에 대 한 내용은 **언어** 공급자가 지원 공급자 설명서를 참조 하십시오.  
  
## <a name="xml-template-query-example"></a>XML 서식 파일 쿼리 예제  
 다음 예에서는 VBScript에서 Northwind 데이터베이스에 기록 됩니다.  
  
 첫째, 초기화 하 고 열은 **스트림** 쿼리 스트림이 포함 하는 데 사용할 개체:  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 쿼리 스트림의 내용을 XML 서식 파일 쿼리 됩니다.  
  
 서식 파일 쿼리에 sql로 식별 되는 XML 네임 스페이스에 대 한 참조가 필요:의 접두사는 \<sql:query > 태그입니다. SQL SELECT 문은 XML 서식 파일의 내용으로 포함 되며 다음과 같이 문자열 변수에 할당 됩니다.  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 스트림에 문자열을 다음으로 기록:  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 AdoStreamQuery에 할당 된 **CommandStream** ADO의 속성 **명령** 개체:  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 명령 언어를 지정 **언어**, SQL Server OLE DB 공급자 명령 스트림 해석 방법을 나타냅니다. 공급자 관련 GUID로 지정 된 언어:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 마지막으로 쿼리를 실행 하 고 결과를 반환 된 **레코드 집합** 개체:  
  
```  
Set objRS = adoCmd.Execute  
```

