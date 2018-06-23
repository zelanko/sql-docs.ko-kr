---
title: Integration Services 매개 변수 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f178c02cc93d23a14e0fb658398e5f0ba4cf6dc0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089450"
---
# <a name="integration-services-parameters"></a>Integration Services 매개 변수
  에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 분석 하도록 선택할 수 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 컴퓨터에 패키지 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 파일 시스템에 패키지 파일입니다. 파일 시스템에 있는 파일을 분석할 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지가 들어 있는 폴더의 경로를 제공합니다.  
  
## <a name="options"></a>변수  
 **컴퓨터에 있는 SSIS 패키지 분석**  
 컴퓨터에 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 분석하려면 이 옵션을 선택합니다. 기본적으로 이 옵션은 선택되어 있습니다.  
  
 **SSIS 패키지 파일 분석**  
 파일 시스템에 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 분석하려면 이 옵션을 선택합니다.  
  
 **SSIS 패키지의 경로**  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지가 들어 있는 UNC 또는 로컬 경로를 찾습니다. 파일 이름을 포함할 필요는 없습니다. 입력 한 경로 액세스할 수 없는 경우를 클릭할 수 **다음**합니다. 기본적으로 경로는 비어 있습니다. 이 필드는 선택한 경우에 활성화 됩니다 **SSIS 패키지 파일 분석**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [업그레이드 관리자 사용자 인터페이스 참조](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  