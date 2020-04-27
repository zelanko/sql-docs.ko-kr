---
title: '3 단원: dta 명령 프롬프트 유틸리티 사용 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2881a2a118306f9d567236516f05bb29ad2d60a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68186577"
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>3단원: dta 명령 프롬프트 유틸리티 사용
  **dta** 명령 프롬프트 유틸리티는 데이터베이스 엔진 튜닝 관리자에서 제공하는 기능 외에도 많은 기능을 제공합니다.  
  
 자주 사용하는 XML 도구에서 데이터베이스 엔진 튜닝 관리자 XML 스키마를 사용하여 유틸리티의 입력 파일을 만들 수 있습니다. 이 스키마는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치할 때 설치되며 C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd에서 확인할 수 있습니다.  
  
 데이터베이스 엔진 튜닝 관리자 XML 스키마는 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)에서 온라인으로도 제공됩니다.  
  
 데이터베이스 엔진 튜닝 관리자 XML 스키마를 사용하면 튜닝 옵션을 보다 유연하게 설정할 수 있습니다. 예를 들어 "가정(what-if)" 분석을 수행할 수 있습니다. "가정(what-if)" 분석에는 튜닝하려는 데이터베이스에 대해 일련의 기존 및 가상 물리적 디자인 구조를 지정한 다음 데이터베이스 엔진 튜닝 관리자로 분석하여 이 가상 물리적 디자인으로 쿼리 처리 성능이 개선될지 확인하는 작업이 포함됩니다. 이 분석 유형은 실제 구현 시 오버헤드를 발생시키지 않고 새 구성을 평가하는 이점이 있습니다. 가상 물리적 디자인으로 원하는 성능 개선이 이루어지지 않으면 필요한 결과를 만드는 구성에 도달할 때까지 해당 디자인을 쉽게 변경하고 다시 분석할 수 있습니다.  
  
 또한 데이터베이스 엔진 튜닝 관리자 XML 스키마와 **dta** 명령 프롬프트 유틸리티를 사용하면 데이터베이스 엔진 튜닝 관리자 기능을 스크립트에 통합하여 다른 데이터베이스 디자인 도구에서 사용할 수 있습니다.  
  
 데이터베이스 엔진 튜닝 관리자의 XML 입력 기능을 사용하는 방법은 이 단원에서 다루지 않습니다.  
  
 이 단원에서는 기본 **dta** 명령 프롬프트 유틸리티 구문을 소개하고 도움말에 액세스하는 방법과 단순 작업을 튜닝하는 데 유용한 방법을 제공합니다.  
  
 다음 항목이 포함됩니다.  
  
-   **Dta** 명령 프롬프트 유틸리티 시작 및 작업 튜닝  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [dta 명령 프롬프트 유틸리티 시작 및 작업 튜닝](lesson-1-1-tuning-a-workload.md)  
  
  
