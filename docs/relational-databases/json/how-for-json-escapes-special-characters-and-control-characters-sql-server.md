---
title: "FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법(SQL Server) | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 0b0816ec492422b72abd22f0b493c6fc1670471a
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 SQL Server **SELECT**의 **FOR JSON** 절이 특수 문자를 이스케이프 처리하고 JSON 출력에서 제어 문자를 표시하는 방법에 대해 설명합니다.  

> [!IMPORTANT]
> 이 페이지에서는 Microsoft SQL Server에서 기본 제공되는 JSON 지원에 대해 설명합니다. JSON에서 이스케이프 및 인코딩에 대한 일반적인 정보는 JSON RFC - [http://www.ietf.org/rfc/rfc4627.txt](http://www.ietf.org/rfc/rfc4627.txt)의 섹션 2.5를 참조하세요.

## <a name="escaping-of-special-characters"></a>특수 문자를 이스케이프 처리  
원본 데이터에 특수 문자가 포함된 경우 **FOR JSON** 절은 다음 표에 나와 있는 것처럼 `\`를 사용하여 JSON 출력의 특수 문자를 이스케이프 처리합니다. 속성 이름과 해당 값에서 모두 특수 문자가 이와 같이 이스케이프 처리됩니다.  
  
|**특수 문자**|**이스케이프 처리된 출력**|  
|---------------------------|--------------------------|  
|따옴표(")|\\"|  
|백슬래시(\\)|\\\|  
|슬래시(/)|\\/|  
|백스페이스|\b|  
|용지 공급|\f|  
|줄 바꿈|\n|  
|캐리지 리턴|\r|  
|가로 탭|\t|  
  
## <a name="control-characters"></a>제어 문자  
원본 데이터에 제어 문자가 포함된 경우 **FOR JSON** 절은 다음 표에 나와 있는 것처럼 JSON 출력의 제어 문자를 `\u<code>` 형식으로 인코딩합니다.  
  
|**제어 문자**|**인코딩된 출력**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|…|…|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>예제  
 다음은 특수 문자와 제어 문자를 모두 포함하는 원본 데이터에 대한 **FOR JSON** 출력의 예입니다.  
  
 쿼리:  
  
```sql  
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
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>기본 제공 SQL Server에서 JSON 지원에 대 한 자세한 정보  
특정 솔루션에 많이 사용 사례 및 권장 사항, 참조는 [기본 제공 JSON 지원에 대 한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) SQL Server와 Microsoft 프로그램 관리자 인 Jovan popovic의 Azure SQL 데이터베이스에 있습니다.
  
## <a name="see-also"></a>관련 항목:  
 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[FOR 절](../../t-sql/queries/select-for-clause-transact-sql.md)

