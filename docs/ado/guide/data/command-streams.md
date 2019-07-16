---
title: 스트림을 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd0c2273739a3651c7fdd4c424ce0cb47d39dd5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925840"
---
# <a name="command-streams"></a>명령 스트림
ADO를 문자열 형식으로 지정 하 여 명령 입력 지원 왔지만 합니다 **CommandText** 속성입니다. 대신 2.7 이상 ADO를 사용 하 여 사용할 수도 있습니다 정보 스트림을 명령 입력에 대 한이 스트림에 할당 하 여 합니다 **CommandStream** 속성입니다. ADO를 할당할 수 있습니다 **Stream** 개체나 COM을 지 원하는 모든 개체 **IStream** 인터페이스입니다.  
  
 명령 스트림의 내용은 간단히에서 전달 됩니다 ADO 공급자에 공급자에 명령 입력 스트림에서이 기능이 작동 하기 위해 지원 해야 합니다. 예를 들어, SQL Server XML 템플릿 또는 TRANSACT-SQL로 OpenXML 확장 형식의 쿼리를 지원합니다.  
  
 설정 하 여 명령 스트림의 세부 정보 공급자가 해석할 해야 하기 때문에 지정 해야 합니다 **언어** 속성입니다. 변수의 **언어** 공급자에 정의 된 GUID를 포함 하는 문자열입니다. 에 대 한 유효한 값에 대 한 자세한 **언어** 공급자가 지원 공급자 설명서를 참조 하세요.  
  
## <a name="xml-template-query-example"></a>XML 서식 파일 쿼리 예제  
 다음 예에서는 VBScript에서 Northwind 데이터베이스에 기록 됩니다.  
  
 첫째, 초기화 하 고 엽니다는 **Stream** 쿼리 스트림을 포함 하는 데 사용할 개체:  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 쿼리 스트림의 내용을 XML 템플릿을 쿼리 됩니다.  
  
 템플릿 쿼리가 sql 식별 된 XML 네임 스페이스에 대 한 참조가 필요: 접두사는 \<sql:query > 태그입니다. SQL SELECT 문은 XML 서식 파일의 콘텐츠로 포함 이며 다음과 같은 문자열 변수에 할당 됩니다.  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 그런 다음 문자열을 스트림에 쓸:  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 AdoStreamQuery에 할당 합니다 **CommandStream** ado 속성 **명령** 개체:  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 명령 언어를 지정 **언어**, SQL Server OLE DB 공급자 명령 스트림 해석 해야 하는 방법을 나타냅니다. 공급자별 GUID로 지정 된 언어:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 마지막으로 쿼리를 실행 하 고 결과를 반환 된 **레코드 집합** 개체:  
  
```  
Set objRS = adoCmd.Execute  
```
