---
title: XML 데이터 검색 및 쿼리 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML data [SQL Server], retrieving
- XML instance retrieval
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3fd1505bbbfc03308cbdbf6a5fc9fba122c4da24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995271"
---
# <a name="retrieve-and-query-xml-data"></a>XML 데이터 검색 및 쿼리
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 XML 데이터를 쿼리할 때 지정해야 하는 쿼리 옵션에 대해 설명합니다. 또한 XML 인스턴스가 데이터베이스에 저장될 때 보존되지 않는 인스턴스의 일부분에 대해 설명합니다.  
  
##  <a name="features"></a> 보존되지 않는 XML 인스턴스 기능  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 XML 인스턴스의 내용을 보존하지만 XML 데이터 모델에서 중요하다고 간주되지 않는 XML 인스턴스의 측면은 보존하지 않습니다. 즉, 검색된 XML 인스턴스는 서버에 저장된 인스턴스와 다를 수 있지만 동일한 정보를 포함한다는 의미입니다.  
  
### <a name="xml-declaration"></a>XML 선언  
 인스턴스가 데이터베이스에 저장될 때 인스턴스에 있는 XML 선언이 보존되지 않습니다. 예를 들어  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 결과는 `<doc/>`입니다.  
  
 XML 데이터가 `<?xml version='1.0'?>`데이터 형식 인스턴스에 저장될 때 **xml** 과 같은 XML 선언이 보존되지 않습니다. 이것은 의도적인 것입니다. XML 선언()과 해당 특성(version/encoding/stand-alone)은 데이터가 **xml**유형으로 변환된 다음 삭제됩니다. XML 선언은 XML 파서에 대한 지시어로 취급됩니다. XML 데이터는 내부적으로 ucs-2로 저장되며 XML 인스턴스의 다른 모든 PI는 보존됩니다.  
  
  
### <a name="order-of-attributes"></a>특성 순서  
 XML 인스턴스의 특성 순서는 보존되지 않습니다. **xml** 유형의 열에 저장된 XML 인스턴스를 쿼리할 때 결과 XML의 특성 순서는 원래 XML 인스턴스와 다를 수 있습니다.  
  
  
### <a name="quotation-marks-around-attribute-values"></a>따옴표로 묶는 특성 값  
 특성 값에 표시된 작은따옴표와 큰따옴표는 보존되지 않습니다. 특성 값은 이름 및 값의 쌍으로 데이터베이스에 저장됩니다. 물음표는 저장되지 않습니다. XML 인스턴스에 대해 XQuery가 실행되는 경우 결과 XML은 특성 값이 큰따옴표로 묶여서 직렬화됩니다.  
  
```  
DECLARE @x xml  
-- Use double quotation marks.  
SET @x = '<root a="1" />'  
SELECT @x  
GO  
DECLARE @x xml  
-- Use single quotation marks.  
SET @x = '<root a=''1'' />'  
SELECT @x  
GO  
```  
  
 두 쿼리 모두 = `<root a="1" />`을 반환합니다.  
  
  
### <a name="namespace-prefixes"></a>네임스페이스 접두사  
 네임스페이스 접두사는 유지되지 않습니다. **xml** 유형의 열에 대해 XQuery를 지정하는 경우 직렬화된 XML 결과는 다른 네임스페이스 접두사를 반환할 수 있습니다.  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 결과의 네임스페이스 접두사는 다를 수 있습니다. 예를 들어  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
  
##  <a name="query"></a> 필수 쿼리 옵션 설정  
 **xml** 데이터 형식 메서드를 사용하여 **xml** 유형의 열 또는 변수를 쿼리할 때는 다음 옵션을 표시된 것과 같이 설정해야 합니다.  
  
|SET 옵션|필요한 값|  
|-----------------|---------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNINGS|ON|  
|ARITHABORT|ON|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
  
 옵션이 표시된 대로 설정되어 있지 않으면 **xml** 데이터 형식의 메서드에 있는 쿼리 및 수정 작업이 실패합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
