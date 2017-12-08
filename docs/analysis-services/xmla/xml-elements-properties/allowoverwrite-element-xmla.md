---
title: "AllowOverwrite 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AllowOverwrite Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.allowoverwrite
- urn:schemas-microsoft-com:xml-analysis#EndSession
helpviewer_keywords: AllowOverwrite element
ms.assetid: e7e92481-5f29-47f2-9efd-4e5e60c002bb
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8a65790ff5e85497fcff60551c4bc38d1fab75b4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="allowoverwrite-element-xmla"></a>AllowOverwrite 요소(XMLA)
  결정 여부 부모 [백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) 또는 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 명령은 대상 파일이 나 데이터베이스를 덮어쓰려면 하려고 시도 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <AllowOverwrite>...</AllowOverwrite>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **Backup** 명령의 경우 **AllowOverwrite** 요소는 명령으로 **File** 요소에 지정된 백업 파일을 덮어쓸 수 있는지 여부를 결정합니다.  
  
 에 대 한 **복원** 요소는 **AllowOverwrite** 요소 명령을 덮어쓸 수 있는지 여부를 결정은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 는 에지정된데이터베이스**DatabaseName** 요소입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DatabaseName 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/databasename-element-xmla.md)   
 [File 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
