---
title: OPENQUERY (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OPENQUERY
dev_langs:
- DMX
helpviewer_keywords:
- OPENQUERY statement
ms.assetid: fe57f3a3-a8e6-402c-995e-bd2fe28a7a7c
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ed189fdef9d1d2d96d8100276d3a97779a08ac7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;원본 데이터 쿼리와&gt; -OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  원본 데이터 쿼리를 기존 데이터 원본에 대한 쿼리로 바꿉니다. INSERT, 선택 FROM PREDICTION JOIN 및 선택 FROM NATURAL PREDICTION JOIN 문을 지원 **OPENQUERY**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>인수  
 *명명 된 데이터 원본*  
 데이터 원본에 존재 하는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스입니다.  
  
 *쿼리 구문*  
 행 집합을 반환하는 쿼리 구문입니다.  
  
## <a name="remarks"></a>주의  
 **OPENQUERY** 데이터 원본 권한을 지원 하 여 외부 데이터에 액세스 하는 보다 안전한 방법을 제공 합니다. 연결 문자열은 데이터 원본에 저장되어 있으므로 관리자는 데이터 원본의 속성을 사용하여 데이터에 대한 액세스를 관리할 수 있습니다. 데이터 원본에 대 한 자세한 내용은 참조 [데이터 원본 지원 &#40;SSAS-다차원 데이터&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)합니다.  
  
 쿼리하여 서버에서 사용할 수 있는 데이터 원본 목록을 가져올 수는 **MDSCHEMA_INPUT_DATASOURCES** 스키마 행 집합입니다. 사용에 대 한 자세한 내용은 **MDSCHEMA_INPUT_DATASOURCES**, 참조 [MDSCHEMA_INPUT_DATASOURCES 행 집합](../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)합니다.  
  
 다음 DMX 쿼리를 사용하여 현재 Analysis Services 데이터베이스의 데이터 원본 목록을 반환할 수도 있습니다.  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>예  
 다음 예제에 이미 정의 되어 있는 MyDS 데이터 원본을 사용 하 여는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에 대 한 연결을 만들려는 데이터베이스의 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스 및 쿼리는 **vTargetMail** 보기.  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>관련 항목:  
 [&#60;원본 데이터 쿼리&#62;](../dmx/source-data-query.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions & #40; DMX & #41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
