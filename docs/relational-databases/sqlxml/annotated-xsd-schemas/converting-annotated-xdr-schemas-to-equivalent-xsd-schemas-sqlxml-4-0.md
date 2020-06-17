---
title: 주석이 추가 된 XDR 스키마를 XSD로 변환 (SQLXML)
description: SQLXML 4.0의 XDR to XSD 변환기 도구를 사용 하 여 주석이 추가 된 XDR 스키마를 해당 XSD 스키마로 변환 하는 방법에 대해 알아봅니다.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XDR schemas, converting schemas
- annotated XSD schemas, converting schemas
- XDR to XSD Converter tool [SQLXML]
- XDR schemas [SQLXML], converting
- converting annotated schemas
- mapping schema [SQLXML], conversions
- XSD schemas [SQLXML], converting schemas
ms.assetid: 151c94a8-66d3-4c46-a5ff-a22df456940a
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0e0932bc7a7bd1b40f260d0eda130aea0711d069
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84883045"
---
# <a name="converting-annotated-xdr-schemas-to-equivalent-xsd-schemas-sqlxml-40"></a>주석이 추가된 XDR 스키마를 해당 XSD 스키마로 변환(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSD(XML 스키마 정의) 언어는 XDR(XML-Data Reduced) 스키마 정의 언어의 후속 제품입니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0에서는 새로 XSD를 지원하므로 XSD를 사용하여 주석이 추가된 새 스키마를 만들 수 있습니다. SQLXML 4.0에는 기존의 주석이 추가된 XDR 스키마를 해당하는 XSD 스키마로 변환하는 데 도움을 주기 위한 XDR-XSD 변환기 도구가 포함되어 있습니다.  
  
> [!IMPORTANT]  
>  주석이 추가된 스키마를 SQLXML 4.0에서 사용하기 위해 XSD로 변환하려는 경우에만 이 도구를 사용합니다. 이 도구는 범용 XDR-XSD 변환 도구가 아닙니다. 따라서 변환된 XSD 스키마를 다른 환경에서 사용할 경우 원래 XDR 스키마와 동일하게 동작하지 않을 수도 있습니다.  
  
 입력 XDR 파일에서 XML 선언 내에 인코딩을 지정하는 경우 이것이 생성되는 XSD 출력 파일의 인코딩이 될 수 있습니다.  
  
 변환기 도구(Cvtschema.exe)는 Program Files\SQLXML 4.0\bin 폴더에 설치되며 명령 프롬프트에서 실행됩니다.  
  
 일반 구문은 다음과 같습니다.  
  
```  
cvtschema XDRFileName, [-y], [-w] [-?]  
```  
  
 위치:  
  
 XDRFileName  
 XSD로 변환될 XDR 파일의 이름입니다. 이 도구는 입력 XDR 파일을 읽어 들이고 현재 디렉터리에 XSD 출력 파일을 생성합니다. 입력 파일의 확장명이 .xdr 또는 .xml인 경우 생성되는 출력 XDR 파일은 이름은 같지만 확장명은 .xsd입니다. 입력 파일 이름 확장명이 .xml 또는. n e t이 아닌 경우 (또는 확장이 없는 경우) 출력 파일은 동일한 이름으로 만들어지고 확장명이 .xsd 인 확장명이 입력 파일 이름에 추가 됩니다. 예를 들어 입력 XDR 파일 이름이 SampleFile.abc인 경우 결과 XSD는 SampleFile.abc.xsd로 저장됩니다.  
  
 -y  
 (옵션) 기존 XSD 파일을 변환기 도구에서 생성되는 XSD 파일로 덮어씁니다. 이 플래그를 지정하지 않으면 도구에서는 기존 XSD 파일을 덮어쓸지 여부를 지정하라는 메시지를 표시하고 출력 파일 이름을 변경할 수 있는 옵션을 제공합니다.  
  
 -w  
 (옵션) 도구의 변환 프로세스에서 생성된 심각하지 않은 경고를 반환합니다. 기본적으로 심각한 오류에 대한 메시지만 표시됩니다.  
  
 -?  
 설명과 함께 **cvtschema**를 사용 하 여 지정할 수 있는 옵션의 목록을 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [&#40;SQLXML 4.0&#41;XSD 데이터 형식을 XPath 데이터 형식에 매핑](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)   
 [&#40;SQLXML 4.0&#41;XSD 주석](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
  
  
