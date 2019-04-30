---
title: XML 데이터 로드 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML data [SQL Server], loading
- loading XML data
ms.assetid: d1741e8d-f44e-49ec-9f14-10208b5468a7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb3365195e3a64353fb0cbd45e832cd0206f678e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241309"
---
# <a name="load-xml-data"></a>XML 데이터 로드
  XML 데이터를 여러 가지 방법으로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 으로 전송할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 [n]text 또는 image 열에 데이터가 있으면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 사용하여 테이블을 가져올 수 있습니다. ALTER TABLE 문을 사용하여 열 유형을 XML로 바꿉니다.  
  
-   bcp out을 사용하여 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 대량 복사한 다음 bcp in을 사용하여 데이터를 최신 버전 데이터베이스로 대량 삽입할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 관계형 열에 데이터가 있는 경우 [n]text 열 및 행 식별자의 경우 기본 키 열(옵션)이 포함된 새 테이블을 만듭니다. 클라이언트 쪽 프로그래밍을 사용하여 FOR XML로 서버에서 생성된 XML을 검색하고 이를 `[n]text` 열에 씁니다. 그런 다음 앞에서 언급한 기술을 사용하여 데이터를 최신 데이터베이스에 전송합니다. 최신 데이터베이스에 있는 XML 열로 XML을 직접 작성하도록 선택할 수 있습니다.  
  
## <a name="bulk-loading-xml-data"></a>XML 데이터 대량 로드  
 bcp와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 대량 로드 기능을 사용하여 XML 데이터를 서버에 대량 로드할 수 있습니다. OPENROWSET을 사용하면 데이터를 파일에서 XML 열로 로드할 수 있습니다. 다음 예에서는 이러한 점을 보여 줍니다.  
  
##### <a name="example-loading-xml-from-files"></a>예: 파일에서 XML 로드  
 이 예에서는 테이블 T에 행을 삽입하는 방법을 보여 줍니다. XML 열의 값은 C:\MyFile\xmlfile.xml 파일로부터 CLOB으로 로드되고 정수 열에는 값 10이 제공됩니다.  
  
```  
INSERT INTO T  
SELECT 10, xCol  
FROM    (SELECT *      
    FROM OPENROWSET (BULK 'C:\MyFile\xmlfile.xml', SINGLE_CLOB)   
 AS xCol) AS R(xCol)  
```  
  
## <a name="text-encoding"></a>텍스트 인코딩  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 XML 데이터를 유니코드(UTF-16)로 저장합니다. 서버에서 검색된 XML 데이터는 UTF-16 인코딩으로 출력됩니다. 다른 인코딩이 필요한 경우 검색된 데이터에서 필요한 변환을 수행해야 합니다. 일부 경우 XML 데이터는 다른 인코딩으로 표시될 수 있습니다. 이 경우 데이터를 로드하는 동안 주의해야 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
-   XML 텍스트가 유니코드(UCS-2, UTF-16)인 경우 문제 없이 이를 XML 열, 변수 또는 매개 변수에 할당할 수 있습니다.  
  
-   인코딩이 유니코드가 아니고 암시적인 경우 원본 코드 페이지로 인해 데이터베이스의 문자열 코드 페이지는 로드하려는 코드 지점과 호환되거나 동일해야 합니다. 필요한 경우 COLLATE를 사용합니다. 이러한 서버 코드 페이지가 없는 경우 명시적 XML 선언을 올바른 인코딩으로 추가해야 합니다.  
  
-   명시적 인코딩을 사용하려면 코드 페이지와 상호 작용이 없는 `varbinary()` 유형을 사용하거나 적합한 코드 페이지의 문자열 유형을 사용합니다. 그런 다음 데이터를 XML 열, 변수 또는 매개 변수에 할당합니다.  
  
### <a name="example-explicitly-specifying-an-encoding"></a>예: 인코딩을 명시적으로 지정  
 명시적 XML 선언 없이 `varchar(max)`로 저장된 XML 문서인 vcdoc가 있다고 가정해 보십시오. 다음 문은 "iso8859-1" 인코딩으로 XML 선언을 추가하고 XML 문서를 연결하고 결과를 `varbinary(max)`로 캐스팅하여 바이트 표현이 유지되도록 한 다음 마지막으로 XML로 캐스팅합니다. 이렇게 하면 XML 프로세서가 지정된 "iso8859-1" 인코딩에 따라 데이터를 구문 분석하고 문자열 값에 대한 해당 UTF-16 표현을 생성할 수 있습니다.  
  
```  
SELECT CAST(   
CAST (('<?xml version="1.0" encoding="iso8859-1"?>'+ vcdoc) AS VARBINARY (MAX))   
 AS XML)  
```  
  
### <a name="string-encoding-incompatibilities"></a>문자열 인코딩 비호환성  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쿼리 편집기 창에서 XML을 문자열 리터럴로 복사 및 붙여 넣는 경우 [N]VARCHAR 문자열 인코딩이 호환되지 않는 경우가 발생할 수 있습니다. 이것은 해당 XML 인스턴스의 인코딩에 따라 달라집니다. 대부분의 경우 XML 선언을 제거해야 할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
  <xsd:schema ...  
```  
  
 그런 다음 해당 XML 인스턴스를 유니코드 인스턴스로 만들기 위해 N을 포함시켜야 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
-- Assign XML instance to a variable.  
DECLARE @X XML  
SET @X = N'...'  
-- Insert XML instance into an xml type column.  
INSERT INTO T VALUES (N'...')  
-- Create an XML schema collection  
CREATE XML SCHEMA COLLECTION XMLCOLL1 AS N'<xsd:schema ... '  
```  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터&#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
