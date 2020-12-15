---
title: SQLXMLOLEDB 공급자 소개 (SQLXML)
description: ADO(ActiveX Data Objects) (ADO)를 통해 SQLXML 기능을 노출 하는 OLE DB 공급자 인 SQLXMLOLEDB 공급자에 대해 알아봅니다.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, properties
- adExecuteStream flag
- SQLXMLOLEDB Provider, about SQLXMLOLEDB Provider
ms.assetid: 2e3f3817-4209-4bf4-9f46-248c95bc6f1b
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6b3d36e6aae398c8b480a800cdd2dc6064eb220e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462894"
---
# <a name="introduction-to-the-sqlxmloledb-provider-sqlxml-40"></a>SQLXMLOLEDB 공급자 소개(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  SQLXMLOLEDB 공급자는 ADO(ActiveX Data Objects)를 통해 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 기능을 노출하는 OLE DB Provider입니다. 하지만 이 공급자는 ADO의 "출력 스트림에 쓰기" 모드에서만 명령을 실행할 수 있습니다. SQLXMLOLEDB 공급자는 행 집합 공급자가 아닙니다. 명령을 실행할 때 adExecuteStream 플래그를 지정 해야 합니다 .이 플래그는 지정 된 출력 스트림을 ADO에 사용 하도록 지시 합니다.  
  
 다음 예에서는 adExecuteStream 플래그가 지정 된 Execute 명령에 대 한 구문을 보여 줍니다.  
  
```  
Dim oTestCommand As New ADODB.Command  
...  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Execute , , adExecuteStream  
...  
```  
  
## <a name="sqlxmloledb-provider-specific-properties"></a>SQLXMLOLEDB 공급자별 속성  
 SQLXMLOLEDB 공급자는 다음과 같은 공급자별 연결 속성을 노출합니다.  
  
|연결<br /><br /> 속성(property)|기본값<br /><br /> (있는 경우)|설명|  
|-----------------------------|----------------------------|-----------------|  
|데이터 공급자||SQLXMLOLEDB에서 명령을 실행하는 데 사용하는 OLE DB Provider의 PROGID를 제공합니다. SQLXML 4.0 및 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터 이 공급자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 내에 포함되어 있으므로 이 속성 값은 "SQLNCLI11"으로 제한됩니다. 자세한 내용은 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)을 참조하세요.|  
  
 SQLXMLOLEDB 공급자는 다음과 같은 공급자별 명령 속성을 노출합니다.  
  
|명령<br /><br /> 속성(property)|기본값<br /><br /> (있는 경우)|설명|  
|--------------------------|----------------------------|-----------------|  
|기본 경로|""|기본 파일 경로를 지정합니다. 기본 파일 경로는 XSL(XML Stylesheet Language) 또는 매핑 스키마 파일의 위치를 지정하는 데 사용됩니다. 기본 파일 경로는 XSL 또는 매핑 스키마 속성에 지정 된 XSL 또는 매핑 스키마 파일의 상대 경로를 확인 하는 데도 사용 됩니다.<br /><br /> 이 속성을 사용 하는 예는 [XPath 쿼리 실행 &#40;SQLXMLOLEDB Provider&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md)를 참조 하세요.|  
|ClientSideXML|False|행 집합을 XML로 변환하는 프로세스가 서버 대신 클라이언트에서 수행되도록 하려면 이 속성을 True로 설정합니다. 이 속성은 성능 부하를 중간 계층으로 이동하려는 경우에 유용합니다.<br /><br /> 이 속성을 사용 하는 예는 [sql 쿼리 실행 &#40;SQLXMLOLEDB provider&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md) 또는 [Sql 쿼리가 포함 된 템플릿 실행 &#40;SQLXMLOLEDB provider&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md)를 참조 하세요.|  
|콘텐츠 유형||출력 내용 유형을 반환합니다. READ ONLY 속성입니다.<br /><br /> 이 속성은 내용 유형(예: TEXT/XML, TEXT/HTML, image/jpeg 등)에 대한 정보를 브라우저에 제공합니다. 이 속성의 값은 HTTP 헤더의 일부로 브라우저로 전송 되는 **content-type** 필드가 됩니다. 여기에는 본문으로 전송 되는 문서에 대 한 MIME 형식 (다목적 인터넷 메일 확장 프로그램)이 포함 됩니다.|  
|매핑 스키마|NULL|클라이언트 애플리케이션이 매핑 스키마(XDR 또는 XSD)에 대해 XPath 쿼리를 실행하는 경우 이 속성은 매핑 스키마의 이름을 지정하는 데 사용됩니다.<br /><br /> 지정된 경로는 상대 경로(xyz/abc/MySchema.xml) 또는 절대 경로(C:\MyFolder\abc\MySchema.xml)일 수 있습니다.<br /><br /> 상대 경로를 지정 하는 경우 기본 경로 속성으로 지정 된 기본 경로를 사용 하 여 상대 경로를 확인 합니다. 기본 경로 속성에 경로가 지정 되지 않은 경우 상대 경로는 현재 디렉터리를 기준으로 합니다.<br /><br /> 매핑 스키마 속성에 대 한 값을 지정할 때 로컬 디렉터리 경로 또는 URL (https://)을 지정할 수 있습니다. URL을 지정 하는 경우 프록시 서버를 통해 HTTP 및 HTTPS 서버에 액세스 하도록 WinHTTP를 구성 해야 합니다. Proxycfg.exe 유틸리티를 실행하여 이 작업을 수행할 수 있습니다. 자세한 내용은 MSDN 라이브러리의 "WinHTTP 프록시 구성 유틸리티 사용"을 참조하십시오.<br /><br /> 이 속성을 사용 하는 예는 [XPath 쿼리 실행 &#40;SQLXMLOLEDB Provider&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-sqlxmloledb-provider.md)를 참조 하세요.|  
|네임스페이스||이 속성을 사용하면 네임스페이스를 사용하는 XPath 쿼리를 실행할 수 있습니다. 이 속성을 사용 하는 예제는 [SQLXMLOLEDB Provider&#41;&#40;네임 스페이스를 사용 하 여 XPath 쿼리 실행 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md)을 참조 하세요.|  
|ss Stream Flags||이 속성은 보안 제한의 특정 유형을 지정하는 데 사용됩니다. 예를 들어 파일에 대한 URL 참조나 파일(예: 외부 사이트)에 대한 절대 경로를 허용하지 않을 수 있습니다. 또는 템플릿에서 쿼리를 허용하지 않을 수도 있습니다.<br /><br /> 이 속성에는 다음과 같은 값을 할당할 수 있습니다.<br /><br /> 1 = STREAM_FLAGS_DISALLOW_URL 2 = STREAM_FLAGS_DISALLOW_ABSOLUTE_PATH 4 = STREAM_FLAGS_DISALLOW_QUERY 8 = STREAM_FLAGS_       DONTCACHEMAPPINGSCHEMA 16 = STREAM_FLAGS_DONTCACHETEMPLATE 32 = STREAM_FLAGS_DONTCACHEXSL<br /><br /> 다음 표에서는 이러한 값에 대한 추가 정보를 제공합니다.|  
|xml root||이 속성은 결과 XML의 루트 태그를 정의하는 데 사용됩니다. 예를 들어 데이터베이스에 대해 SQL 쿼리를 실행하고 결과 XML 문서에 단일 루트 요소가 없는 경우 이 속성 값을 사용하여 문서에 단일 루트 요소를 추가합니다.<br /><br /> 이 속성을 사용 하는 예는 [SQLXMLOLEDB Provider&#41;&#40;SQL 쿼리 실행 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/executing-sql-queries-sqlxmloledb-provider.md)을 참조 하세요.|  
|xsl||이 속성은 쿼리에서 반환된 XML 문서에 XSL 변환을 적용하려는 경우 XSL 파일 이름을 지정하는 데 사용됩니다.<br /><br /> 지정된 경로는 상대 경로(xyz/abc/MyXSL.xsl) 또는 절대 경로(C:\MyFolder\abc\MyXSL.xsl)일 수 있습니다.<br /><br /> 상대 경로를 지정 하는 경우 기본 경로 속성으로 지정 된 기본 경로를 사용 하 여 상대 경로를 확인 합니다. 기본 경로 속성에 경로가 지정 되지 않은 경우 상대 경로는 현재 디렉터리를 기준으로 합니다.<br /><br /> 이 속성을 사용 하는 예제는 XSL 변환 적용 (SQLXMLOLEDB Provider)을 참조 하세요.|  
  
 다음 표에는 ss 스트림 플래그 속성 값에 대 한 설명이 나와 있습니다.  
  
|속성 값|설명|  
|--------------------|-----------------|  
|STREAM_FLAGS_DISALLOW_URL|매핑 스키마 또는 XSL에 URL을 사용할 수 없습니다.|  
|STREAM_FLAGS_DISALLOW_ABSOLTE_PATH|매핑 스키마 또는 XSL에 대해 지정된 경로는 템플릿 자체의 기본 경로에 상대적이어야 합니다.|  
|STREAM_FLAGS_DISALLOW_QUERY|템플릿에 쿼리를 사용할 수 없습니다.|  
|STREAM_FLAGS_DONTCACHEMAPPINGSCHEMA|매핑 스키마가 캐시되지 않습니다. 이 속성 값은 데이터베이스 스키마가 변경될 수 있는 데이터베이스 개발 단계에서 유용합니다.|  
|STREAM_FLAGS_DONTCACHETEMPLATE|템플릿이 캐시되지 않습니다.|  
|STREAM_FLAGS_DONTCACHEXSL|XSL이 캐시되지 않습니다.|  
  
  
