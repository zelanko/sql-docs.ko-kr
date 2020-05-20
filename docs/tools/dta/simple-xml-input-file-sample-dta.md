---
title: 단순 XML 입력 파일 예제(DTA)
description: 이 문서에는 데이터베이스 엔진 튜닝 관리자에서 사용할 샘플 XML 입력 파일과 튜닝 작업이 포함되어 있습니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 5b00e4eb-1742-43ec-98d8-d84216b6b840
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: cf1b08904c35ebdea6b3365f02e9221d7a3c799a
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151779"
---
# <a name="simple-xml-input-file-sample-dta"></a>단순 XML 입력 파일 예제(DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

튜닝 작업에 사용할 간단한 이 XML 입력 파일 예제를 복사하여 자주 사용하는 XML 편집기나 텍스트 편집기에 붙여넣습니다. 그런 다음 **Server**, **Database**, **Schema**, **Table**, **Workload**및 **TuningOptions** 요소에 지정된 값을 특정 튜닝 세션에 대한 값으로 바꿉니다. 이러한 요소에 사용할 수 있는 특성 및 자식 요소에 대한 자세한 내용은 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)를 참조하세요. 다음 예에서는 사용 가능한 특성 및 자식 요소 옵션의 하위 집합만 사용합니다.  
  
## <a name="code"></a>코드  
 [!code-xml[InputFileSamples#SimpleXMLInputFile](../../tools/dta/codesnippet/xml/simple-xml-input-file-sa_1.xml)]  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 튜닝 관리자 시작 및 사용](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
