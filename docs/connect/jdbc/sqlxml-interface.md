---
title: SQLXML 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72cccce89d5e30a92f38b956c8b7996949d3bb46
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027697"
---
# <a name="sqlxml-interface"></a>SQLXML 인터페이스

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

JDBC 드라이버에서는 java.sql.SQLXML 인터페이스를 소개하는 JDBC 4.0 API가 지원됩니다. SQLXML 인터페이스는 XML 데이터에 대한 상호 작용 및 조작을 수행하는 메서드를 정의합니다. **SQLXML** 데이터 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml** 데이터 형식에 매핑됩니다.  
  
SQLXML 인터페이스는 **String**, **Reader** 또는 **Writer** 또는 **Stream**으로서 XML 값에 액세스하는 메서드를 제공합니다. XML 값은 또한 **Source**를 통해 액세스하거나 **Result**로 설정할 수 있는데 이들은 DOM(문서 개체 모델), SAX(Simple API for XML), StAX(Streaming API for XML)와 같은 XML 파서와 XSLT 변환 및 XPath와 함께 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  

다음 표에서는 SQLXML 인터페이스에 정의된 메서드에 대해 설명합니다.  
  
|메서드 구문|메서드 설명|  
|-------------------|------------------------|  
|[void free()](https://go.microsoft.com/fwlink/?LinkId=131685)|이 메서드는 SQLXML 개체 및 이 개체가 보유한 리소스를 해제합니다.|  
|[InputStream getBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131754)|SQLXML에서 데이터를 읽기 위한 입력 스트림을 반환합니다.|  
|[Reader getCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131755)|**XML** 데이터를 java.io.Reader 개체 또는 문자 스트림으로 반환합니다.|  
|[T extends Source T getSource(Class\<T> sourceClass)](https://go.microsoft.com/fwlink/?LinkId=131756)|이 **SQLXML** 개체에서 지정한 **XML** 값을 읽기 위한 **소스**를 반환 합니다.<br /><br /> **참고:**  getSource 메서드는 원본 javax.xml.transform.dom.DOMSource, javax.xml.transform.sax.SAXSource, javax.xml.transform.stax.StAXSource 및 java.io.InputStream을 지원합니다.|  
|[String getString()](https://go.microsoft.com/fwlink/?LinkId=131757)|이 SQLXML 개체가 지정하는 **XML** 값의 문자열 표현을 반환합니다.|  
|[OutputStream setBinaryStream()](https://go.microsoft.com/fwlink/?LinkId=131758)|이 SQLXML 개체가 나타내는 **XML** 값을 쓰는 데 사용할 수 있는 스트림을 검색합니다.|  
|[Writer setCharacterStream()](https://go.microsoft.com/fwlink/?LinkId=131759)|이 SQLXML 개체가 나타내는 **XML** 값을 쓰는 데 사용할 스트림을 반환합니다.|  
|[T extends Result T setResult(Class\<T> resultClass)](https://go.microsoft.com/fwlink/?LinkId=131760)|이 **SQLXML** 개체에서 지정한 **XML** 값을 설정하기 위한 **결과**를 반환합니다.<br /><br /> **참고:** setResult 메서드는 원본 javax.xml.transform.dom.DOMResult, javax.xml.transform.sax.SAXResult, javax.xml.transform.stax.StaxResult 및 java.io.OutputStream을 지원합니다.|  
|[void setString(String value)](https://go.microsoft.com/fwlink/?LinkId=131762)|이 SQLXML 개체가 지정하는 XML 값을 지정된 **String** 표현으로 설정합니다.|  
  
애플리케이션은 SQLXML 개체에 XML 값을 한 번만 읽고 쓸 수 있습니다.  
  
free() 메서드가 호출되면 SQLXML 개체가 더 이상 유효하지 않고 읽거나 쓸 수 없게 됩니다. 애플리케이션이 해당 SQLXML 개체에 대해 free() 메서드 이외의 메서드를 호출하려고 시도하면 예외가 throw됩니다.  
  
애플리케이션에서 getter 메서드인 getSource, getCharacterStream, getBinaryStream 및 getString 중 하나를 호출하면 SQLXML 개체를 읽거나 쓸 수 없게 됩니다.  
  
애플리케이션에서 getter 메서드인 setResult, setCharacterStream, setBinaryStream 및 setString 중 하나를 호출하면 SQLXML 개체를 쓰거나 읽을 수 없게 됩니다.  
  
## <a name="see-also"></a>참고 항목  

[XML 데이터 지원](../../connect/jdbc/supporting-xml-data.md)  
