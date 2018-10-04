---
title: SqlXmlCommand 개체 (SQLXML 관리 되는 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- void ExecuteNonQuery() method
- namespaces property
- Stream ExecuteStream() method
- CommandType property
- RootTag property
- OutputEncoding property
- XmlReader ExecuteXmlReader() method
- Managed Classes [SQLXML], SqlXmlCommand object
- SQLXML Managed Classes, SqlXmlCommand object
- Base Path property
- void ClearParameters() method
- public void ExecuteToStream(Stream outputStream) method
- SqlXmlCommand object
- CommandText property
- XslPath property
- SchemaPath property
- SqlXmlParameter CreateParameter() method
- ClientSideXML property
- CommandStream property
ms.assetid: c1f9e0bb-a89d-4d6a-a96e-289ef516a3a6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0aba35418c1a7759f5c083bd5e5f7485118cbfc3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207223"
---
# <a name="sqlxmlcommand-object-sqlxml-managed-classes"></a>SqlXmlCommand 개체(SQLXML 관리되는 클래스)
  SqlXmlCommand 개체에 대 한 생성자는 다음과 같습니다.  
  
```  
public SqlXmlCommand(string cnString)  
```  
  
 여기서 `cnString`은 서버, 데이터베이스 및 로그인 정보를 식별하는 ADO 또는 OLEDB 연결 문자열입니다(예: `Provider=SQLOLEDB; Server=(local); database=AdventureWorks; Integrated Security=SSPI"`).  
  
 연결 문자열에서 `Provider`는 SQLOLEDB여야 하고 `Data Provider`는 공급자 문자열에 포함되면 안 됩니다.  
  
 작업 샘플을 보려면 [SQL 쿼리 실행 &#40;SQLXML Managed Classes&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)합니다.  
  
## <a name="methods"></a>메서드  
 TheSqlXmlCommand 개체는 명령을 실행 하기 위한 다음 방법을 비롯 하 여 몇 가지 메서드를 지원 합니다.  
  
 void executenonquery)  
 명령을 실행하지만 아무것도 반환하지 않습니다. 이 메서드는 쿼리를 사용하지 않는 명령, 즉 아무것도 반환하지 않는 명령을 실행하려는 경우에 유용합니다. 예를 들어 레코드를 업데이트하지만 아무것도 반환하지 않는 DiffGram 또는 updategram이 이러한 메서드에 속합니다.  
  
 Stream executestream)  
 새 Stream 개체를 반환합니다. 이 메서드는 쿼리 결과를 새 스트림에 반환하려는 경우에 유용합니다. 작업 샘플을 보려면 [SQL 쿼리 실행 &#40;SQLXML Managed Classes&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)합니다.  
  
 public void ExecuteToStream (Stream outputStream)  
 쿼리 결과를 기존 스트림에 씁니다. 이 메서드는 결과 (예: 쿼리 결과 System.Web.HttpResponse.OutputStream 쓸) 추가 해야 하는 스트림이 있는 경우에 유용 합니다. 작업 샘플을 보려면 [SQL 쿼리 실행 &#40;SQLXML Managed Classes&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)합니다.  
  
 XmlReader executexmlreader)  
 XmlReader 개체를 반환합니다. XmlReader 개체의 데이터를 직접 조작 하거나 System.Xml의 포함 된 연결 가능한 아키텍처 플러그 인이 메서드를 사용할 수 있습니다. 자세한 내용은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 설명서를 참조하십시오. 작업 샘플을 보려면 [ExecuteXMLReader 메서드를 사용 하 여 SQL 쿼리 실행](executing-sql-queries-by-using-the-executexmlreader-method.md)합니다.  
  
 TheSqlXmlCommand 개체는 이러한 추가 메서드를 지원합니다.  
  
 SqlXmlParameter createparameter)  
 SqlXmlParameter 개체를 만듭니다. 에 대 한 값을 설정할 수는 *이름을* 하 고 *값* 이 개체의 매개 변수입니다. 이 메서드는 명령에 매개 변수를 전달하려는 경우에 유용합니다. 작업 샘플을 보려면 [SQL 쿼리 실행 &#40;SQLXML Managed Classes&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)합니다.  
  
 void clearparameters)  
 지정된 명령 개체에 대해 만든 매개 변수를 지웁니다. 이 메서드는 동일한 명령 개체에 여러 개의 쿼리를 실행하려는 경우에 유용합니다.  
  
## <a name="properties"></a>속성  
 SqlXmlCommand 개체는 또한 이러한 속성을 지원합니다.  
  
 ClientSideXml  
 True로 설정할 경우 행 집합과 XML 사이의 변환을 서버 대신 클라이언트에서 수행하도록 지정합니다. 이 속성은 성능 부하를 중간 계층으로 이동하려는 경우에 유용합니다. 이 속성을 사용하면 기존의 저장 프로시저를 FOR XML에 래핑하여 XML 출력을 얻을 수도 있습니다.  
  
 SchemaPath  
 디렉터리 경로를 포함한 매핑 스키마의 이름입니다(예: C:\x\y\MySchema.xml). 이 속성은 XPath 쿼리의 매핑 스키마를 지정할 때 유용합니다. 이 속성에는 절대 경로 또는 상대 경로를 지정할 수 있으며 경로 상대 경로, 상대 경로를 확인할 기본 경로에 지정 된 기본 경로 사용 됩니다. 기본 경로가 지정되어 있지 않으면 상대 경로는 현재 디렉터리에 상대적입니다. 작업 샘플을 보려면 [.NET 환경에서 SQLXML 기능 액세스](accessing-sqlxml-functionality-in-the-net-environment.md)합니다.  
  
 XslPath  
 디렉터리 경로를 포함한 XSL 파일의 이름입니다. 이 속성에는 절대 경로 또는 상대 경로를 지정할 수 있으며 경로 상대 경로, 상대 경로를 확인할 기본 경로에 지정 된 기본 경로 사용 됩니다. 기본 경로가 지정되어 있지 않으면 상대 경로는 현재 디렉터리에 상대적입니다. 작업 샘플을 보려면 [XSL 변환 적용 &#40;SQLXML Managed Classes&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md)합니다.  
  
 기본 경로  
 기본 경로(디렉터리 경로)입니다. 이 속성은 XSL 파일 (사용 하 여 XslPath 속성), (SchemaPath 속성)을 사용 하 여 매핑 스키마 파일 또는 XML 서식 파일에서 외부 스키마 참조에 지정 된 상대 경로 확인 하는 데 유용 (사용 하 여 지정 된 `mapping-schema` 특성)입니다.  
  
 OutputEncoding  
 명령을 실행하여 반환되는 스트림의 인코딩을 지정합니다. 이 속성은 반환되는 스트림에 특정 인코딩을 사용하려는 경우에 유용합니다. 일반적으로 UTF-8, ANSI 및 유니코드와 같은 인코딩이 사용되며 기본 인코딩은 UTF-8입니다.  
  
 네임스페이스  
 네임스페이스를 사용하는 XPath 쿼리를 실행할 수 있습니다. 네임 스페이스가 있는 XPath 쿼리 하는 방법에 대 한 자세한 내용은 참조 하세요. [네임 스페이스가 있는 XPath 쿼리 실행 &#40;SQLXML Managed Classes&#41;](executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)합니다. 작업 샘플을 보려면 [XPath 쿼리 실행 &#40;SQLXML Managed Classes&#41;](executing-xpath-queries-sqlxml-managed-classes.md)합니다.  
  
 RootTag  
 명령을 실행하여 생성된 XML의 단일 루트 요소를 제공합니다. 유효한 XML 문서에는 루트 수준의 단일 태그가 필요합니다. 명령을 실행하여 XML 조각(단일 최상위 요소가 없음)이 생성된 경우, 반환되는 XML의 루트 요소를 지정할 수 있습니다. 작업 샘플을 보려면 [XSL 변환 적용 &#40;SQLXML Managed Classes&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md)합니다.  
  
 CommandText  
 명령 텍스트입니다. 이 속성은 실행할 명령의 텍스트를 지정하는 데 사용됩니다. 작업 샘플을 보려면 [SQL 쿼리 실행 &#40;SQLXML Managed Classes&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)합니다.  
  
 CommandStream  
 명령 스트림입니다. 이 속성은 파일(예: XML 템플릿)에서 명령을 실행하려는 경우에 유용합니다. 사용할 때 CommandStream에만 **"템플릿"**, **"UpdateGram"** 하 고 **"DiffGram" CommandType** 값이 지원 됩니다. 작업 샘플을 보려면 [CommandStream 속성을 사용 하 여 템플릿 파일 실행](executing-template-files-by-using-the-commandstream-property.md)합니다.  
  
 CommandType  
 명령의 형식을 식별합니다. 이 속성은 실행할 명령의 형식을 지정하는 데 사용됩니다. 명령 형식은 다음 표에 나와 있는 값에 따라 결정됩니다. 작업 샘플을 보려면 [.NET 환경에서 SQLXML 기능 액세스](accessing-sqlxml-functionality-in-the-net-environment.md)합니다.  
  
|값|Description|  
|-----------|-----------------|  
|SqlXmlCommandType.Sql|SQL 명령(예: `SELECT * FROM Employees FOR XML AUTO`)을 실행합니다.|  
|SqlXmlCommandType.XPath|XPath 명령(예: `Employees[@EmployeeID=1]`)을 실행합니다.|  
|SqlXmlCommandType.Template|XML 템플릿을 실행합니다.|  
|SqlXmlCommandType.TemplateFile|지정된 경로에 있는 템플릿 파일을 실행합니다.|  
|SqlXmlCommandType.UpdateGram|Updategram을 실행합니다.|  
|SqlXmlCommandType.Diffgram|DiffGram을 실행합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SqlXmlParameter 개체 &#40;SQLXML 관리 되는 클래스&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)   
 [SqlXmlAdapter 개체 &#40;SQLXML 관리 되는 클래스&#41;](sqlxml-managed-classes-sqlxmladapter-object.md)  
  
  
