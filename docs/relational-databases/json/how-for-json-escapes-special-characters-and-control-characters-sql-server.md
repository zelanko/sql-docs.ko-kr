---
title: "FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법(SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON, 특수 문자"
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 **FOR JSON** 절이 특수 문자를 이스케이프 처리하고 JSON 출력에서 제어 문자를 표시하는 방법에 대해 설명합니다.  
  
## 특수 문자를 이스케이프 처리  
 **FOR JSON** 절은 다음 표에 나와 있는 것처럼 `\`를 사용하여 JSON 출력의 특수 문자를 이스케이프 처리합니다. 속성 이름과 해당 값에서 모두 특수 문자가 이와 같이 이스케이프 처리됩니다.  
  
|**특수 문자**|**인코딩된 시퀀스**|  
|---------------------------|--------------------------|  
|따옴표(")|\\"|  
|백슬래시(\\)|\\\|  
|슬래시(/)|\\/|  
|백스페이스|\b|  
|용지 공급|\f|  
|줄 바꿈|\n|  
|캐리지 리턴|\r|  
|가로 탭|\t|  
  
## 제어 문자  
 **FOR JSON** 절은 다음 표에 나와 있는 것처럼 JSON 출력의 제어 문자를 `\u<code>` 형식으로 표시합니다.  
  
|**제어 문자**|**인코딩된 시퀀스**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|…|…|  
|CHAR(31)|\u001f|  
  
## 예제  
 아래에는 이스케이프 처리와 제어 문자가 모두 포함된 **FOR JSON** 절의 예가 나와 있습니다.  
  
 쿼리:  
  
```tsql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 결과:  
  
```json  
{  
   "KEY\\\t\/\"":"VALUE\\\t\/\r\n\"",  
   "0":"\u0000",  
   "1":"\u0001",  
  "31":"\u001f“  
}  
```  
  
## 참고 항목  
 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  