---
title: XML 태스크를 사용하여 XML 유효성 검사 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- XML validation
- XML, validating
ms.assetid: 224fc025-c21f-4d43-aa9d-5ffac337f9b0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2617ab51ffdde7bd8986c0a7d508067ac2686e1e
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53203262"
---
# <a name="validate-xml-with-the-xml-task"></a>Validate XML with the XML Task
  XML 태스크의 **ValidationDetails** 속성을 사용하도록 설정하여 XML 문서의 유효성을 검사하고 풍부한 오류 출력을 가져올 수 있습니다.  
  
 다음 스크린샷에는 다양한 오류 출력을 제공하는 XML 유효성 검사에 필요한 설정이 포함된 **XML 태스크 편집기** 가 나와 있습니다.  
  
 ![XML 태스크 편집기에서 XML 태스크 속성](../../integration-services/control-flow/media/xmltaskproperties.jpg "XML 태스크 편집기에서 XML 태스크 속성")  
  
 **ValidationDetails** 속성을 사용할 수 있게 되기 전에 먼저 XML 태스크에 의해 수행된 XML 유효성 검사가 오류 또는 해당 위치에 대한 정보 없이 true 또는 false 결과만 반환했습니다. 이제는 **ValidationDetails** 를 true로 설정할 경우 출력 파일에 줄 번호 및 위치를 포함하여 모든 오류에 대한 자세한 정보가 포함됩니다. 이 정보를 사용하여 XML 문서의 오류를 이해하고, 찾고, 수정할 수 있습니다.  
  
 대형 XML 문서 및 많은 수의 오류에 사용할 수 있도록 XML 유효성 검사 기능을 쉽게 확장할 수 있습니다. 출력 파일 자체가 XML 형식이므로 출력을 쿼리하고 분석할 수 있습니다. 예를 들어 출력에 오류가 많이 포함되어 있으면 이 항목에서 설명하는 대로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 사용하여 오류를 그룹화할 수 있습니다.  
  
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]([!INCLUDE[ssIS](../../includes/ssis-md.md)])는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 서비스 팩 2에서 **ValidationDetails** 속성을 도입했습니다. 이 속성은 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서도 사용할 수 있습니다.  
  
## <a name="sample-output-for-xml-thats-valid"></a>유효한 XML의 샘플 출력  
 아래에는 유효한 XML 파일의 유효성 결과가 포함된 샘플 출력 파일이 나와 있습니다.  
  
```xml  
  
<root xmlns:ns="https://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>true</result>  
        <errors>0</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:27:22.087</startTime>  
        <endTime>2015-05-28T10:29:07.007</endTime>  
        <xmlFile>d:\Temp\TestData.xml</xmlFile>  
        <xsdFile>d:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages />  
</root>  
```  
  
## <a name="sample-output-for-xml-thats-not-valid"></a>유효하지 않은 XML의 샘플 출력  
 아래에는 오류가 많지 않은 XML 파일의 유효성 결과가 포함된 샘플 출력 파일이 나와 있습니다. 코드를 쉽게 확인할 수 있도록 \<error> 요소의 텍스트에 줄 바꿈이 적용되었습니다.  
  
```xml  
  
<root xmlns:ns="https://schemas.microsoft.com/xmltools/2002/xmlvalidation">  
    <metadata>  
        <result>false</result>  
        <errors>2</errors>  
        <warnings>0</warnings>  
        <startTime>2015-05-28T10:45:09.538</startTime>  
        <endTime>2015-05-28T10:45:09.558</endTime>  
        <xmlFile>C:\Temp\TestData.xml</xmlFile>  
        <xsdFile>C:\Temp\TestSchema.xsd</xsdFile>  
    </metadata>  
    <messages>  
        <error line="5" position="26">The 'ApplicantRole' element is invalid - The value 'wer3' is invalid  
    according to its datatype 'ApplicantRoleType' - The Enumeration constraint failed.</error>  
        <error line="16" position="28">The 'Phone' element is invalid - The value 'we3056666666' is invalid  
     according to its datatype 'phone' - The Pattern constraint failed.</error>  
    </messages>  
</root>  
```  
  
## <a name="analyze-xml-validation-output-with-a-transact-sql-query"></a>Transact-SQL 쿼리를 통해 XML 유효성 검사 출력 분석  
 XML 유효성 검사의 출력에 오류가 많이 포함되어 있으면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 출력을 로드할 수 있습니다. 그런 다음 WHERE, GROUP BY, ORDER BY, JOIN 등을 비롯한 T-SQL 언어의 모든 기능을 사용하여 오류 목록을 분석할 수 있습니다.  
  
```sql  
DECLARE @xml XML;  
  
SELECT @xml = XmlDoc     
FROM OPENROWSET (BULK N'C:\Temp\XMLValidation_2016-02-212T10-41-00.xml', SINGLE_BLOB) AS Tab(XmlDoc);  
  
-- Query # 1, flat list of errors  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('https://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT * FROM rs;  
-- WHERE error LIKE '%whatever_string%'  
  
-- Query # 2, count of errors grouped by the error message  
-- convert to relational/rectangular  
;WITH XMLNAMESPACES ('https://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS  
(  
SELECT col.value('@line','INT') AS line  
     , col.value('@position','INT') AS position  
     , col.value('.','VARCHAR(1024)') AS error  
FROM @XML.nodes('/root/messages/error') AS tab(col)  
)  
SELECT COALESCE(error,'Total # of errors:') AS [error], COUNT(*) AS [counter]  
FROM rs  
GROUP BY GROUPING SETS ((error), ())  
ORDER BY 2 DESC, COALESCE(error, 'Z');  
  
```  
  
 위 텍스트에 나와 있는 두 번째 샘플 쿼리를 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 표시한 결과는 다음과 같습니다.  
  
 ![Management Studio에서 XML 오류를 그룹화하기 위해 쿼리](../../integration-services/control-flow/media/queryforxmlerrors.jpg "Management Studio에서 XML 오류를 그룹화하기 위해 쿼리")  
  
## <a name="see-also"></a>참고 항목  
 [XML 태스크](../../integration-services/control-flow/xml-task.md)   
 [XML 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/xml-task-editor-general-page.md)  
  
  
