---
title: XML 데이터 검색 및 쿼리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML data [SQL Server], retrieving
- XML instance retrieval
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f556bfccdd117b23db36bb9551e885f4c38614e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241206"
---
# <a name="retrieve-and-query-xml-data"></a>XML 데이터 검색 및 쿼리
  이 항목에서는 XML 데이터를 쿼리할 때 지정해야 하는 쿼리 옵션에 대해 설명합니다. 또한 XML 인스턴스가 데이터베이스에 저장될 때 보존되지 않는 인스턴스의 일부분에 대해 설명합니다.  
  
##  <a name="features"></a> 보존되지 않는 XML 인스턴스 기능  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 XML 인스턴스의 내용을 보존하지만 XML 데이터 모델에서 중요하다고 간주되지 않는 XML 인스턴스의 측면은 보존하지 않습니다. 즉, 검색된 XML 인스턴스는 서버에 저장된 인스턴스와 다를 수 있지만 동일한 정보를 포함한다는 의미입니다.  
  
### <a name="xml-declaration"></a>XML 선언  
 인스턴스가 데이터베이스에 저장될 때 인스턴스에 있는 XML 선언이 보존되지 않습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 결과는 `<doc/>`입니다.  
  
 XML 데이터가 `xml` 데이터 형식 인스턴스에 저장될 때 `<?xml version='1.0'?>`과 같은 XML 선언이 보존되지 않습니다. 이것은 의도적인 것입니다. XML 선언 () 및 해당 특성 (버전/encoding/stand-alone) 없어진다 데이터 형식으로 변환 됩니다 `xml`합니다. XML 선언은 XML 파서에 대한 지시어로 취급됩니다. XML 데이터는 내부적으로 ucs-2로 저장되며 XML 인스턴스의 다른 모든 PI는 보존됩니다.  
  
  
### <a name="order-of-attributes"></a>특성 순서  
 XML 인스턴스의 특성 순서는 보존되지 않습니다. `xml` 유형의 열에 저장된 XML 인스턴스를 쿼리할 때 결과 XML의 특성 순서는 원래 XML 인스턴스와 다를 수 있습니다.  
  
  
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
 네임스페이스 접두사는 유지되지 않습니다. `xml` 유형의 열에 대해 XQuery를 지정하는 경우 직렬화된 XML 결과는 다른 네임스페이스 접두사를 반환할 수 있습니다.  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 결과의 네임스페이스 접두사는 다를 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
  
##  <a name="query"></a> 필수 쿼리 옵션 설정  
 쿼리할 때 `xml` 유형의 열 또는 변수를 사용 하 여 `xml` 표시 된 것 처럼 데이터 형식 메서드를 다음 옵션을 설정 해야 합니다.  
  
|SET 옵션|필요한 값|  
|-----------------|---------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNINGS|ON|  
|ARITHABORT|ON|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
  
 에 표시 된 대로, 쿼리 및 수정 옵션을 설정 하지 않으면 `xml` 데이터 형식 메서드가 실패 합니다.  
  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터 인스턴스 만들기](create-instances-of-xml-data.md)  
  
  
