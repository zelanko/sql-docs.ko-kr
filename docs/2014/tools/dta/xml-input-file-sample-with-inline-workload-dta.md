---
title: 인라인 작업이 포함된 XML 입력 파일 샘플(DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b53076a7528d0e9eaff1244c206dee4127150e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769535"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>인라인 작업이 포함된 XML 입력 파일 예제(DTA)
  **EventString** 요소를 사용하여 작업을 지정하는 XML 입력 파일의 이 예제를 복사한 다음 자주 사용하는 XML 편집기나 텍스트 편집기에 붙여넣습니다. **EventString** 요소를 사용하면 별개의 작업 파일을 사용하는 대신에 XML 입력 파일에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 작업을 지정할 수 있습니다. 이 예제를 편집 도구에 복사한 후에 **Server**, **Database**, **Schema**, **Table**, **Workload**, **EventString**및 **TuningOptions** 요소에 지정된 값을 특정 튜닝 세션에 대한 값으로 바꿉니다. 이러한 요소에 사용할 수 있는 모든 특성 및 자식 요소에 대한 자세한 내용은 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)를 참조하세요. 다음 예에서는 사용 가능한 특성 및 자식 요소 옵션의 하위 집합만 사용합니다.  
  
## <a name="code"></a>코드  
 [!code-xml[InputFileSamples#InlineWorkloadInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#inlineworkloadinputfile)]  
  
## <a name="comments"></a>주석  
 `USE database_name` EventString **요소에 포함된 인라인 작업에서** 문을 지정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 튜닝 관리자 시작 및 사용](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
