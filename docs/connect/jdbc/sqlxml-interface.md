---
title: "SQLXML 인터페이스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c636345439175c516b647a2951ac3bfa8824b06
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlxml-interface"></a>SQLXML 인터페이스
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 드라이버에서는 java.sql.SQLXML 인터페이스를 소개하는 JDBC 4.0 API가 지원됩니다. SQLXML 인터페이스는 XML 데이터에 대한 상호 작용 및 조작을 수행하는 메서드를 정의합니다. **SQLXML** 에 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** 데이터 형식입니다.  
  
 XML 값에 액세스 하기 위한 메서드를 제공 하는 SQLXML 인터페이스는 **문자열**, **판독기** 또는 **기록기**로 **스트림**합니다. XML 값을 통해 액세스할 수도 있습니다는 **소스** 나 식으로 설정할는 **결과**는 문서 개체 모델 (DOM), 간단한 API와 같은 XML 파서 Api와 XML (SAX) 및 스트리밍 API에 대 한 for XML), StAX (으로 사용 xslt 변형으로 제대로 되 고 XPath입니다.  
  
## <a name="remarks"></a>주의  
 다음 표에서는 SQLXML 인터페이스에 정의된 메서드에 대해 설명합니다.  
  
|메서드 구문|메서드 설명|  
|-------------------|------------------------|  
|[free (void)](http://go.microsoft.com/fwlink/?LinkId=131685)|이 메서드는 SQLXML 개체 및 이 개체가 보유한 리소스를 해제합니다.|  
|[InputStream getBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131754)|SQLXML에서 데이터를 읽기 위한 입력 스트림을 반환합니다.|  
|[판독기 getCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131755)|반환 된 **XML** 데이터를 java.io.Reader 개체 또는 문자 스트림으로 합니다.|  
|[T 소스 T getSource 확장 (클래스\<T > sourceClass)](http://go.microsoft.com/fwlink/?LinkId=131756)|반환 된 **소스** 읽기에 대 한는 **XML** 이 지정 된 값 **SQLXML** 개체입니다.<br /><br /> **참고:** getSource 메서드에서 지원 다음 소스: javax.xml.transform.dom.DOMSource, javax.xml.transform.sax.SAXSource, javax.xml.transform.stax.StAXSource 및 java.io.InputStream 합니다.|  
|[문자열 getString()](http://go.microsoft.com/fwlink/?LinkId=131757)|문자열 표현을 반환 된 **XML** 이 SQLXML 개체가 지정 된 값입니다.|  
|[OutputStream setBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131758)|쓰는 데 사용할 수 있는 스트림을 검색는 **XML** 이 SQLXML 개체가 나타내는 값입니다.|  
|[기록기 setCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131759)|쓰는 데 사용할 스트림을 반환 된 **XML** 이 SQLXML 개체가 나타내는 값입니다.|  
|[T 결과 T setResult 확장 (클래스\<T > resultClass)](http://go.microsoft.com/fwlink/?LinkId=131760)|반환 된 **결과** 설정에 대 한는 **XML** 이 지정 된 값 **SQLXML** 개체입니다.<br /><br /> **참고:** setResult 메서드에서 지원 다음 소스: javax.xml.transform.dom.DOMResult, javax.xml.transform.sax.SAXResult, javax.xml.transform.stax.StaxResult 및 java.io.outputstream을 지원 합니다.|  
|[void setString(String value)](http://go.microsoft.com/fwlink/?LinkId=131762)|지정 된이 SQLXML 개체가 지정 된 XML 값을 설정 **문자열** 표현 합니다.|  
  
 응용 프로그램은 SQLXML 개체에 XML 값을 한 번만 읽고 쓸 수 있습니다.  
  
 Free () 메서드를 호출할 때 SQLXML 개체는 유효 하지 않게 되어은 읽을 없으며 쓰기 가능한 합니다. 응용 프로그램을 free () 메서드 이외의 해당 SQLXML 개체에서 메서드를 호출 하려고 하는 경우 예외가 throw 됩니다.  
  
 응용 프로그램이 다음 getter 메서드 중 하나를 호출 하는 경우 SQLXML 개체 읽거나 쓸 수 됩니다: getSource, getCharacterStream, getBinaryStream, 및 getString 합니다.  
  
 응용 프로그램이 다음 setter 메서드 중 하나를 호출 하는 경우 SQLXML 개체 읽거나 쓸 수:, setBinaryStream, setCharacterStream, setResult 및 setString 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터 지원](../../connect/jdbc/supporting-xml-data.md)  
  
  

